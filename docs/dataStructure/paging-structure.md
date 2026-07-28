# 페이징 응답 규격 ***(paging response structure)***
[SearchMode](/docs/props/cfg/search-mode) 3, 4, 5에서 [doSearchPaging](/docs/funcs/core/do-search-paging) 함수로 데이터 바인딩 시 사용되는 `서버 응답 데이터 구조`를 정의합니다.

## 기본 응답 규격
- 서버 응답 데이터는 `Data` 속성을 최상위로 가지고 있으며, `Data` 속성 안에는 각각의 항목이 객체 형태로 들어 있는 배열이 포함되어 있습니다.
- `Data` 배열의 길이는 `(Cfg) PageLength` 설정 값을 기준으로 하며, 마지막 페이지의 경우 해당 값보다 작을 수 있습니다.
- 반드시 `Total` 속성에는 DB 전체 데이터 건수가 포함되어야 하며, 페이징 UI 계산에 사용됩니다.
- 시트는 `doSearchPaging` 호출 시 서버로 `ibpage`(페이지 번호)와 `ibpagelength`(페이지당 데이터 수) 파라미터를 자동으로 전송합니다.
- 그 외 속성이나 데이터 형식, 에러 처리(IO, Result 코드)는 [조회 응답 규격](/docs/dataStructure/data-structure)을 참고하세요.


```js
//서버 응답 예시: cfg.PageLength 개수만큼 Data 배열 포함
{"Data":
    [
        {"sa_name":"홍길동","sa_no":"940154","sa_dept":"A021"},
        {"sa_name":"김지수","sa_no":"950757","sa_dept":"B022"}
    ],
 "Total":25410      //<-- DB상의 전체 건수
}
```
```jsp
// ※ 예제 코드이며, 실제 서비스에서는 DB / SQL / 페이징 방식에 맞게 수정 필요
// 서버 예제
import java.io.IOException;
import java.sql.*;
import javax.servlet.*;
import javax.servlet.http.*;
import org.json.JSONArray;
import org.json.JSONObject;

public class PagingExampleServlet extends HttpServlet {
    protected void doGet(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {

        response.setContentType("application/json;charset=UTF-8");

        Connection conn = null;
        PreparedStatement pstmt = null;
        ResultSet rs = null;
        
        // 요청 페이지
        int page = Integer.parseInt(request.getParameter("ibpage")); 
        // 페이지당 데이터 수, (Cfg) PageLength에 설정한 개수와 동일
        int pageLength = Integer.parseInt(request.getParameter("ibpagelength")); 
        int total = 0; // 전체 건수

        try {
            conn = getConnection(); // DB 연결

            // 1. 최초 조회 시 전체 건수 확인
            if (page == 1) {
                pstmt = conn.prepareStatement("SELECT COUNT(1) AS CNT FROM TABLE_NAME");
                rs = pstmt.executeQuery();
                if (rs.next()) {
                    total = rs.getInt("CNT");
                }
                rs.close();
                pstmt.close();
            }

            // 2. 페이지 계산
            int startRow = (page - 1) * pageLength + 1;
            int endRow = startRow + pageLength - 1;

            // 3. 데이터 조회 (ROWNUM 기반)
            StringBuilder sb = new StringBuilder();
                          sb.append("SELECT * FROM (")
                         .append("  SELECT ROWNUM RN, EMP, EMP_NO, DEPT ")
                         .append("  FROM (SELECT EMP, EMP_NO, DEPT FROM TABLE_NAME ORDER BY EMP_NO)")
                         .append(") WHERE RN BETWEEN ? AND ?");

            String query = sb.toString();

            pstmt = conn.prepareStatement(query);
            pstmt.setInt(1, startRow);
            pstmt.setInt(2, endRow);
            rs = pstmt.executeQuery();

            // 4. JSON 객체 생성
            JSONObject json = new JSONObject();
            JSONArray dataArr = new JSONArray();

            while (rs.next()) {
                JSONObject row = new JSONObject();
                row.put("RN", rs.getInt("RN"));
                row.put("EMP", rs.getString("EMP"));
                row.put("EMP_NO", rs.getString("EMP_NO"));
                row.put("DEPT", rs.getString("DEPT"));
                dataArr.put(row);
            }

            json.put("Data", dataArr);
            json.put("Total", total);

            // 5. JSON 출력
            response.getWriter().print(json.toString());

        } catch (Exception e) {
            e.printStackTrace();
            response.getWriter().print("{\"error\":\""+e.getMessage()+"\"}");
        } finally {
            try { if(rs!=null) rs.close(); } catch(Exception e) {}
            try { if(pstmt!=null) pstmt.close(); } catch(Exception e) {}
            try { if(conn!=null) conn.close(); } catch(Exception e) {}
        }
    }

    private Connection getConnection() throws SQLException {
        // 예시: Oracle DataSource 또는 DriverManager 사용
        // return DriverManager.getConnection(dbUrl, user, password);
        return null;
    }
}
```

### Read More
- [SearchMode cfg](/docs/props/cfg/search-mode)
- [doSearchPaging method](/docs/funcs/core/do-search-paging)
- [getChangedData method](/docs/funcs/core/get-changed-data)
- [onReceiveData](/docs/events/on-receive-data)
- [onBeforeDataLoad](/docs/events/on-before-data-load)
- [onDataLoad](/docs/events/on-data-load)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|

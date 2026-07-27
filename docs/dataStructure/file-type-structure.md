# File Type(파일) 응답 규격 ***(file-type response structure)***
`File Type` 컬럼은 시트에서 파일 업로드 및 다운로드를 지원합니다.<br/>
서버와 통신 시 `조회/저장/응답 데이터`의 구조가 일정해야 하며, 아래와 같이 정리할 수 있습니다.

## 주의 사항
- 파일 업로드(추가/편집) 후, 셀을 클릭해도 서버 호출(다운로드)이 자동으로 발생하지 않습니다.
- 조회 데이터에는 반드시 `Path` 또는` Cfg.Export.FilePath`가 설정되어 있어야 셀에 데이터가 표시됩니다.

## 1. 조회 응답 규격
조회 데이터는 다음 규칙에 따라 구성해야 합니다.
- 파일의 이름 : (Col) Name
- 파일의 저장 경로 : (Col) Name + "Path"
- 별칭 정보 : (Col) Name + "Alias"(선택 사항. 미설정시 lblist로 값이 표시됨)
- Cfg.Export.FilePath가 설정된 경우, Path 설정 없어도 다운로드 가능 합니다.

```javascript
// 컬럼 설정 예시
Cols: [
    {Header: "파일", Type: "File", Name: "lblist", Width: 300, Align: "Center"}
]

// 서버 응답 예시
{
  "data": [
    {
      "lblist": "file.xlsx",         // 실제 파일 이름
      "lblistPath": "/customer-sample/", // 파일 저장 경로
      "lblistAlias": "파일.xlsx"     // 화면에 표시될 별칭
    }
  ]
}
```

## 2. 저장
File Type 컬럼 데이터를 저장할 때는 [doSave](/docs/funcs/core/do-save) 또는 Ajax 통신 후 [applySaveResult](/docs/funcs/core/apply-save-result)를 이용하여 결과를 시트에 반영할 수 있습니다.<br/>
시트의 파일 데이터는 `rowID$colName: (binary)` 형태로 서버에 전송됩니다.
```javascript

var url = '../jsp/samples/customer/file_save.jsp';

//doSave 저장 예시
sheet.doSave({
    url: url,
    queryMode: 0,
});


//ajax 저장 예시
var saveData = sheet.getSaveJson({ formData: true}); //시트의 데이터와 file를 추출

//추출된 데이터를 서버로 전송
$.ajax({
  	url: url,
      	data: saveData,
      	method: "POST",
      	enctype: 'multipart/form-data',
      	contentType: false,
      	processData: false,
      	cache: false,
      	success:function(data){
      	      var result = data.IO.Result;
      	      var fileData = data.IO.data;

     	      //결과를 시트에 반영한다.
              //저장처리 이후 파일 다운로드 동작을 하려면 fileData에 값을 전달해야 한다.
              // applySaveResult(result, message, response, files)
      	      sheet.applySaveResult(result, null, null, fileData);
     	}
});
```
## 3. 저장 응답 규격
- `id`는 시트의 `Row ID`와 매핑되며,해당 Row의 File 타입 셀에 파일 정보가 반영됩니다.
- 저장 후 파일 다운로드를 위해 data 항목이 필요합니다.

## 성공 응답
```javascript
// 서버에서 시트로 보낼 응답 규격
// 성공 시
{"IO": {
    "Result": 0 ,
    "Message": "저장 되었습니다.",
    "data":[ 
            //저장처리 이후 파일 다운로드 하려면 필요
            {"file":"file.xlsx", "filePath":"/customer-sample/", "id":"AR7"},
            {"file":"file1.xlsx", "filePath":"/customer-sample/", "id":"AR4"},
           ]
    }
}
```
## 실패 응답

```javascript
// 실패 시 Result 값을 음수로 설정.
{"IO": {"Result": -9, "Message":"오류내용..." }}
```

## 서버 예제(JSP)
```jsp
<%@ page language="java" contentType="application/json; charset=UTF-8" pageEncoding="UTF-8"%>
<%@ page import="java.util.*, javax.servlet.http.Part, com.ibleaders.utility.ib_json.*"%>

<%!
    /**
     * 업로드된 파일의 실제 파일명을 반환한다.
     */
    public String getFilename(Part part) {
        for (String cd : part.getHeader("content-disposition").split(";")) {
            if (cd.trim().startsWith("filename")) {
                String filename = cd.substring(cd.indexOf('=') + 1)
                                     .trim()
                                     .replace("\"", "");
                return filename.substring(
                        Math.max(filename.lastIndexOf('/'), filename.lastIndexOf('\\')) + 1
                );
            }
        }
        return null;
    }
%>

<%
    request.setCharacterEncoding("UTF-8");
    response.setContentType("application/json; charset=UTF-8");
    response.setStatus(200);

    boolean process = false;     // 전체 처리 성공 여부
    boolean hasFile = false;     // 파일 처리 여부

    JSONArray jsonArr = new JSONArray();   // 시트에 반영할 파일 정보

    try {
        Collection<Part> parts = request.getParts();

        for (Part part : parts) {

            // ===== File 타입 데이터 처리 =====
            if (part.getHeader("Content-Disposition") != null &&
                part.getHeader("Content-Disposition").contains("filename=")) {

                hasFile = true;

                // 파라미터명 규칙: rowID$colName
                String fileParam = part.getName();
                String id  = fileParam.split("\\$", 2)[0];
                String col = fileParam.split("\\$", 2)[1];

                String filename = getFilename(part);

                // ※ 예제용 경로 (실제 서비스에서는 환경에 맞게 변경 필요)
                String filepath = "C:/myPath/temp/";
                part.write(filepath + filename);

                // 시트 반영용 파일 정보 구성
                JSONObject file = new JSONObject();
                file.put("id", id);
                file.put(col, filename);
                file.put(col + "Path", filepath);

                jsonArr.add(file);

            } else {
                // ===== 일반 데이터 처리 =====
                // (필요 시 컬럼 값 처리)
                String colName = part.getName();
                String value = request.getParameter(colName);
            }
        }

        // 파일이 하나라도 정상 처리되면 성공으로 간주
        process = hasFile;

    } catch (Exception ex) {
        // 파일 저장 또는 파싱 중 오류 발생
        process = false;
    }

    // ===== IBSheet 응답 데이터 구성 =====
    JSONObject result = new JSONObject();
    JSONObject IO = new JSONObject();

    int res = process ? 0 : -9;  // Result 오류는 음수 사용 (-1 ~ -7 제외)

    IO.put("Result", res);
    IO.put("Message", process ? "저장 되었습니다." : "파일 저장 중 오류가 발생했습니다.");

    if (process) {
        // 저장 후 파일 다운로드 가능하게 하기 위해 file 정보 전달
        IO.put("data", jsonArr);
    }

    result.put("IO", IO);

    out.print(result);
%>

```

### Read More
- [Alias cell](/docs/props/cell/Alias)
- [applySaveResult method](/docs/funcs/core/apply-save-result)
- [doSave method](/docs/funcs/core/do-save)
- [doSearch method](/docs/funcs/core/do-search)
- [getSaveJson method](/docs/funcs/core/get-save-json)
- [loadSearchData method](/docs/funcs/core/load-search-data)
- [onSetFile event](/docs/events/on-set-file)
- [onCancelFile event](/docs/events/on-cancle-file)
- [onBeforeFileDown event](/docs/events/on-before-file-down)
- [Path cell](/docs/props/cell/Path)
- [type appendix](/docs/appx/type)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|

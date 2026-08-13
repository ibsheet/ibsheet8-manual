# directDown2Excel ***(method)***

<!-- synonyms: 서버 데이터 엑셀 다운로드, direct down to excel, 대용량 엑셀 다운로드, 서버 조회 결합 엑셀, 여러 시트 다운로드, 다중 워크시트, 여러 워크시트 한 파일, 시트 여러개 엑셀, down2ExcelBuffer, 서버 데이터 다중시트, SHEETDATA1, SHEETDATA2 -->

> 시트의 조회 데이터는 무시하고 시트 정보(컬럼 정의 등)만 서버로 전송해, 서버에서 별도로 만든 데이터와 결합해 엑셀 파일을 생성하고 다운로드합니다.  
> 시트의 조회 데이터 대신 서버에서 직접 만든 데이터로 엑셀을 생성하는 경우 사용합니다.  
> 사용 전 [서버모듈 설치](/docs/appx/import-export)와 `/plugins/ibsheet-excel.js` 스크립트 로드가 필요합니다.  
> 이 함수를 호출하면 `url` 인자로 지정한 서버 페이지가 호출됩니다.  
> 이 페이지에서 `List<Map>` 구조의 데이터를 만들어 `SHEETDATA`라는 이름으로 `request` 객체에 담아 `DirectDown2Excel.jsp`(또는 `DirectDown2Excel.aspx`)로 `forward`합니다.  
> `DirectDown2Excel.jsp` 페이지에서 시트 정보(컬럼 정의 등)와 결합해 엑셀 파일을 생성해 클라이언트로 전송합니다.  
> 서버에서 별도로 만든 데이터이므로 데이터 행의 머지(셀 병합), 합계행, 색상 정보 등은 반영되지 않습니다.   
> 화면에 보이는 그대로 다운로드하려면 [down2Excel](./down-to-excel)을 사용하세요.

![DirectDown2Excel 과정](/assets/imgs/directdown2excel_process.png)

다운로드가 서버에서 실패하면 오류 메시지는 [onExportFinish](/docs/events/on-export-finish)의 `message`로 전달됩니다(`result`가 `0`일 때). 중계 페이지에서 조건에 따라 오류 메시지를 내보내는 방법은 [엑셀 서버 모듈 트러블슈팅](/docs/appx/excel-server-troubleshooting)을 참고하세요.


### Syntax
```javascript
void directDown2Excel( param );
```

### Parameters

|Name|Type|Required|Description|
|----------|-----|---|----|
|url|`string`|<span class='required'>필수</span>|데이터를 조회할 서버 url|
|extendParam|`string`|<span class='optional'>선택</span>|url로 전달할 parameter(querystring형식으로 작성)|
|extendParamMethod|`string`|<span class='optional'>선택</span>|`extendParam`의 내용을 `GET` 또는 `POST`로 전달할지를 설정합니다. (`default: "GET"`)|
|multipart|`boolean`|<span class='optional'>선택</span>|url로 전송시 Content-Type 설정<br>`0(false)`:일반적인 POST로 전송<br>`1(true)`:Content-Type을 multipart로 전송 (`default`)|
|fileName|`string`|<span class='optional'>선택</span>|생성할 엑셀파일 명 (`default: "Excel.xlsx"`) <br/>**이 속성에서 파일명과 함께 확장자를 xls, xlsx로 붙이느냐에 따라서 생성 파일이 xls형식이나, xlsx형식으로 만들어집니다.<br>가급적 xlsx 형식으로 다운로드 하실 것을 권합니다.**<br/>파일 이름에 쓸 수 없는 특수문자(`\ / : * ? " < > \|`)가 포함되면 다운로드한 파일을 열 때 복구 경고가 뜨거나 손상될 수 있으니 제거하세요.|
|sheetName|`string`|<span class='optional'>선택</span>|만들어지는 엑셀 파일의 WorkSheet에 부여할 이름<br/>워크시트 이름에 쓸 수 없는 특수문자(`\ / ? * [ ] :`)가 포함되면 다운로드한 파일을 열 때 복구 경고가 뜨거나 손상될 수 있으니 제거하세요.|
|downCols|`string`|<span class='optional'>선택</span>|구분자를 통해 지정한 열만 다운로드 합니다.<br/> 별도의 설정이 없으시 모든 열이 다운로드 됩니다.<br/>(ex: "Price\|AMT\|TotalReward" 식의 컬럼 명을 구분자("\|")로 연결한 문자열)|
|sheetDesign|`number`|<span class='optional'>선택</span>|`main.css` 파일에 설정된 시트의 디자인 요소를 엑셀에도 반영할지 여부를 설정합니다.<br/>반영되는 디자인 요소는 다음과 같습니다.<br/>헤더의 배경색(`main.css` 파일에 설정한 `IBCellHeader` class 속성값), 헤더의 폰트 색상(`main.css` 파일에 설정한 `IBHeaderText` class 속성값), 폰트명(`main.css` 파일에 설정한 `IBMain` class 속성값, excelFontFamily로 재지정 가능), 폰트크기(`main.css` 파일에 설정한 `.IBMain, .IBMain *` 값, excelFontSize 속성으로 재지정 가능)<br/>`0`:셀 외곽선을 제외한 모든 디자인을 적용하지 않습니다.<br/>`1`:셀 외곽선을 포함해 모든 디자인을 적용합니다. (`default`)<br/>`2`:셀 외곽선을 제외한 셀 스타일을 적용합니다.<br/>`3`:셀 외곽선 및 스타일을 모두 적용하지 않습니다.|
|merge|`boolean`|<span class='optional'>선택</span>|헤더 영역에 대한 머지 정보를 엑셀에 반영할지 여부<br>`0(false)`:헤더 영역에 대한 머지 정보 엑셀에 반영 안함 (`default`)<br>`1(true)`:헤더 영역에 대한 머지 정보 엑셀에 반영|
|numberFormatMode|`number`|<span class='optional'>선택</span>|실수 형태의 데이터 타입에 대한 셀 서식 설정 방식을 설정합니다.<br/>`0`:시트의 컬럼 포맷을 따릅니다. (`default`)<br/>`1`:셀의 값 기준에 따라 정수 또는 실수 형태로 셀 서식을 설정합니다.<br/>`2`:일반 서식으로 설정합니다.|
|titleText|`string`|<span class='optional'>선택</span>|엑셀 문서의 상단에 원하는 문자를 추가합니다.<br/> 문자는 열구분자("\|")와 행구분자("\r\n")을 통해서 작성하실수 있습니다.<br/>가령 "A\|B\|C\r\nD\|E\|F" 와 같이 입력한 경우 첫 행에 3개의 셀에 각각 A,B,C 값이 들어가고 두번째 행의 3개의 셀에 각각 D,E,F 값이 입력됩니다. 값 안에서 엔터를 포함하려면 \r 이나 \n 을 삽입하면 됩니다. \r\n 이 10개가 포함되면 11줄을 차지하게 되고 12번째 행부터 시트 내용이 출력됩니다.|
|titleAlign|`string`|<span class='optional'>선택</span>|titleText로 삽입한 문자들에 대한 좌우 정렬 (`default: "center"`, "left","right"선언가능)|
|downCombo|`string`|<span class='optional'>선택</span>|`Enum` 타입의 선택 항목을 `Enum` 속성과 `EnumKeys` 속성 어떤 형태로 다운로드를 받을 지 설정합니다.<br/> `TEXT`: `Enum` 속성을 사용하여 다운로드 합니다. (`default`)<br/> `CODE`: `EnumKeys` 속성을 사용하여 다운로드합니다.|
|userMerge|`string`|<span class='optional'>선택</span>|TitleText와 더불어 사용하면서 엑셀 안에 원하는 영역을 머지(병합)합니다.<br/> 입력방법은 4개의 숫자로 <br/>"머지시작셀 row index,머지시작셀 col index,아래로 병합할 행 개수(1을 설정하면 병합 없음),우측으로 병합할 개수"<br/>로 이루어 집니다.(여러개 병합시에는 띄어쓰기로 구분)<br/>가령 "2,2,1,6 3,2,3,3"위와 같이 설정하였다면 2,2 셀부터 오른쪽으로 6칸이 병합되고, 3,2 셀부터 아래로 3칸,오른쪽으로 3칸이 병합 됩니다.<br/>![userMerge](/assets/imgs/userMerge.png)|
|excelRowHeight|`number`|<span class='optional'>선택</span>|엑셀 문서의 행 높이를 설정합니다.|
|excelHeaderRowHeight|`number`|<span class='optional'>선택</span>|엑셀의 헤더행의 높이를 설정합니다.|
|excelFontSize|`number`|<span class='optional'>선택</span>|엑셀의 폰트 크기를 설정합니다.<br/>미지정 시 `main.css`의 `.IBMain, .IBMain *`에 설정된 폰트 크기가 기본 적용되며, 화면과 다른 크기로 내리려면 이 값을 지정합니다.|
|excelFontFamily|`string`|<span class='optional'>선택</span>|엑셀의 폰트(글꼴)를 설정합니다.<br/>미지정 시 `main.css`의 `.IBMain`에 설정된 폰트명이 기본 적용되며, 화면과 다른 글꼴로 내리려면 이 값을 지정합니다.|
|comboValidation|`boolean`|<span class='optional'>선택</span>|Enum 타입으로 만들어진 열에 대해 엑셀에서도 데이터 기능을 통해 드롭다운리스트 형태로 표현합니다.<br/>Enum의 종류가 많은 경우 무시됩니다.<br>`0(false)`:드롭다운리스트 형태 사용 안함 (`default`)<br>`1(true)`:드롭다운리스트 형태 사용|
|reqHeader|`object`|<span class='optional'>선택</span>|서버 전송 헤더에 사용자가 지정한 헤더 정보를 설정합니다.|
|useXhr|`boolean`|<span class='optional'>선택</span>| xhr 통신을 이용해 엑셀 파일을 다운로드받습니다.<br>`0(false)`:xhr 통신 사용 안함 (`default`)<br>`1(true)`:xhr 통신 사용|
|exHead|`object`|<span class='optional'>선택</span>|시트 상단에 표시하고 싶은 내용을 설정합니다.<br>titleText, userMerge, header, footer 속성과 같이 사용할 수 없으며, 같이 사용시 titleText, userMerge, header, footer속성은 무시됩니다. <br> 해당 속성은 poi를 사용하는 경우에만 설정이 가능합니다.|
|exFoot|`object`|<span class='optional'>선택</span>|시트 하단에 표시하고 싶은 내용을 설정합니다.<br>titleText, userMerge, header, footer 속성과 같이 사용할 수 없으며, 같이 사용시 titleText, userMerge, header, footer속성은 무시됩니다. <br> 해당 속성은 poi를 사용하는 경우에만 설정이 가능합니다.|
<!--!
|`[비공개]` hiddenColumn|`boolean`|<span class='optional'>선택</span>|시트 내에 감춰진 열을 엑셀에서도 "열 숨기기" 형태로 다운로드 합니다.<br>`0(false)`:감춰진 열 다운로드 시 미포함 (`default`)<br>`1(true)`:감춰진 열 "열 숨기기" 형태로 다운로드 시 포함|
!-->


### Return Value
***none***

### Example
```javascript
var param = {
        url:"./apex/yearApexDataList.do",
        extendParam:"year=2019&deptNo=0041",
        fileName:"년단위 결산 정보.xlsx"
};
sheet.directDown2Excel(param);
```

```java
//directDown2Excel 자바 서버모듈 예시
String[] sido = { "서울특별시", "수원시", "성남시" };
String[] sigungu = { "관악구", "팔달구", "분당구" };

List<Map<String, Object>> data = new ArrayList<>();

for (int i = 0; i < sido.length(); i++) {
  Map<String, Object> row = new HashMap<>();

  row.put("sSido", sido[i]);
  row.put("sSiGunGu", sigungu[i]);

  data.add(row);
}

request.setAttribute("SHEETDATA", data);

String forwardPath = "./DirectDown2Excel.jsp";
if (!"".equals(forwardPath)) {
  RequestDispatcher rd = request.getRequestDispatcher(forwardPath);
  rd.forward(request, response);
}
```

조회 결과가 조건에 맞지 않는 등 **다운로드를 중단해야 할 때**는, `forward` 대신 `IBSheetDown`의 `getDownError`로 오류 응답을 내려보냅니다.

```java
// [오류 처리] 조건에 맞지 않으면 forward 대신 getDownError로 오류 응답
List<Map<String, Object>> data = queryData(request);   // 서버에서 데이터 조회

if (data.size() > 100000) {                            // 오류 조건 (예: 건수 초과)
    IBSheetDown down = new IBSheetDown();
    down.setService(request, response);                // getDownError가 response를 사용 → 필수
    OutputStream out = response.getOutputStream();
    out.write(down.getDownError("조회 건수가 너무 많습니다. 기간을 나누어 조회해 주세요."));
    out.flush();
} else {                                                // 정상: SHEETDATA 담아 forward
    request.setAttribute("SHEETDATA", data);
    request.getRequestDispatcher("./DirectDown2Excel.jsp").forward(request, response);
}
```

클라이언트는 [onExportFinish](/docs/events/on-export-finish)의 `result`로 성공(`1`)/실패(`0`)를 판정하고, 실패 시 `message`로 안내합니다.  
오류 처리 상세(오류 메시지 작성 주의 등)는 [엑셀 서버 모듈 트러블슈팅](/docs/appx/excel-server-troubleshooting)을 참고하세요.

```cs
// directDown2Excel 닷넷 서버모듈 예시
// 엑셀로 내려질 데이터를 DB에서 조회 
String connectionString = "Provider=Microsoft.JET.OLEDB.4.0;data source=C:\\mdb\\bussinessList.mdb";
String query = "SELECT * FROM bussinessList";

OleDbConnection conn = new OleDbConnection(connectionString);
OleDbCommand cmd = new OleDbCommand(query, conn);
conn.Open();

OleDbDataReader reader = cmd.ExecuteReader();

// 데이터를 List(Dictionary -> Object)형태로 전환.
// Dictionary 데이터 생성 시 key는 반드시 시트 컬럼의 Name과 동일해야 함.
List<Object> li = new List<object>();
while (reader.Read()) {
  Dictionary<String, String> row = new Dictionary<string, string>();
  for (int i = 0; i < reader.FieldCount; i++) {
    row[reader.GetName(i)] = reader.GetValue(i).ToString();
  }

  li.Add(row);
}

reader.Close();
conn.Close();

this.Context.Items["SHEETDATA"] = li; 

// DirectDown2Excel.aspx 페이지로 forwarding             
String forwardPath = "./DirectDown2Excel.aspx"; 
if(forwardPath != "") {
  Server.Execute(forwardPath);
}

```

**여러 워크시트로 다운로드** — [down2ExcelBuffer](/docs/funcs/excel/down-to-excel-buffer)로 감싸면 여러 시트를 하나의 엑셀 파일(여러 워크시트)로 내릴 수 있습니다. 버퍼 안에서 각 시트의 `directDown2Excel`을 호출하고, 서버(중계 페이지)는 시트 수만큼 `SHEETDATA`, `SHEETDATA1`, `SHEETDATA2` … 속성에 각 시트 데이터를 담습니다. (첫 시트는 `SHEETDATA`(번호 없음), 이후 `SHEETDATA`+인덱스)

```javascript
// 클라이언트: 버퍼로 감싸 여러 시트를 한 파일로
sheet1.down2ExcelBuffer(true);
sheet1.directDown2Excel({ url: "./salesData.do", fileName: "multi.xlsx", sheetName: "1분기" });
sheet2.directDown2Excel({ url: "./salesData.do", sheetName: "2분기" });
sheet3.directDown2Excel({ url: "./salesData.do", sheetName: "3분기" });
sheet1.down2ExcelBuffer(false);   // 종료 → 다운로드 시작
```

```java
// 서버(중계 페이지): 시트 수만큼 SHEETDATA 세팅 (첫 시트 = SHEETDATA, 이후 SHEETDATA1, SHEETDATA2 ...)
request.setAttribute("SHEETDATA",  sheet1List);
request.setAttribute("SHEETDATA1", sheet2List);
request.setAttribute("SHEETDATA2", sheet3List);

RequestDispatcher rd = request.getRequestDispatcher("./DirectDown2Excel.jsp");
rd.forward(request, response);
```

```javascript
//exHead 사용 예제
var param = {
          url: "./apex/yearApexDataList.do",
          extendParam: "year=2022&deptNo=0041",
          sheetDesign: 1,
          merge: 1,
          fileName: '22년도_근무외수당.xlsx'
        };

        param["exHead"] = [
          { // 첫번째 행
            Height: 30,
            Cells:[
              {
                // 첫번째 셀에 이미지 설정
                Type:"Img",
                Value:"|/assets/imgs/logo.png|78|28"
              },
              {},{},{},{},{},{},{}, //7칸 빈셀
              {
                Type:"Text",
                Value:"(취급주의)대외비",
                TextColor:"#FF0000",
                Wrap: 0,
                TextSize: 14
              }
            ]
          }, 
          { // 두번째 행
            Height: 40,
            Cells:[
              {}, //첫칸 빈셀
              {
                Type:"Text",
                Align: "Center",
                Value: "2022년 근무 외 수당 청구 내역",
                Color:"#DEDEDE",
                TextSize: 45,
                TextStyle: 1,
                BorderTop:"2 dashed #0000FF",
                BorderBottom:"2 dashed #0000FF",
                BorderLeft:"2 dashed #0000FF",
                ColSpan: 8
              },
              {
                BorderTop:"2 dashed #0000FF",
                BorderBottom:"2 dashed #0000FF"
              },
              {
                BorderTop:"2 dashed #0000FF",
                BorderBottom:"2 dashed #0000FF"
              },
              {
                BorderTop:"2 dashed #0000FF",
                BorderBottom:"2 dashed #0000FF"
              },
              {
                BorderTop:"2 dashed #0000FF",
                BorderBottom:"2 dashed #0000FF"
              },
              {
                BorderTop:"2 dashed #0000FF",
                BorderBottom:"2 dashed #0000FF"
              },
              {
                BorderTop:"2 dashed #0000FF",
                BorderBottom:"2 dashed #0000FF"
              },
              {
                BorderTop:"2 dashed #0000FF",
                BorderBottom:"2 dashed #0000FF",
                BorderRight:"2 dashed #0000FF"
              }
            ]
          },
          {}, // 3번째 행 (빈행)
          {// 4번째 행
            Cells:[
              {
                Value:"부서",
                Align:"Right",
                Color:"#DEDEDE",
                BorderTop:"1 solid #222222",
                BorderRight:"1 solid #222222",
                BorderBottom:"1 solid #222222",
                BorderLeft:"1 solid #222222",
              },{
                ColSpan: 3,
                Value:"총무부",
                Align:"Left",
                BorderTop:"1 solid #222222",
                BorderRight:"1 solid #222222",
                BorderBottom:"1 solid #222222",
                BorderLeft:"1 solid #222222",
              },
              {
                BorderTop:"1 solid #222222",
                BorderBottom:"1 solid #222222"
              },
              {
                BorderTop:"1 solid #222222",
                BorderBottom:"1 solid #222222",
                BorderRight:"1 solid #222222"
              }
            ]
          },
          {// 5번째 행
            Cells:[
              {
                Value:"기간",
                Align:"Right",
                Color:"#DEDEDE",
                BorderTop:"1 solid #222222",
                BorderRight:"1 solid #222222",
                BorderBottom:"1 solid #222222",
                BorderLeft:"1 solid #222222",
              },
              {
                ColSpan: 3,
                Value:"2022/01/01 ~ 2022/12/31",
                Align:"Left",
                BorderTop:"1 solid #222222",
                BorderBottom:"1 solid #222222",
                BorderLeft:"1 solid #222222",
              },
              {
                BorderTop:"1 solid #222222",
                BorderBottom:"1 solid #222222"
              },
              {
                BorderTop:"1 solid #222222",
                BorderBottom:"1 solid #222222",
                BorderRight:"1 solid #222222"
              }
            ]
          }
        ];
        param["exFoot"] = [
          {}, //첫번째 행 (빈행)
          { 
            Height:30,
            Cells:[
              {
                Value: "출력: 2023-06-23 홍길동",
                Align: "Left",
                Wrap: 0
              }
            ]
          }
        ];


        sheet.directDown2Excel(param);

```
![exHead,exFoot](/assets/imgs/exportDataExHeadExFoot.png "exHead,exFoot")

### Read More
- [down2Excel method](./down-to-excel)
- [down2ExcelBuffer method](./down-to-excel-buffer)
- [directLoadExcel method](./direct-load-excel)
- [exportData method](/docs/funcs/core/export-data)
- [SearchMode cfg](/docs/props/cfg/search-mode)
- [onBeforeExport event](/docs/events/on-before-export)
- [onExportFinish event](/docs/events/on-export-finish)
- [엑셀 업로드/다운로드 설정 appendix](/docs/appx/import-export)
- [엑셀 서버 모듈 트러블슈팅 appendix](/docs/appx/excel-server-troubleshooting)
- [엑셀 DRM 처리 appendix](/docs/appx/excel-drm)
- [엑셀 비밀번호 설정 appendix](/docs/appx/excel-password)

### Since

|product|version|desc|
|---|---|---|
|excel|0.0.0|기능 추가|
|excel|0.0.8|`reqHeader` 기능 추가|

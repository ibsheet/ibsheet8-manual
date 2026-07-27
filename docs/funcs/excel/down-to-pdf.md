# down2Pdf ***(method)***

<!-- synonyms: PDF 다운로드, PDF 내보내기, down to pdf, 시트 PDF 출력 -->

> 시트의 내용을 PDF 파일로 다운로드합니다.  
> 사용 전 [서버모듈 설치](/docs/appx/import-export)와 `/plugins/ibsheet-excel.js` 스크립트 로드가 필요합니다.  
> 이 함수를 호출하면 `Cfg.Export` 속성에 지정한 `Down2Pdf.jsp`(또는 `Down2Pdf.aspx`)가 호출되며, 이 jsp 파일이 시트 정보(컬럼 정의 등)와 데이터를 받아 PDF 파일을 생성해 클라이언트로 전송합니다.  
> 시트마다 반복 설정이 번거로우면 [IBSheet.CommonOptions](/docs/static/common-options)로 공통 적용할 수 있습니다.  
> [MultiRecord](/docs/props/cfg/multi-record) 기능을 사용하는 시트에서는 제약이 있습니다.

### Syntax
```javascript
void down2Pdf( param );
```

### Parameters

|Name|Type|Required|Description|
|----------|-----|---|----|
|fileName|`string`|<span class='optional'>선택</span>|생성할 PDF 파일명. 파일 확장자는 반드시 `.pdf`여야 합니다.<br/>확장자를 생략할 경우 자동으로 `.pdf`를 붙여 다운로드 합니다. (`default: "ibsheet.pdf"`) |
|downCols|`string`|<span class='optional'>선택</span>|지정한 열만 다운로드 합니다.<br/>별도의 설정이 없을시 모든 열이 다운로드 됩니다.<br> 보여지는 열만 다운로드하고 싶을 경우 `"Visible"`로 설정하면 됩니다.<br>(ex: "Price\|AMT\|TOTAL" 식의 문자열)|
|dpi|`number`|<span class='optional'>선택</span>|축소/확대 비율로 값이 작을 수록 크게 출력됩니다.<br/>50~32840 사이 값으로 설정 가능합니다. (`defalut: 2000`)|
|fontTo|`string`|<span class='optional'>선택</span>|PDF에 사용할 한글 폰트를 설정.<br/>"Gothic", "Gulim" 중 선택 (`default: "Gulim"`)<br/><br/>**<mark>주의</mark> : `Gothic` 폰트는 서버모듈 제품에 포함되어 있지 않습니다.**|
|paper|`string`|<span class='optional'>선택</span>|용지의 방향을 설정합니다.<br/>가로: `landscape` 또는 세로: `portrait` (`default: "portrait"`)|
|title|`string`|<span class='optional'>선택</span>|PDF 파일에 출력할 제목 설정 (`default: ""`)<br/><br/>**<mark>주의</mark> : 해당 기능은 닷넷 서버모듈에서 지원하지 않습니다.** |
|titleStyle|`string`|<span class='optional'>선택</span>|PDF 파일에 출력할 제목에 적용할 css style (`default: ""`)|
|url|`string`|<span class='optional'>선택</span>|`down2Pdf`와 더불어 서버에서 처리해야 하는 내용이 있는 경우 로직을 처리할 URL을 넣어주면 `Down2Pdf.jsp` 페이지를 호출하기 전에 먼저 URL인자에서 설정한 페이지를 호출한다.<br/> 따라서 설정 페이지에서는 작업이 끝난 후, request를 `Down2Pdf.jsp` 페이지로 전달해야 한다. (`default: ""`)|
|extendParam|`string`|<span class='optional'>선택</span>|서버로 전달해야 하는 내용이 있는 경우 `GET` 방식의 QueryString으로 연결하여 설정 (`default: ""`)|
|extendParamMethod|`string`|<span class='optional'>선택</span>|extendParam을 전달하는 방식을 설정 (`default: "POST"`)|
|reqHeader|`object`|<span class='optional'>선택</span>|서버 전송 헤더에 사용자가 지정한 헤더 정보를 설정합니다.|
|useXhr|`boolean`|<span class='optional'>선택</span>| xhr 통신을 이용해 파일을 다운로드받습니다.<br>`0(false)`:xhr 통신 사용 안함 (`default`)<br>`1(true)`:xhr 통신 사용|
<!--!
|`[동작안됨 비공개]` wordWrap|`boolean`|<span class='optional'>선택</span>|(`default: 0`)|
!-->

### Return Value
***none***

### Example
```javascript
  var param = {
    fileName: "홍길동 교통비 내역.pdf",
    title: "홍길동 교통비 내역",
    titleStyle: "color:red; font-size:100px;"
  };

  sheet.down2Pdf(param);
```

### Read More
- [down2Excel method](./down-to-excel)
- [down2Hwpx method](./down-to-hwpx)
- [down2Text method](./down-to-text)
- [doPrint method](/docs/funcs/core/do-print)
- [CanPrint row](/docs/props/row/can-print)
- [CanPrint col](/docs/props/col/can-print)
- [MultiRecord cfg](/docs/props/cfg/multi-record)
- [onBeforeExport event](/docs/events/on-before-export)
- [onExportFinish event](/docs/events/on-export-finish)


### Since

|product|version|desc|
|---|---|---|
|excel|0.0.0|기능 추가|
|excel|0.0.8|`reqHeader` 기능 추가|

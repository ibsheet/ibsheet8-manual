# down2Excel ***(method)***

<!-- synonyms: 엑셀 다운로드, 엑셀 내려받기, down to excel, 서버 엑셀 다운, jsp 엑셀, POI 엑셀, xlsx 다운로드, DRM, 문서보안, DRM 적용 -->

> 시트의 내용을 엑셀 파일로 다운로드합니다.  
> 사용 전 [서버모듈 설치](/docs/appx/import-export)와 `/plugins/ibsheet-excel.js` 스크립트 로드가 필요합니다.  
> 이 함수를 호출하면 `Cfg.Export` 속성에 지정한 `Down2Excel.jsp`(또는 `Down2Excel.aspx`)가 호출되며, 이 jsp 파일이 시트 정보(컬럼 정의 등)와 데이터를 받아 엑셀 파일을 생성해 클라이언트로 전송합니다.  
> 시트마다 반복 설정이 번거로우면 [IBSheet.CommonOptions](/docs/static/common-options)로 공통 적용할 수 있습니다.

다운로드가 서버에서 실패하면 오류 메시지는 [onExportFinish](/docs/events/on-export-finish)의 `message`로 전달됩니다(`result`가 `0`일 때).

여러 개의 엑셀 파일을 한 번에 다운로드하려면, `down2Excel`을 그냥 연달아 호출하는 대신 [onExportFinish](/docs/events/on-export-finish) 이벤트에서 다음 파일을 호출해 **한 번에 하나씩** 받거나, 각 호출에 `useXhr: 1`을 지정합니다. (연달아 호출하면 마지막 호출의 파일만 다운로드됩니다.)

### Syntax
```javascript
void down2Excel( param );
```

### Parameters

|Name|Type|Required|Description|
|----------|-----|---|----|
|fileName|`string`|<span class='optional'>선택</span>|생성할 엑셀파일 명 (`default: "Excel.xlsx"`) <br/>**이 속성에서 파일명과 함께 확장자를 xls, xlsx로 붙이느냐에 따라서 생성 파일이 xls형식이나, xlsx형식으로 만들어집니다.**<br/>파일 이름에 쓸 수 없는 특수문자(`\ / : * ? " < > \|`)가 포함되면 다운로드한 파일을 열 때 복구 경고가 뜨거나 손상될 수 있으니 제거하세요.|
|sheetName|`string`|<span class='optional'>선택</span>|만들어지는 엑셀 파일의 WorkSheet에 부여할 이름<br/>워크시트 이름에 쓸 수 없는 특수문자(`\ / ? * [ ] :`)가 포함되면 다운로드한 파일을 열 때 복구 경고가 뜨거나 손상될 수 있으니 제거하세요.|
|downRows|`string`|<span class='optional'>선택</span>|지정한 행만 다운로드 합니다.<br/>(ex: "1\|3\|4\|5\|9" 식의 문자열)<br> 별도의 설정이 없을 시 모든 행이 다운로드 됩니다.<br/> 화면에 보이는 행 또는 필터된 행만 포함하고 싶은 경우 `"Visible"`로 설정하면 됩니다.<br/> `downRows`로 행을 일부만 다운로드하면 **데이터 영역의 머지가 정상 적용되지 않습니다**(헤더 머지는 유지). 행 일부만 받을 때는 머지를 기대하지 마세요.<br> 데이터 행만 설정할 수 있으며, 데이터 행의 시작 Index는 1부터 시작합니다.|
|downCols|`string`|<span class='optional'>선택</span>|지정한 열만 다운로드 합니다.<br/> 별도의 설정이 없을시 모든 열이 다운로드 됩니다.<br> 보여지는 열만 다운로드하고 싶을 경우 `"Visible"`로 설정하면 됩니다.<br/>(ex: "Price\|AMT\|TOTAL" 식의 문자열)<br/> 지정한 순서대로 컬럼이 재배열되므로, 머지가 있는 시트에서 컬럼 순서를 바꾸면 헤더 머지가 어긋날 수 있습니다(화면과 같은 순서 권장). 특정 컬럼을 제외하면 머지는 남은 컬럼에 맞춰 조정됩니다.|
|downTreeHide|`boolean`|<span class='optional'>선택</span>|tree를 사용하는 경우, 접혀진 행도 엑셀에 다운로드 할지 여부<br>`0(false)`:접혀진 행(자식노드)들 다운로드 대상 제외 (`default`)<br>`1(true)`:접혀진 행(자식노드)들 다운로드 대상 포함|
|downHeader|`boolean`|<span class='optional'>선택</span>|헤더행을 다운로드 할지 여부를 설정합니다.<br>`0(false)`:다운로드 시 헤더행 미포함<br>`1(true)`:다운로드 시 헤더행 포함 (`default`)|
|sheetDesign|`number`|<span class='optional'>선택</span>|시트에 적용된 디자인 요소를 엑셀에도 반영할지 여부를 설정합니다.<br>`main.css` 스타일뿐 아니라 `setAttribute`로 지정한 `Color`/`TextColor`도 반영됩니다.<br>반영되는 디자인 요소는 다음과 같습니다.<br/>헤더의 배경색(`main.css` 파일에 설정한 `IBCellHeader` class 속성값), 헤더의 폰트 색상(`main.css` 파일에 설정한 `IBHeaderText` class 속성값),<br/> 폰트명(`main.css` 파일에 설정한 `IBMain` class 속성값, excelFontFamily로 재지정 가능),<br/>폰트크기(`main.css` 파일에 설정한 `.IBMain, .IBMain *` 값, excelFontSize 속성으로 재지정 가능),데이터 배경색 <br> `0`:셀 외곽선을 제외한 모든 디자인을 적용하지 않습니다.<br/> `1`:셀 외곽선을 포함해 모든 디자인을 적용합니다. (`default`)<br>`2`:셀 외곽선을 제외한 셀 스타일을 적용합니다.<br/>`3`:셀 외곽선 및 스타일을 모두 적용하지 않습니다.<br/> `4`:헤더행에만 모든 디자인을 적용합니다. **해당 옵션을 사용하시려면 서버모듈을 1.1.16 이후 버전으로 업데이트해주셔야 합니다.**
|titleText|`string`|<span class='optional'>선택</span>|엑셀 문서의 상단에 원하는 문자를 추가합니다.<br/> 문자는 열구분자("\|")와 행구분자("\r\n")을 통해서 작성하실수 있습니다.<br/>가령 "A\|B\|C\r\nD\|E\|F" 와 같이 입력한 경우 첫 행에 3개의 셀에 각각 A,B,C 값이 들어가고 두번째 행의 3개의 셀에 각각 D,E,F 값이 입력됩니다. <br/> 값 안에서 엔터를 포함하려면 \r 이나 \n 을 삽입하면 됩니다. \r\n 이 10개가 포함되면 11줄을 차지하게 되고 12번째 행부터 시트 내용이 출력됩니다.|
|userMerge|`string`|<span class='optional'>선택</span>|`TitleText`와 더불어 사용하면서 엑셀 안에 원하는 영역을 머지(병합)합니다.<br/> 입력방법은 4개의 숫자로 <br/>`"머지시작셀 row index,머지시작셀 col index,아래로 병합할 행 개수(1을 설정하면 병합 없음),우측으로 병합할 개수"`<br/>로 이루어 집니다.(여러개 병합시에는 띄어쓰기로 구분)<br/>가령 `"2,2,1,6 3,2,3,3"`위와 같이 설정하였다면 2,2 셀부터 오른쪽으로 6칸이 병합되고, 3,2 셀부터 아래로 3칸, 오른쪽으로 3칸이 병합 됩니다.<br/>![userMerge](/assets/imgs/userMerge.png)|
|excelRowHeight|`number`|<span class='optional'>선택</span>|엑셀 문서의 행 높이를 설정합니다. -1 설정시 셀의 내용물 크기에 맞춰 엑셀 문서의 행 높이가 조절됩니다.|
|excelHeaderRowHeight|`number`|<span class='optional'>선택</span>|엑셀의 헤더행의 높이를 설정합니다.|
|wordWrap|`boolean`|<span class='optional'>선택</span>|엑셀 문서의 "텍스트 줄바꿈" 여부를 설정합니다.<br>`0(false)`:줄바꿈 미적용<br>`1(true)`:줄바꿈 적용 (`default`)|
|comboValidation|`boolean`|<span class='optional'>선택</span>|Enum 타입으로 만들어진 열에 대해 엑셀에서도 데이터 기능을 통해 드롭다운리스트 형태로 표현합니다.<br/>Enum의 종류가 많은 경우 무시됩니다.<br>`0(false)`:드롭다운리스트 형태 사용 안함 (`default`)<br>`1(true)`:드롭다운리스트 형태 사용|
|hiddenColumn|`boolean`|<span class='optional'>선택</span>|숨은 컬럼들을 엑셀로 다운로드 받은 경우, 해당 컬럼이 눈에 보이지는 않지만 엑셀 메뉴중 "숨기기 취소"를 선택한 경우 해당 컬럼이 다시 보일 수 있도록 엑셀 문서에 다운로드 받는다.<br> `hiddenColumn:1` 은 `downCols`와 **절대 같이 사용하시면 안됩니다.**<br>`0(false)`: 엑셀 다운로드 시 감춰진 열도 Visible:1 컬럼과 동일하게 일반 컬럼처럼 표현됨 (`default`)<br>`1(true)`:감춰진 열 다운로드 시 "열 숨기기" 형태로 엑셀 다운로드|
|merge|`number`|<span class='optional'>선택</span>|시트의 머지 상태를 엑셀에 그대로 반영할지를 설정합니다.<br/>`0`:사용 안 함 (`default`)<br/>`1`:사용함 (셀 병합 시, 부속 셀의 값을 원본으로 유지함)<br/>`2`:사용함 (셀 병합 시, 부속 셀의 값을 비움)|
|textToGeneral|`boolean`|<span class='optional'>선택</span>|Type:`Text`의 엑셀 서식 형식<br/>`0(false)`: Type:`Text`의 엑셀 서식을 텍스트 서식으로 지정 <br/>`1(true)`: Type:`Text`의 엑셀 서식을 일반 서식으로 지정(`default`)|
|allTypeToText|`boolean`|<span class='optional'>선택</span>|시트의 `Int`, `Float` 타입을 제외한 모든 컬럼의 엑셀 서식을 `Text` 타입으로 받고자 하는 경우 설정합니다.<br>`0(false)`:`Int`, `Float` 타입을 제외한 모든 컬럼의 엑셀 서식을 `Text` 타입으로 설정 안함 (`default`)<br>`1(true)`:`Int`, `Float` 타입을 제외한 모든 컬럼의 엑셀 서식을 `Text` 타입으로 설정|
|appendPrevSheet|`boolean`|<span class='optional'>선택</span>|[down2ExcelBuffer](./down-to-excel-buffer) 메소드를 사용하여 2개 이상의 시트를 엑셀로 다운로드 할 때 이전의 시트 내용을 마지막으로 작성한 워크시트에 시트 내용을 덧붙일지 여부를 설정합니다.<br/>`0(false)`: 워크시트를 새로 생성하여 작성합니다. (`default`)<br/>`1(true)`: 마지막으로 작성한 워크시트에 시트 내용을 덧붙입니다.|
|checkBoxOnValue|`string`|<span class='optional'>선택</span>|체크박스와 라디오 박스에서 체크를 한 경우 `1`값 대신 지정한 값을 사용합니다.|
|checkBoxOffValue|`string`|<span class='optional'>선택</span>|체크박스와 라디오 박스에서 체크 해제를 한 경우 `0`값 대신 지정한 값을 사용합니다.|
|downSum|`boolean`|<span class='optional'>선택</span>|합계 행 다운로드 여부를 설정합니다.<br>`0(false)`:합계 행 다운로드 시 미포함<br>`1(true)`:합계 행 다운로드 시 포함 (`default`)|
|excelFontSize|`number`|<span class='optional'>선택</span>|엑셀의 폰트 크기를 설정합니다.<br/>미지정 시 `main.css`의 `.IBMain, .IBMain *`에 설정된 폰트 크기가 기본 적용되며, 화면과 다른 크기로 내리려면 이 값을 지정합니다.|
|excelFontFamily|`string`|<span class='optional'>선택</span>|엑셀의 폰트(글꼴)를 설정합니다.<br/>미지정 시 `main.css`의 `.IBMain`에 설정된 폰트명이 기본 적용되며, 화면과 다른 글꼴로 내리려면 이 값을 지정합니다.|
|excludeFooterRow|`boolean`|<span class='optional'>선택</span>|푸터 행 제외 여부를 설정합니다.<br>`0(false)`:푸터 행 포함 (`default`) <br>`1(true)`:푸터 행 제외|
|numberTypeToText|`boolean`|<span class='optional'>선택</span>|`Int`, `Float` 타입의 컬럼을 `Text` 타입으로 다운로드 받을지 여부를 설정합니다.<br>`0(false)`:`Int`, `Float` 타입의 컬럼을 `Text` 타입으로 설정 안함 (`default`)<br>`1(true)`:`Int`, `Float` 타입의 컬럼을 `Text` 타입으로 설정|
|reqHeader|`object`|<span class='optional'>선택</span>|서버 전송 헤더에 사용자가 지정한 헤더 정보를 설정합니다.|
|extendParam|`string`|<span class='optional'>선택</span>|서버로 전달해야 하는 내용이 있는 경우 `GET` 방식의 `QueryString`으로 연결하여 서버로 같이 전달됩니다.<br/> (ex: `sheet.down2Excel({extendParam: "sido=서울시&sigungu=관악구"}`)|
|extendParamMethod|`string`|<span class='optional'>선택</span>|`extendParam`의 내용을 `GET` 또는 `POST`로 전달할지를 설정합니다. (`default: "GET"`)|
|requiredMark|`boolean`|<span class='optional'>선택</span>|필수 입력 항목 마크(`*`)를 다운로드 받을지 여부를 설정합니다.<br>`0(false)`:필수 입력 항목 마크(`*`) 다운로드 시 미포함<br>`1(true)`:필수 입력 항목 마크(`*`) 다운로드 시 포함 (`default`)|
|titleAlign|`string`|<span class='optional'>선택</span>|`titleText`로 설정한 내용에 대하여 `left`, `center`, `right` 중 정렬을 설정합니다. (`default: "center"`)|
|downCombo|`string`|<span class='optional'>선택</span>|`Enum` 타입의 선택 항목을 `Enum` 속성과 `EnumKeys` 속성 어떤 형태로 다운로드를 받을 지 설정합니다.<br/> `TEXT`: `Enum` 속성을 사용하여 다운로드 합니다. (`default`)<br/> `CODE`: `EnumKeys` 속성을 사용하여 다운로드합니다.|
|onlyHeaderMerge|`boolean`|<span class='optional'>선택</span>|시트의 데이터 영역의 머지를 강제로 제한하고 헤더 영역의 머지만을 엑셀에 반영 여부<br>`0(false)`:헤더 영역과 데이터 영역의 머지 사항을 다운로드 시 반영 (`default`)<br>`1(true)`:헤더 영역의 머지 사항만 다운로드 시 반영|
|numberExMode|`boolean`|<span class='optional'>선택</span>|시트의 `Int`, `Float` 타입의 컬럼을 숫자 서식으로 다운로드 받을 지 여부를 설정합니다. 설정하지 않을 시, 통화나 사용자 지정 서식으로 다운로드됩니다.<br>`0(false)`:다운로드 시, 시트의 `Int`, `Float` 타입의 컬럼을 통화나 사용자 지정 서식으로 받습니다 (`default`)<br>`1(true)`:다운로드 시, 시트의 `Int`, `Float` 타입의 컬럼을 숫자 서식으로 다운로드 받습니다|
|numberFormatMode|`number`|<span class='optional'>선택</span>|실수 형태의 데이터 타입에 대한 셀 서식 설정 방식을 설정합니다.<br/>`0`:시트의 컬럼 포맷을 따릅니다. (`default`)<br/>`1`:셀의 값 기준에 따라 정수 또는 실수 형태로 셀 서식을 설정합니다.<br/>`2`:일반 서식으로 설정합니다.|
|useXhr|`boolean`|<span class='optional'>선택</span>| xhr 통신을 이용해 엑셀 파일을 다운로드받습니다.<br/>`1(true)`로 설정하면 여러 번 연달아 호출해도 요청이 충돌하지 않아 각 파일이 모두 다운로드됩니다(기본 방식은 마지막 호출의 파일만 다운로드됨).<br>`0(false)`:xhr 통신 사용 안함 (`default`)<br>`1(true)`:xhr 통신 사용|
|exHead|`object`|<span class='optional'>선택</span>|시트 상단에 표시하고 싶은 내용을 설정합니다.<br>titleText, userMerge, header, footer 속성과 같이 사용할 수 없으며, 같이 사용시 titleText, userMerge, header, footer속성은 무시됩니다. <br> 해당 속성은 poi를 사용하는 경우에만 설정이 가능합니다.|
|exFoot|`object`|<span class='optional'>선택</span>|시트 하단에 표시하고 싶은 내용을 설정합니다.<br>titleText, userMerge, header, footer 속성과 같이 사용할 수 없으며, 같이 사용시 titleText, userMerge, header, footer속성은 무시됩니다. <br> 해당 속성은 poi를 사용하는 경우에만 설정이 가능합니다.|
|tempFile|`string`|<span class='optional'>선택</span>|템플릿으로 사용할 엑셀 파일명을 설정합니다. **반드시 `Down2Excel.jsp` 또는 `Down2Excel.aspx`에서 템플릿 경로를 설정해야합니다.**|
|sheetNo|`number`|<span class='optional'>선택</span>|`tempFile`인자로 지정한 엑셀 파일에서 템플릿으로 사용할 워크시트 번호를 설정합니다. (`default: 0`)|
|startCol|`number`|<span class='optional'>선택</span>|템플릿 적용 다운로드 시, 엑셀 파일 내 데이터를 쓰기 시작할 컬럼 번호를 설정합니다. (`default: 0`)|
|startRow|`number`|<span class='optional'>선택</span>|템플릿 적용 다운로드 시, 엑셀 파일 내 데이터를 쓰기 시작할 행 번호를 설정합니다. (`default: 0`)|
|freezePane|`number`|<span class='optional'>선택</span>|상단 행과 왼쪽 열을 틀 고정하여 다운로드하는 옵션입니다. 옵션 설정에 따라 다르게 틀 고정이 적용되어 다운로드되며, 비트 연산으로 동작합니다. <br/> <br/> `0`: 틀 고정을 적용하지 않음(`default`) <br/> `1`: 헤더 틀 고정 적용 (`2`과 함께 적용시 헤드 영역 틀 고정으로 동작) <br/> `2`: 헤드 영역 틀 고정 적용 <br/> `4`: 왼쪽 고정 열 틀 고정 적용|
|workbookPassword|`string`|<span class='optional'>선택</span>| 다운받을 엑셀 파일에 비밀번호를 설정하려는 경우 사용하는 옵션입니다.<br/>xlsx 확장자 파일에서만 지원됩니다.|
|enableFilter|`boolean`|<span class='optional'>선택</span>| 시트를 엑셀로 다운로드할 때, 시트영역에 엑셀 필터 기능을 활성화하여 다운로드합니다. <br>  **이 옵션은 현재 시트에 필터가 적용되어 있는지 여부와는 무관합니다. 더불어 이 옵션은 필터링된 결과를 다운로드하는 기능이 아니며, 단지 엑셀 필터 기능을 바로 사용할 수 있도록 시트 영역에 필터를 설정하는데 그칩니다.**|
<!--!
|`[점검]` excludeSubSum|`boolean`|<span class='optional'>선택</span>|소계/누계 행 제외 여부를 설정합니다.<br/> `0(false)`: 소계/누계 모두 제외하지 않습니다. (`default`)<br/> `1(true)`: 소계/누계 모두 제외합니다.|
|`[비공개]` autoSizeColumn|`boolean`|<span class='optional'>선택</span>|엑셀의 컬럼 너비를 자동으로 조절할 지 여부를 설정합니다.(단, 자동 조절 결과가 정확하지 않을 수 있습니다.) (`default: 0(false)`)|
|`[비공개]` printSetup|`object`|<span class='optional'>선택</span>|엑셀을 다운로드할 때, 프린트에 관한 설정(용지 크기, 용지 방향 등)을 설정합니다.|
|`[비공개]` reportXMLURL|`boolean`|<span class='optional'>선택</span>|엑셀에 타이틀이나 패턴 등을 별도의 xml파일을 통해 설정합니다.|
|`[비공개]` treeLevel|`boolean`|<span class='optional'>선택</span>|트리 구조의 데이터를 다운 받을 때, 트리 레벨을 엑셀에 별도의 컬럼으로 표시할 지 여부를 설정합니다. (`default: 0(false))`|
|`[비공개]` URL|`string`|<span class='optional'>선택</span>|`down2Excel`과 더불어 서버에서 처리해야하는 내용이 있는 경우, 로직을 처리할 URL을 설정합니다.|

!-->

### downCols, downRows 사용 시 merge 적용 정리

`merge` 옵션을 켜도 행이나 열을 일부만 다운로드하면 머지가 그대로 적용되지 않을 수 있습니다.

- **`downRows`로 행을 일부만 받으면** 데이터 영역의 머지가 적용되지 않습니다. (헤더 머지는 유지)
- **`downCols`로 열을 받을 때**는 화면에 보이는 컬럼 순서 그대로 지정해야 머지가 유지됩니다. 머지된 컬럼을 빼거나 순서를 바꾸면 머지가 정상 적용되지 않으므로, `Visible:0`인 컬럼까지 포함해 화면과 같은 순서로 지정하세요.

![downCols사용시 머지](/assets/imgs/downcols_merge.png "downCols사용시 머지")

예를 들어 "머지 컬럼"을 머지된 채로 다운로드받으려면 `downCols: "컬럼1|컬럼2|컬럼3|컬럼4"`처럼 지정합니다. `"컬럼2|컬럼3|컬럼4"`(특정 컬럼 제외)나 `"컬럼4|컬럼1|컬럼3|컬럼2"`(순서 변경)는 머지가 온전히 적용되지 않습니다.

### exHead,exFoot options
|Name|Type|Required|Description|
|----------|-----|---|----|
|Height|`number`|<span class='optional'>선택</span>|행의 높이|
|Cells|`array[object]`|<span class='optional'>선택</span>|행의 각셀에 표시될 내용,속성 설정|
|Cells[{Value}]|`string`|<span class='optional'>선택</span>|셀에 표시될 내용|
|Cells[{Color}]|`string`|<span class='optional'>선택</span>|셀의 배경색 (ex `#FFDDEE`)|
|Cells[{TextColor}]|`string`|<span class='optional'>선택</span>|셀의 글자색 (ex `#446622`)|
|Cells[{TextSize}]|`number`|<span class='optional'>선택</span>|셀의 글자 크기|
|Cells[{TextStyle}]|`number`|<span class='optional'>선택</span>|셀의 글자 style <br> 8, 16, 32는 설정이 불가합니다. ([참고](/docs/props/cell/text-style))|
|Cells[{Wrap}]|`boolean`|<span class='optional'>선택</span>|자동 줄바꿈 여부<br>`0(false)`:자동 줄바꿈 적용 안함<br>`1(true)`:자동 줄바꿈 적용 (`default`)|
|Cells[{Type}]|`string`|<span class='optional'>선택</span>|셀타입(Image를 사용해야 하는 경우에만 Img로 설정)|
|Cells[{ColSpan}]|`number`|<span class='optional'>선택</span>|가로 병합 셀 개수(`default: 1`) (주의: 가로 병합 옵션은 시트에 걸쳐서 사용할 수는 없습니다.)|
|Cells[{RowSpan}]|`number`|<span class='optional'>선택</span>|세로 병합 셀 개수(`default: 1`) (주의: 세로 병합 옵션은 시트에 걸쳐서 사용할 수는 없습니다.)|
|Cells[{BorderTop}]|`string`|<span class='optional'>선택</span>|`상단 보더` 굵기,스타일,색상을 구분자 " "로 연결한 문자열  (ex: "1 solid #FF0000")|
|Cells[{BorderBottom}]|`string`|<span class='optional'>선택</span>|`하단 보더` 굵기,스타일,색상을 구분자 " "로 연결한 문자열  (ex: "1 solid #FF0000")|
|Cells[{BorderLeft}]|`string`|<span class='optional'>선택</span>|`좌측 보더` 굵기,스타일,색상을 구분자 " "로 연결한 문자열  (ex: "1 solid #FF0000")|
|Cells[{BorderRight}]|`string`|<span class='optional'>선택</span>|`우측 보더` 굵기,스타일,색상을 구분자 " "로 연결한 문자열  (ex: "1 solid #FF0000")|
 
#### Cells 내에 Border 속성 설정시 주의 사항

1. 굵기는 px단위가 아니며, 1은 가늘게 2는 굵게 표시하도록 설정합니다. <br>
   스타일은 `solid`,`dashed`,`dotted` 세 가지 스타일을 제공합니다. <br>
   색상은 hex code로 설정합니다. (ex `#FF00FF`)
2. 좌우로 붙어있는 셀에 각각 우측보더와 좌측보더를 다르게 설정했을 때는 우측셀에 설정한 좌측 보더값이 적용됩니다.<br>
   상하로 붙어있는 셀에 각각 하단보더와 상단보더를 다르게 설정했을 때는 하단셀에 설정하 상단 보더값이 적용됩니다.
3. RowSpan,ColSpan속성으로 통해 병합된 셀이라도 각 셀별로 보더 설정이 필요합니다.

<br><br>

### 템플릿을 적용하여 엑셀 파일 다운로드하기

`tempFile` 옵션은 미리 서버에 템플릿을 준비해둔 뒤, 해당 템플릿에 시트 데이터만 삽입해 엑셀 파일을 다운로드하고 싶으실 때 사용하는 옵션입니다.  <br>

템플릿 기능을 사용하시려면 `Down2Excel.jsp`또는 `Down2Excel.aspx`에 미리 `TempRoot` 설정을 이용해 템플릿 파일 폴더 위치를 지정해주셔야 됩니다. <br>

`startRow`, `startCol` 옵션으로 템플릿 파일에서 데이터를 작성하기 시작할 위치를 지정하실 수 있으며, `sheetNo` 옵션으로 템플릿 파일에서 데이터를 작성할 워크시트를 지정하실 수 있습니다. <br>

더불어 `tempFile` 옵션을 이용해 엑셀 파일을 다운로드받는 경우, 디자인은 온전히 템플릿 파일에 설정된 디자인을 따라가게 되며 `excelFontSize`, `excelRowHeight`, `sheetDesign` 등 옵션은 무시됩니다. <br>

```js

// 5번째 행, 3번째 컬럼부터 데이터 작성 시작
sheet.down2Excel({
      fileName: "sheet.xlsx",
      tempFile: "template.xlsx",
      startRow: 4,
      startCol: 2,
})
```

```java
// 서버 사이드 설정
// 템플릿 파일이 위치한 폴더 경로 설정
down.setTempRoot("D:/");
```

[템플릿 파일 예시]

<img src="../../../assets/imgs/down2ExcelTempFile1.png" width="700" height="400"/>

[템플릿 파일을 활용해 다운로드받은 파일 결과물]

<img src="../../../assets/imgs/down2ExcelTempFile2.png" width="700" height="400"/>
 <br/>

### Return Value
***none***

### Example
```javascript
var param = {
  fileName:"홍길동 교통비 내역.xlsx",
  titleText:"||2019년 3월 교통비\r\n|||||||홍길동",
  userMerge:"0,2,1,4"
};
sheet.down2Excel(param);
```

```javascript
//exHead 사용 예제
var param = {
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


        sheet.down2Excel(param);

```
![exHead,exFoot](/assets/imgs/exportDataExHeadExFoot.png "exHead,exFoot")

### Read More
- [Down2ExcelConfig cfg](/docs/props/cfg/down-to-excel-config)
- [AutoExcelMode cfg](/docs/props/cfg/auto-excel-mode)
- [exportData method](/docs/funcs/core/export-data)
- [down2ExcelBuffer method](./down-to-excel-buffer)
- [loadExcel method](./load-excel)
- [down2Text method](./down-to-text)
- [down2Pdf method](./down-to-pdf)
- [onBeforeExport event](/docs/events/on-before-export)
- [onExportFinish event](/docs/events/on-export-finish)
- [엑셀 업로드/다운로드 설정 appendix](/docs/appx/import-export)
- [엑셀 서버 모듈 트러블슈팅 appendix](/docs/appx/excel-server-troubleshooting)
- [엑셀 DRM 처리 appendix](/docs/appx/excel-drm)
- [엑셀 비밀번호 설정 appendix](/docs/appx/excel-password)
- [한 시트를 그룹별로 나눠 여러 파일/워크시트로 다운로드 appendix](/docs/appx/excel-split-download)


### Since

|product|version|desc|
|---|---|---|
|excel|0.0.0|기능 추가|
|excel|0.0.8|`reqHeader` 기능 추가|
|excel|1.0.19|`sheetDesign: 4` 옵션 추가|
|excel|1.0.18|`requiredMark` 기능 수정: 소문자로 사용 가능|
|excel, servermodule|1.1.0, 1.1.24|`exHead`, `exFoot` 기능 추가|
|excel, servermodule|1.1.15, 1.1.37|`freezePane` 기능 추가|
|excel, servermodule|1.1.32(excel), 2.0.15(servermodule) |`enableFilter` 기능 추가|

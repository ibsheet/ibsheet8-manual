# exportData ***(method)***

<!-- synonyms: 엑셀 다운로드, 엑셀 내려받기, 클라이언트 엑셀, jszip 엑셀, xlsx 다운로드, txt csv 다운로드, export data, CSV 인젝션, 수식 인젝션, formula injection, csv injection, escapeCsvInjection -->

> 시트의 내용을 엑셀 파일로 다운로드합니다.  
> 해당 기능은 브라우저에서 처리되는 클라이언트 기능이며, 엑셀 파일 생성을 위해 `jszip` 라이브러리를 사용합니다.  
> `/plugins/jszip.min.js` 파일이 반드시 존재해야 하며, 해당 파일이 없으면 엑셀 다운로드 기능은 동작하지 않습니다.  
> 지원하는 파일 형식은 **xlsx, txt, csv** 입니다. (구버전 `xls` 형식은 지원하지 않습니다.)  
> 엑셀 다운로드/업로드 구현, 옵션, 트러블슈팅 상세는 IBSheet 지원 포털의 [엑셀 가이드 모음](https://portal.ibsheet.com/support/solutions/folders/72000394868)에서 확인하세요.

### Syntax
```javascript
void exportData( param );
```

### Parameters

|Name|Type|Required|Description|
|----------|-----|---|----|
|fileName|`string`|<span class='optional'>선택</span>|생성할 엑셀파일 명 (`default: Excel.xlsx`)<br/>확장자를 입력하지 않으면 임의의 파일명으로(xlsx) 다운로드 합니다.<br/>확장자를 `xlsx`, `txt`, `csv`로 지정하면 해당 형식으로 다운로드 됩니다.|
|sheetName|`string`|<span class='optional'>선택</span>|만들어지는 엑셀 파일의 WorkSheet에 부여할 이름 `(xlsx에서만 지원)`|
|downRows|`string`|<span class='optional'>선택</span>|지정한 행만 다운로드 합니다.<br/>(ex: "1\|3\|4\|5\|9" 식의 문자열)<br> 별도의 설정이 없을 시 모든 행이 다운로드 됩니다.<br/>화면에 보이는 행 또는 필터된 행만 포함하고 싶은 경우 `"Visible"`로 설정하면 됩니다.<br/> `downRows`를 설정하면 **데이터 영역의 머지가 적용되지 않습니다**(헤더 머지는 유지).<br> 데이터 행만 설정할 수 있으며, 데이터 행의 시작 Index는 1부터 시작합니다.|
|downCols|`string`|<span class='optional'>선택</span>|지정한 열만 다운로드 합니다.<br/> 별도의 설정이 없을시 모든 열이 다운로드 됩니다.<br> 보여지는 열만 다운로드하고 싶을 경우 `"Visible"`로 설정하면 됩니다.<br/>(ex: "Price\|AMT\|TOTAL" 식의 문자열)<br/> 지정한 순서는 무시되고 시트의 원래 컬럼 순서로 출력됩니다.|
|downTreeHide|`boolean`|<span class='optional'>선택</span>|tree를 사용하는 경우, 접혀진 행도 엑셀에 다운로드 할지 여부를 설정합니다.<br>`1(true)`로 설정시 접혀있는 자식노드도 모두 다운로드 됩니다.(`default: 0(false)`)|
|downHeader|`boolean`|<span class='optional'>선택</span>|헤더행을 다운로드 할지 여부를 설정합니다.(`default: 1(true)`)|
|sheetDesign|`number`|<span class='optional'>선택</span>|시트의 디자인 요소를 엑셀에도 반영할지 여부를 설정합니다. <br> 반영되는 디자인 요소는 다음과 같습니다: 헤더의 배경색,폰트명,폰트크기,데이터 배경색 <br> `0`: 셀 외곽선을 제외한 모든 디자인을 적용하지 않습니다.<br/> `1`: 셀 외곽선을 포함해 모든 디자인을 적용합니다. (default) <br/> `2`: 셀 외곽선을 제외한 셀 스타일을 적용합니다. <br/> `3`: 셀 외곽선 및 스타일을 모두 적용하지 않습니다.`(xlsx에서만 지원)` <br/>  `4`: 헤더행에만 모든 디자인을 적용합니다. 
|titleText|`string`|<span class='optional'>선택</span>|엑셀 문서의 상단에 원하는 문자를 추가합니다.<br/> 문자는 열구분자("\|")와 행구분자(`"\r\n"`)을 통해서 작성하실수 있습니다.<br/>가령 "A\|B\|C\r\nD\|E\|F" 와 같이 입력한 경우 첫 행에 3개의 셀에 각각 A, B, C 값이 들어가고,<br/>두번째 행의 3개의 셀에 각각 D, E, F 값이 입력됩니다.<br/>값 안에서 엔터를 포함하려면 `"\r"` 이나 `"\n"` 을 삽입하면 됩니다.<br/> `"\r\n"` 이 10개가 포함되면 11줄을 차지하게 되고 12번째 행부터 시트 내용이 출력됩니다. `(xlsx에서만 지원)`|
|userMerge|`string`|<span class='optional'>선택</span>|`titleText`와 같이 사용하며, titleText를 원하는 모양으로 머지합니다.<br/> 입력방법은 4개의 숫자로 `"머지시작셀 row index, 머지시작셀 col index, 아래로 병합할 행 개수(1을 설정하면 병합 없음), 우측으로 병합할 개수"` 로 이루어 집니다. <br/>(여러개 병합시에는 띄어쓰기로 구분)<br/>가령 `"2,2,1,6 3,2,3,3"`위와 같이 설정하였다면,<br/>2,2 셀부터 오른쪽으로 6칸이 병합되고,<br/>3,2 셀부터 아래로 3칸, 오른쪽으로 3칸이 병합 됩니다. `(xlsx에서만 지원)`<br/>![userMerge](/assets/imgs/userMerge.png)|
|excelRowHeight|`number`|<span class='optional'>선택</span>|엑셀 문서의 행 높이를 설정합니다.<br/>-1 설정시 셀의 내용물 크기에 맞춰 엑셀 문서의 행 높이가 조절됩니다. `(xlsx에서만 지원)`|
|excelHeaderRowHeight|`number`|<span class='optional'>선택</span>|엑셀의 헤더행의 높이를 설정합니다.<br/>`(xlsx에서만 지원)`|
|wordWrap|`boolean`|<span class='optional'>선택</span>|엑셀 문서의 "텍스트 줄바꿈" 여부를 설정합니다.<br/>(`default: 1(true)`) `(xlsx에서만 지원)`|
|comboValidation|`boolean`|<span class='optional'>선택</span>|Enum 타입으로 만들어진 열에 대해 엑셀에서도 데이터 기능을 통해 드롭다운리스트 형태로 표현합니다.<br/>`(xlsx에서만 지원)`|
|rowDelim|`string`|<span class='optional'>선택</span>|text파일을 만들때 행 구분자(기본은 줄넘김 문자 `"\r\n"`)<br/>`(txt, csv)에서만 지원`
|colDelim|`string`|<span class='optional'>선택</span>|txt 다운로드 일 경우(`default: \t(탭문자)`<br/>csv 다운로드 일 경우(`default: ,(콤마))` <br/>업로드되는 파일에 따라 기본 구분자가 변경됩니다.<br/>`(txt, csv)에서만 지원`
|hiddenColumn|`boolean`|<span class='optional'>선택</span>|숨은 컬럼들을 엑셀로 다운로드 받은 경우,<br/>해당 컬럼이 눈에 보이지는 않지만 엑셀 메뉴중 "숨기기 취소"를 선택한 경우 해당 컬럼이 다시 보일 수 있도록 엑셀 문서에 다운로드 받는다.<br/>`hiddenColumn:1` 은 `downCols`와 **절대 같이 사용하시면 안됩니다.**<br>`0(false)`: 엑셀 다운로드 시 감춰진 열도 Visible:1 컬럼과 동일하게 일반 컬럼처럼 표현됨 (`default`)<br/>`1(true)`:감춰진 열 다운로드 시 "열 숨기기" 형태로 엑셀 다운로드|
|merge|`number`|<span class='optional'>선택</span>|시트의 머지 상태를 엑셀에 그대로 반영할지를 설정합니다.<br/> `0`: 사용 안 함 (`default`)<br/> `1`: 사용함 (셀 병합 시, 부속 셀의 값을 원본으로 유지함)<br/> `2`: 사용함 (셀 병합 시, 부속 셀의 값을 비움) `(xlsx에서만 지원)`|
|textToGeneral|`boolean`|<span class='optional'>선택</span>|Type:`Text`의 엑셀 서식 형식<br/>`0(false)`: Type:`Text`의 엑셀 서식을 텍스트 서식으로 지정 <br/>`1(true)`: Type:`Text`의 엑셀 서식을 일반 서식으로 지정(`default`)|
|allTypeToText|`boolean`|<span class='optional'>선택</span>|시트의 `Int`, `Float` 타입을 제외한 모든 컬럼의 엑셀 서식을 `Text` 타입으로 받고자 하는 경우 설정합니다.<br/>(`default: 0(false)`) `(xlsx에서만 지원)`|
|checkBoxOnValue|`string`|<span class='optional'>선택</span>|체크박스와 라디오 박스에서 체크를 한 경우 `1`값 대신 지정한 값을 사용합니다.<br/>`(xlsx에서만 지원)`|
|checkBoxOffValue|`string`|<span class='optional'>선택</span>|체크박스와 라디오 박스에서 체크 해제를 한 경우 `0`값 대신 지정한 값을 사용합니다.<br/>`(xlsx에서만 지원)`|
|downSum|`boolean`|<span class='optional'>선택</span>|합계 행 다운로드 여부를 설정합니다.(`default: 1(true)`)|
|excelFontSize|`number`|<span class='optional'>선택</span>|엑셀의 폰트 크기를 설정합니다. `(xlsx에서만 지원)`|
|excludeFooterRow|`boolean`|<span class='optional'>선택</span>|푸터 행 제외 여부를 설정합니다.(`default: 0(false)`) `(xlsx에서만 지원)`|
|numberTypeToText|`boolean`|<span class='optional'>선택</span>|`Int`, `Float` 타입의 컬럼을 `Text` 타입으로 다운로드 받을지 여부를 설정합니다.<br/>(`default: 0(false)`) `(xlsx에서만 지원)`|
|excelFontFamily|`string`|<span class='optional'>선택</span>|엑셀의 폰트를 설정합니다.<br/>`(xlsx에서만 지원)`|
|exHead|`array[object]`|<span class='optional'>선택</span>|시트 상단에 표시하고 싶은 내용을 설정합니다.<br>**titleText 속성과 같이 사용할 수 없으며, 같이 사용시 titleText속성은 무시됩니다.**`(xlsx에서만 지원)`<br/>ex) 첫번째 행의 높이를 30, 첫번째 셀 텍스트를 지정<br/>exHead:[{Height:30, Cells:[{Value:"부서"}]}]|
|exFoot|`array[object]`|<span class='optional'>선택</span>|시트 하단에 표시하고 싶은 내용을 설정합니다.`(xlsx에서만 지원)`<br/>ex) 시트 하단의 첫번째 행 높이를 30, 첫번째 셀 텍스트를 지정<br/>exFoot:[{Height:30, Cells:[{Value:"출력: 2023-06-23 홍길동"}]}]|
|appendPrevSheet|`boolean`|<span class='optional'>선택</span>|[exportDataBuffer](./export-data-buffer) 메소드를 사용하여 2개 이상의 시트를 엑셀로 다운로드 할 때 마지막으로 작성한 워크시트에 해당 옵션이 적용된 시트를 덧붙일지 여부를 설정합니다. <br/> `0(false)`: 워크시트를 새로 생성하여 작성합니다.(`default`) <br/> `1(true)`: 마지막으로 작성한 워크시트에 시트를 덧붙입니다. `(xlsx에서만 지원)`|
|onlyHeaderMerge|`boolean`|<span class='optional'>선택</span>|`1(true)`로 설정 시, 시트의 데이터 영역의 머지를 강제로 제한하고 헤더 영역의 머지만을 엑셀에 반영합니다.(`default: 0(false)`)|
|freezePane|`number`|<span class='optional'>선택</span>|상단 행과 왼쪽 열을 틀 고정하여 다운로드하는 옵션입니다. 옵션 설정에 따라 다르게 틀 고정이 적용되어 다운로드되며, 비트 연산으로 동작합니다. <br/> <br/> `0`: 틀 고정을 적용하지 않음(`default`) <br/> `1`: 헤더 틀 고정 적용 (`2`과 함께 적용시 헤드 영역 틀 고정으로 동작) <br/> `2`: 헤드 영역 틀 고정 적용 <br/> `4`: 왼쪽 고정 열 틀 고정 적용|
|numberFormatMode|`number`|<span class='optional'>선택</span>|실수 형태의 데이터 타입에 대한 셀 서식 설정 방식을 설정합니다.<br/>`0`:시트의 컬럼 포맷을 따릅니다. (`default`)<br/>`1`:셀의 값 기준에 따라 정수 또는 실수 형태로 셀 서식을 설정합니다.<br/>`2`:일반 서식으로 설정합니다.|
|excelPage|`object`|<span class='optional'>선택</span>|엑셀 용지에 대한 동작을 설정합니다 `(xlsx에서만 지원)`<br/>ex)엑셀 용지설정(가로방향)<br/>excelPage: { orientation: "landscape" }|
|widthRate|`number`|<span class='optional'>선택</span>|엑셀 다운로드 시 열 너비에 곱해질 배율을 설정합니다.<br/>`0`보다 큰 양수 값을 사용합니다. (예: `0.5` → 기본 크기의 절반, `0.8` → 80%, `1.3` → 130%)<br/>지정하지 않거나 `0` 이하 값을 지정하면 `1`(기본 다운로드 크기)로 적용됩니다.<br/>(`default: 1`) `(xlsx에서만 지원)`|
|escapeCsvInjection|`boolean`|<span class='optional'>선택</span>|CSV 다운로드 시 CSV 인젝션(수식 인젝션) 방어를 활성화합니다. `csv` 형식에서만 동작하며, 그 외 형식(`xlsx`, `txt`)에서는 값과 무관하게 무시됩니다.<br/>`1(true)`로 설정하면 위험 선두 문자로 시작하는 문자열 셀 값 앞에 작은따옴표(`'`)를 붙여 스프레드시트가 값을 수식이 아닌 텍스트로 인식하도록 강제합니다.<br/>방어 대상 선두 문자: `=`, `+`, `-`, `@`, 탭(`\t`), CR(`\r`), LF(`\n`), `\|`, `%`<br/>`0(false)`:방어 미적용, 셀 값을 원본 그대로 CSV에 기록 (`default`)<br/>`1(true)`:위험 선두 문자로 시작하는 값에 `'` prefix 부여<br/>사용자 입력이 그대로 CSV로 내려가고, 그 파일을 제3자가 열 가능성이 있는 화면에서 켜는 것을 권장합니다. `(csv에서만 지원)`|

<!--!
|`[비공개]` directExcelData|`object`|<span class='optional'>선택</span>|시트의 데이터가 아닌 별도의 데이터를 이용하여 엑셀을 다운로드 하는 기능 (xlsx에서만 지원)|
|`[비공개]` downCombo|`string`|<span class='optional'>선택</span>|`Enum` 타입의 선택 항목을 `Enum` 속성과 `EnumKeys` 속성 어떤 형태로 다운로드를 받을 지 설정합니다.<br/> `TEXT`: `Enum` 속성을 사용하여 다운로드 합니다. (`default`)<br/> `CODE`: `EnumKeys` 속성을 사용하여 다운로드합니다.|
|`[비공개]` requiredMark|`string`|<span class='optional'>선택</span>|필수 입력 항목 마크(`*`)를 다운로드 받을지 여부를 설정합니다.(`default: 1(true)`)|
!-->

### downCols, downRows 사용 시 merge 적용 정리

`merge` 옵션을 켜도 행이나 열을 일부만 다운로드하면 머지가 그대로 적용되지 않을 수 있습니다.

- **`downRows`로 행을 일부만 받으면** 데이터 영역의 머지가 적용되지 않습니다. (헤더 머지는 유지)
- **`downCols`로 열을 받을 때**는 머지된 컬럼을 모두 포함해야 그 머지가 유지됩니다. 지정한 순서는 무시되고 시트의 원래 컬럼 순서로 출력되므로, 순서 때문에 머지가 깨지지는 않습니다.

![downCols사용시 머지](/assets/imgs/downcols_merge.png "downCols사용시 머지")

예를 들어 위 "머지 컬럼"을 머지된 채로 다운로드받으려면 `downCols: "컬럼1|컬럼2|컬럼3|컬럼4"`처럼 머지된 컬럼을 모두 포함합니다.

### excelPage Options

|Name|Type|Required|Description|
|----------|-----|---|----|
|paperSize|`string`|<span class='optional'>선택</span>|용지 크기를 설정합니다. 설정하지 않을 경우 기본 `A4`로 다운로드 됩니다. (`default: "A4"`)|
|orientation|`string`|<span class='optional'>선택</span>|용지 방향을 설정합니다.<br/>세로: "portrait", 가로: "landscape" (`default: "portrait"`)|
|marginLeft|`number`|<span class='optional'>선택</span>|용지 왼쪽의 여백을 설정합니다. (`default: 1.8`)|
|marginRight|`number`|<span class='optional'>선택</span>|용지 오른쪽의 여백을 설정합니다. (`default: 1.8`)|
|marginTop|`number`|<span class='optional'>선택</span>|용지 위쪽의 여백을 설정합니다. (`default: 1.9`)|
|marginBottom|`number`|<span class='optional'>선택</span>|용지 아래쪽의 여백을 설정합니다. (`default: 1.9`)|
|marginHeader|`number`|<span class='optional'>선택</span>|용지 머리글의 여백을 설정합니다. (`default: 0.8`)|
|marginFooter|`number`|<span class='optional'>선택</span>|용지 바닥글의 여백을 설정합니다. (`default: 0.8`)|
|fitToWidth|`number`|<span class='optional'>선택</span>|페이지 레이아웃의 너비를 설정합니다. (`default: 0`)|
|fitToHeight|`number`|<span class='optional'>선택</span>|페이지 레이아웃의 높이를 설정합니다. (`default: 0`)|

### exHead,exFoot options
|Name|Type|Required|Description|
|----------|-----|---|----|
|Height|`number`|<span class='optional'>선택</span>|행의 높이|
|Cells|`array[object]`|<span class='optional'>선택</span>|행의 각셀에 표시될 내용,속성 설정|
|Cells[{Value}]|`string`|<span class='optional'>선택</span>|셀에 표시될 내용|
|Cells[{Color}]|`string`|<span class='optional'>선택</span>|셀의 배경색 (ex `#FFDDEE`)|
|Cells[{TextColor}]|`string`|<span class='optional'>선택</span>|셀의 글자색 (ex `#446622`)|
|Cells[{TextSize}]|`number`|<span class='optional'>선택</span>|셀의 글자 크기|
|Cells[{TextStyle}]|`number`|<span class='optional'>선택</span>|셀의 글자 style ([참고](/docs/props/cell/text-style))|
|Cells[{TextFont}]|`string`|<span class='optional'>선택</span>|셀의 글자 family ([참고](/docs/props/cell/text-font))|
|Cells[{Wrap}]|`boolean`|<span class='optional'>선택</span>|자동 줄바꿈 여부(default: true)|
|Cells[{Type}]|`string`|<span class='optional'>선택</span>|셀타입(Image를 사용해야 하는 경우에만 Img로 설정)|
|Cells[{ColSpan}]|`number`|<span class='optional'>선택</span>|가로 병합 셀 개수(default: 1)|
|Cells[{RowSpan}]|`number`|<span class='optional'>선택</span>|세로 병합 셀 개수(default: 1)|
|Cells[{BorderTop}]|`string`|<span class='optional'>선택</span>|`상단 보더` 굵기,스타일,색상을 구분자 " "로 연결한 문자열<br/>(ex: "1 solid #FF0000")|
|Cells[{BorderBottom}]|`string`|<span class='optional'>선택</span>|`하단 보더` 굵기,스타일,색상을 구분자 " "로 연결한 문자열<br/>(ex: "1 solid #FF0000")|
|Cells[{BorderLeft}]|`string`|<span class='optional'>선택</span>|`좌측 보더` 굵기,스타일,색상을 구분자 " "로 연결한 문자열<br/>(ex: "1 solid #FF0000")|
|Cells[{BorderRight}]|`string`|<span class='optional'>선택</span>|`우측 보더` 굵기,스타일,색상을 구분자 " "로 연결한 문자열<br/>(ex: "1 solid #FF0000")|

#### Cells 내에 Border 속성 설정시 주의 사항

1. 굵기는 px단위가 아닌 1은 가늘게 2는 굵게 표시<br>
   스타일은 `solid`,`dashed`,`dotted` 제공 <br>
   색상은 hex code로 설정 (ex `#FF00FF`)
2. 좌우로 붙어있는 셀에 각각 우측보더와 좌측보더를 다르게 설정시 우측셀에 설정한 좌측 보더값이 적용됨<br>
   상하로 붙어있는 셀에 각각 하단보더와 상단보더를 다르게 설정시 하단셀에 설정하 상단 보더값이 적용됨
3. RowSpan,ColSpan속성으로 통해 병합 된 셀이라도 각 셀별로 보더 설정이 필요함


### Return Value
***none***

### Example
```javascript
// xlsx 확장자로 다운로드, 보여지는 행만 다운로드.
sheet.exportData({fileName: "재고리스트.xlsx",downRows: "Visible"});

// txt 확장자로 다운로드, 열 구분자 ',' 로 변경.
var param = {fileName: "exportTEXT.txt", colDelim: ","};
sheet.exportData(param);

// csv 확장자로 다운로드, 합계행 다운받지 않음.
var param = {fileName: "exportCSV.csv", downSum: 0}
sheet.exportData(param);

// csv 다운로드 + CSV 인젝션 방어.
// 셀 값이 `=1+1`, `+82-10-...`, `@SUM(...)`처럼 위험 선두 문자로 시작하면
// 파일에 `'`가 prefix되어 저장되고, 엑셀에서 텍스트로 표시됩니다.
sheet.exportData({fileName: "safe.csv", escapeCsvInjection: 1});
```

<!--!
### [`비공개`] Example
```js
// 임의의 데이터
var tmpData = [
  {
    SEQ: 1,
    TextData: '박만우',
    ComboData: '02',
    ISO: 'AWG',
    Currency: '아루바 플로린',
    IntData: 1120,
    FloatData: 115.25,
    DateData: '20100922',
    PhoneNo: '0425741245',
    LinesData: '서해상에 위치한 고기압의 영향을 받겠습니다.',
    Userformat: '',
    ImageData: '|../assets/imgs/fe.jpg|||||',
    PassData: '75646',
    RadioData: 'M:1',
    CheckData: 0
  },
  {
    SEQ: 3,
    TextData: '최호건',
    ComboData: '01',
    ISO: 'GBP',
    Currency: '영국 파운드',
    IntData: 65,
    FloatData: 154.36,
    DateData: '',
    PhoneNo: '',
    LinesData: '',
    Userformat: '',
    ImageData: '|../assets/imgs/ch.jpg|||||',
    PassData: '4564',
    RadioData: 'H:1',
    CheckData: 0
  }
];

// 임의의 데이터를 이용한 엑셀 다운로드
sheet.exportData({ directExcelData: tmpData });
```
!-->

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


        sheet.exportData(param);

```
![exHead,exFoot](/assets/imgs/exportDataExHeadExFoot.png "exHead,exFoot")


### Read More

- [importData method](./import-data)
- [AutoExcelMode cfg](/docs/props/cfg/auto-excel-mode)
- [LevelMark cfg](/docs/props/cfg/level-mark)
- [down2Excel method](/docs/funcs/excel/down-to-excel)
- [down2Text method](/docs/funcs/excel/down-to-text)
- [onBeforeExport event](/docs/events/on-before-export)
- [onExportFinish event](/docs/events/on-export-finish)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.0.0.6|`fileName`, `sheetName`, `downRows`, `downCols`, `downRows`, `downTreeHide`, `downHeader`, `sheetDesign`, `titleText`, `userMerge`, `excelRowHeight`, `excelHeaderRowHeight`, `wordWrap`, `comboValidation`, `rowDelim`, `colDelim`, `downSum` 기능 추가|
|core|8.0.0.20|파일 형식 내용 추가|
|core|8.0.0.21|`merge`, `allTypeToText`, `checkBoxOnValue`, `checkBoxOffValue`, `excelFontSize`, `excludeFooterRow`, `numberTypeToText` (xlsx 에서만 지원)|
|core|8.0.0.29|`excelFontFamily` 기능 추가 (xlsx 에서만 지원)|
|core|8.1.0.30|`exHead`,`exFoot` 기능 추가 (xlsx 에서만 지원)|
|core|8.1.0.39|`excelRowHeight : -1` 설정 추가|
|core|8.1.0.41|`sheetDesign : 4` 설정 추가|
|core|8.1.0.83|`appendPrevSheet` 설정 추가 (exportDataBuffer 사용시에만 사용 가능)|
|core|8.2.0.5|`onlyHeaderMerge` 설정 추가|
|core|8.2.0.11|`hiddenColumn` 설정 추가|
|core|8.2.0.25|`freezePane` 설정 추가|
|core|8.3.0.16|`numberFormatMode` 설정 추가|
|core|8.4.0.7|`widthRate` 설정 추가|
|core|8.4.0.10|`escapeCsvInjection` 설정 추가 (csv 형식 전용)|
<!--!
|`[비공개]` core|8.0.0.22|`downCombo` 기능 추가|
|`[비공개]` core|8.1.0.4|`excelPage.paperSize`, `excelPage.orientation`, `excelPage.marginLeft`, `excelPage.marginRight`, `excelPage.marginTop`, `excelPage.marginBottom`, `excelPage.marginHeader`, `excelPage.marginFooter` 기능 추가|
|`[비공개]` core|8.1.0.6|`directExcelData` 기능 추가|
|`[비공개]` core|8.1.0.40|`requiredMark` 기능 추가|
|`[비공개]` core|8.1.0.73|`excelPage.fitToWidth`, `excelPage.fitToHeight` 기능 추가|
!-->

# down2Hwpx ***(method)***

<!-- synonyms: 한글 다운로드, HWPX 다운로드, 한글 파일 내보내기, down to hwpx -->

> 시트의 내용을 한글(Hwpx) 파일로 다운로드합니다.  
> 사용 전 [서버모듈 설치](/docs/appx/import-export)와 `/plugins/ibsheet-excel.js` 스크립트 로드가 필요합니다.  
> 이 함수를 호출하면 `Cfg.Export` 속성에 지정한 `Down2Hwpx.jsp`가 호출되며, 이 jsp 파일이 시트 정보(컬럼 정의 등)와 데이터를 받아 한글 파일을 생성해 클라이언트로 전송합니다.  
> 시트마다 반복 설정이 번거로우면 [IBSheet.CommonOptions](/docs/static/common-options)로 공통 적용할 수 있습니다.

### Syntax
```javascript
void down2Hwpx( param );
```

### Parameters

|Name|Type|Required|Description|
|----------|-----|---|----|
|fileName|`string`|<span class='optional'>선택</span>|생성할 한글파일 명 (`default: "Hwpx.hwpx"`) <br/>**한글 (hwpx)파일명을 지정합니다.**|
|downRows|`string`|<span class='optional'>선택</span>|지정한 행만 다운로드 합니다.<br> 별도의 설정이 없을시 모든 행이 다운로드 됩니다.<br> 보여지는 행만 다운로드하고 싶을 경우 `"Visible"`로 설정하면 됩니다.<br> (ex: "1\|3\|4\|5\|9" 식의 문자열)<br> `downRows`를 사용하면 머지 기능이 동작하지 않습니다.|
|downCols|`string`|<span class='optional'>선택</span>|지정한 열만 다운로드 합니다.<br/> 별도의 설정이 없을시 모든 열이 다운로드 됩니다.<br> 보여지는 열만 다운로드하고 싶을 경우 `"Visible"`로 설정하면 됩니다.<br/>(ex: "Price\|AMT\|TOTAL" 식의 문자열)|
|downHeader|`boolean`|<span class='optional'>선택</span>|헤더행을 다운로드 할지 여부를 설정합니다.<br>`0(false)`:다운로드 시 헤더행 미포함<br>`1(true)`:다운로드 시 헤더행 포함 (`default`)|
|sheetDesign|`number`|<span class='optional'>선택</span>|`main.css` 파일에 설정된 시트의 디자인 요소를 한글 문서의 표에도 반영할지 여부를 설정합니다. <br> 반영되는 디자인 요소는 다음과 같습니다: 헤더의 배경색,폰트명,폰트크기,데이터 배경색 <br>`0`:셀 외곽선을 제외한 모든 디자인을 적용하지 않습니다.<br/>`1`:셀 외곽선을 포함해 모든 디자인을 적용합니다. (`default`) <br>`2`:셀 외곽선을 제외한 셀 스타일을 적용합니다. <br/>`3`:셀 외곽선 및 스타일을 모두 적용하지 않습니다. <br/>`4`:헤더행에만 모든 디자인을 적용합니다.
|merge|`boolean`|<span class='optional'>선택</span>|시트의 머지 상태를 표에 그대로 반영할지를 설정합니다.<br>`0(false)`:시트의 머지 상태를 표에 반영 안함 (`default`)<br>`1(true)`:시트에 머지 상태를 표에 반영|
|downSum|`boolean`|<span class='optional'>선택</span>|합계 행 다운로드 여부를 설정합니다.<br>`0(false)`:합계 행 다운로드 시 미포함<br>`1(true)`:합계 행 다운로드 시 포함 (`default`)|
|sheetFontSize|`number`|<span class='optional'>선택</span>|시트의 폰트 크기를 설정합니다. <br> 설정된 폰트 크기는 한글 문서의 표에만 적용됩니다.|
|excludeFooterRow|`boolean`|<span class='optional'>선택</span>|푸터 행 제외 여부를 설정합니다.<br>`0(false)`:푸터 행 포함 (`default`) <br>`1(true)`:푸터 행 제외|
|reqHeader|`object`|<span class='optional'>선택</span>|서버 전송 헤더에 사용자가 지정한 헤더 정보를 설정합니다.|
|extendParam|`string`|<span class='optional'>선택</span>|서버로 전달해야 하는 내용이 있는 경우 `GET` 방식의 `QueryString`으로 연결하여 서버로 같이 전달됩니다.<br/> (ex: `sheet.down2Excel({extendParam: "sido=서울시&sigungu=관악구"}`)|
|extendParamMethod|`string`|<span class='optional'>선택</span>|`extendParam`의 내용을 `GET` 또는 `POST`로 전달할지를 설정합니다.(`default: "GET"`)|
|excludeSubSum|`boolean`|<span class='optional'>선택</span>|소계/누계 행 제외 여부를 설정합니다.<br/> `0(false)`: 소계/누계 모두 제외하지 않습니다. (`default`)<br/> `1(true)`: 소계/누계 모두 제외합니다.|
|landScape|`boolean`|<span class='optional'>선택</span>|한글 문서의 편집용지 방향을 설정합니다.<br/>`0(false)`:세로방향 (`default`)<br/>`1(true)`:가로방향|
|top|`object`|<span class='optional'>선택</span>|시트를 기준으로 상단에 표현할 문자열을 삽입합니다. <br/><table><tr><td>**Name**</td><td>**Type**</td><td>**Required**</td><td>**Description**</td></tr><tr><td>topAlign</td><td>`string`</td><td><span class='optional'>선택</span></td><td>`left, center, right` 중 정렬을 설정합니다.(`default: "center"`)</td></tr><tr><td>topFontBold</td><td>`boolean`</td><td><span class='optional'>선택</span></td><td>폰트의 굵기를 설정합니다. (`default: 0(false)`)</td></tr><tr><td>topFontColor</td><td>`string`</td><td><span class='optional'>선택</span></td><td>폰트 색상을 설정합니다.</td></tr><tr><td>topFontSize</td><td>`number`</td><td><span class='optional'>선택</span></td><td>폰트 크기를 설정합니다.</td></tr><tr><td>topText</td><td>`string`</td><td><span class='optional'>선택</span></td><td>상단에 표현할 문자열을 설정합니다.\r\n 을 사용하면 줄바꿈이 가능합니다.</td></tr></table>(ex: `top: [{topText: "상단영역 첫번째 줄", topAlign: "center", topFontSize: 10, topFontBold: true, topFontColor:"#ff0000"},`<br> `{topText: "상단영역 두번째 줄", topAlign: "right", topFontSize: 8, topFontBold: false, topFontColor:"#000000"}]`)|
|bottom|`object`|<span class='optional'>선택</span>|시트를 기준으로 하단에 표현할 문자열을 삽입합니다.<table><tr><td>**Name**</td><td>**Type**</td><td>**Required**</td><td>**Description**</td></tr><tr><td>bottomAlign</td><td>`string`</td><td><span class='optional'>선택</span></td><td>`left, center, right` 중 정렬을 설정합니다.(`default: "center"`)</td></tr><tr><td>bottomFontBold</td><td>`boolean`</td><td><span class='optional'>선택</span></td><td>폰트의 굵기를 설정합니다(`default: 0(false)`)</td></tr><tr><td>bottomFontColor</td><td>`string`</td><td><span class='optional'>선택</span></td><td>폰트 색상을 설정합니다.</td></tr><tr><td>bottomFontSize</td><td>`number`</td><td><span class='optional'>선택</span></td><td>폰트 크기를 설정합니다.</td></tr><tr><td>bottomText</td><td>`string`</td><td><span class='optional'>선택</span></td><td>하단에 표현할 문자열을 설정합니다.\r\n 을 사용하면 줄바꿈이 가능합니다.</td></tr></table>(ex: `bottom: [{bottomText: "하단영역 첫번째 줄", bottomAlign: "center", bottomFontSize: 10, bottomFontBold: true, bottomFontColor:"#ff0000"},`<br> `{bottomText: "하단영역 두번째 줄", bottomAlign: "right", bottomFontSize: 8, bottomFontBold: false, bottomFontColor:"#000000"}]`)|
|hwpxHeader|`object`|<span class='optional'>선택</span>|머리말 영역에 표현할 문자열을 삽입합니다.<table><tr><td>**Name**</td><td>**Type**</td><td>**Required**</td><td>**Description**</td></tr><tr><td>hwpxHeaderAlign</td><td>`string`</td><td><span class='optional'>선택</span></td><td>`left, center, right` 중 정렬을 설정합니다.(default: "center")</td></tr><tr><td>hwpxHeaderFontBold</td><td>`boolean`</td><td><span class='optional'>선택</span></td><td>폰트의 굵기를 설정합니다(default: false)</td></tr><tr><td>hwpxHeaderFontColor</td><td>`string`</td><td><span class='optional'>선택</span></td><td>폰트 색상을 설정합니다.</td></tr><tr><td>hwpxHeaderFontSize</td><td>`number`</td><td><span class='optional'>선택</span></td><td>폰트 크기를 설정합니다.</td></tr><tr><td>hwpxHeaderText</td><td>`string`</td><td><span class='optional'>선택</span></td><td>하단에 표현할 문자열을 설정합니다.\r\n 을 사용하면 줄바꿈이 가능합니다.</td></tr></table>(ex: `hwpxHeader: [{hwpxHeaderText: "머리말 영역 첫번째 줄", hwpxHeaderAlign: "center", hwpxHeaderFontSize: 10, hwpxHeaderFontBold: true, hwpxHeaderFontColor:"#ff0000"},`<br> `{hwpxHeaderText: "머리말 영역 두번째 줄", hwpxHeaderAlign: "right", hwpxHeaderFontSize: 8, hwpxHeaderFontBold: false, hwpxHeaderFontColor:"#000000"}]`)|
|hwpxFooter|`object`|<span class='optional'>선택</span>|꼬리말 영역에 표현할 문자열을 삽입합니다.<table><tr><td>**Name**</td><td>**Type**</td><td>**Required**</td><td>**Description**</td></tr><tr><td>hwpxFooterAlign</td><td>`string`</td><td><span class='optional'>선택</span></td><td>`left, center, right` 중 정렬을 설정합니다.(default: "center")</td></tr><tr><td>hwpxFooterFontBold</td><td>`boolean`</td><td><span class='optional'>선택</span></td><td>폰트의 굵기를 설정합니다(default: false)</td></tr><tr><td>hwpxFooterFontColor</td><td>`string`</td><td><span class='optional'>선택</span></td><td>폰트 색상을 설정합니다.</td></tr><tr><td>hwpxFooterFontSize</td><td>`number`</td><td><span class='optional'>선택</span></td><td>폰트 크기를 설정합니다.</td></tr><tr><td>hwpxFooterText</td><td>`string`</td><td><span class='optional'>선택</span></td><td>하단에 표현할 문자열을 설정합니다.\r\n 을 사용하면 줄바꿈이 가능합니다.</td></tr></table>(ex: `hwpxFooter: [{hwpxFooterText: "꼬리말 영역 첫번째 줄", hwpxFooterAlign: "center", hwpxFooterFontSize: 10, hwpxFooterFontBold: true, hwpxFooterFontColor:"#ff0000"},`<br> `{hwpxFooterText: "꼬리말 영역 두번째 줄", hwpxFooterAlign: "right", hwpxFooterFontSize: 8, hwpxFooterFontBold: false, hwpxFooterFontColor:"#000000"}]`)|
|topMargin|`number`|<span class='optional'>선택</span>|편집 용지 위쪽 여백을 설정합니다.(`단위:mm`) (`default: 20`)|
|bottomMargin|`number`|<span class='optional'>선택</span>|편집 용지 아래쪽 여백을 설정합니다.(`단위:mm`) (`default: 20`)|
|leftMargin|`number`|<span class='optional'>선택</span>|편집 용지 왼쪽 여백을 설정합니다.(`단위:mm`) (`default: 30`)|
|rightMargin|`number`|<span class='optional'>선택</span>|편집 용지 오른쪽 여백을 설정합니다.(`단위:mm`) (`default: 30`)|
|headerMargin|`number`|<span class='optional'>선택</span>|편집 용지 머리말 영역 여백을 설정합니다.(`단위:mm`) (`default: 15`)|
|footerMargin|`number`|<span class='optional'>선택</span>|편집 용지 꼬리말 영역 여백을 설정합니다.(`단위:mm`) (`default: 15`)|
|botPage|`boolean`|<span class='optional'>선택</span>|한글 문서 하단 부분 페이지 표시 여부를 설정합니다. <br>`0(false)`:한글 문서 하단 부분 페이지 미표시 (`default`)<br>`1(true)`:한글 문서 하단 부분 페이지 표시|
|repeatHeader|`boolean`|<span class='optional'>선택</span>|시트가 페이지를 넘어가는 경우 시트의 헤더를 반복 출력 여부를 설정합니다. <br>`0(false)`:시트가 페이지를 넘어가는 경우 시트의 헤더 반복 출력하지 않음<br>`1(true)`:시트가 페이지를 넘어가는 경우 시트의 헤더 반복 출력 (`default`)|
|tempFile|`string`|<span class='optional'>선택</span>|템플릿 파일명을 설정합니다. <br>템플릿 파일의 경우 `Down2Hwpx.jsp`의 `setTempRoot`가 설정되어있어야 합니다. <br>`setTempRoot` 의 경우 템플릿 파일이 존재하는 서버의 경로입니다.
|keyField|`object`|<span class='optional'>선택</span>|템플릿기능 사용시 한글의 `필드`기능을 사용한 경우 사용하는 속성입니다.<br> `필드`에서 `필드 이름`이 `keyField`의 키값과 동일한 경우 해당 값으로 매핑됩니다.<br> (ex: `sheet.down2Excel({keyField: {"name": "홍길동"}}` <br>`필드 이름` 중 `name`으로 설정된 필드 값이 `홍길동`으로 매핑 됨) 
|sheetField|`string`|<span class='optional'>선택</span>|템플릿기능 사용시 한글의 `필드`기능을 사용한 경우 사용하는 속성입니다.<br> `필드`에서 `필드 이름`이 `sheetField` 의 값과 동일한 필드가 한글의 표로 변환됩니다.<br> (ex: `sheet.down2Excel({sheetField: "ibsheet"}`<br> `필드 이름` 이 `ibsheet `으로 설정된 필드가 내려받을 `ibsheet`의 위치)


### 한글의 필드 기능 사용 정리
한글에서는 `필드` 기능을 지원합니다. 쉽게 생각하면 <input> 태그의 placeholder 속성 기능이라고 생각하시면 되겠습니다.<br>
`down2Hwpx`에서는 필드 기능을 활용해 원하는 위치에 시트를 표현 및 원하는 값을 입력할 수 있습니다.<br>
![image](/assets/imgs/hanField1.png)<br>
![image](/assets/imgs/hanField2.png)<br>
`필드 이름`을 year로 설정한 경우 `keyField`속성을 아래와 같이 설정하면 year가 2024로 표현됩니다.
```javascript
var param1 = {
        fileName:"문서.hwpx",
        //tempFile과 keyField는 첫번째에서만 설정.
        tempFile:"template.hwpx",
        keyField: {
                "year": "2024",
        },
        sheetField : "sheet1"
};
sheet1.down2Hwpx(param1);
```




### downCols, downRows 사용시 merge 적용 정리

| downCols |화면과 동일하게 컬럼 설정 | 화면과 다르게 컬럼 설정 |
| ------ | ------ | ------ |
| downRows 사용| X |  X |
| downRows 사용 안함 | O | 아래 설명 참고|

merge 옵션을 적용해 downCols를 사용하시려면 downCols에 머지가 이뤄진 컬럼을 **순서대로** **모두** 포함하고 있어야만 합니다. **Visible: 0이 설정된 컬럼이 있다면 해당 컬럼도 반드시 downCols에 포함해둬야만 합니다.** <br>

머지가 이뤄진 컬럼 중 특정 컬럼이 빠지거나, 머지가 이뤄진 컬럼을 모두 포함하고 있더라도 다운로드 받는 컬럼의 순서가 다르면 한들 문서에서 머지가 정상적으로 이뤄지지 않습니다. <br>

<br>

![downCols사용시 머지](/assets/imgs/downcols_merge.png "downCols사용시 머지")

<br>

이미지로 예를 들자면,  "머지 컬럼" 컬럼을 온전히 머지가 적용된 채로 다운로드받고 싶다면 downCols: "컬럼1|컬럼2|컬럼3|컬럼4"와 같이 설정하셔야 합니다. <br>

downCols: "컬럼2|컬럼3|컬럼4"와 같이 특정 컬럼을 제외하거나 downCols: "컬럼4|컬럼1|컬럼3|컬럼2"와 같이 컬럼 순서를 바꾸시면 머지가 온전히 적용되지 않습니다. 



### Return Value
***none***

### Example
```javascript
var param = {
    merge: 1,
    hwpxHeader: [{
        hwpxHeaderText: "머릿글 영역",
        hwpxHeaderAlign: "Center",
        hwpxHeaderFontSize: 8,
        hwpxHeaderFontColor: '#945151'
    }],
    top: [{
        topText: "시트 상단 영역 첫번째 줄",
        topAlign: "center",
        topFontSize: 10,
        topBorder: true
    }, {
        topText: "시트 상단 영역 두번째 줄",
        topAlign: "center",
        topFontSize: 30,
        topFontColor: '#821751'
    }],
    sheetDesign: 1,
    fileName: "test",
    bottom: [{
        bottomText: "시트 하단 영역 첫번째 줄",
        bottomAlign: "center",
        bottomFontSize: 20
    }, {
        bottomText: "시트 하단 영역 두번째 줄",
        bottomAlign: "right",
        bottomFontSize: 10
    }],
    topMargin: 10,
    leftMargin: 10,
    rightMargin: 10,
    headerMargin: 10,
    hwpxFooter: [{
        hwpxFooterText: "바닥글 영역",
        hwpxFooterAlign: "Center",
        hwpxFooterFontSize: 8,
        hwpxFooterFontColor: '#245151'
    }, {
        hwpxFooterText: "바닥글 영역 두번째 줄",
        hwpxFooterAlign: "Center",
        hwpxFooterFontSize: 5,
        hwpxFooterFontColor: '#142991'
    }],
    sheetFontSize: 10,
    // 용지 방향 설정
    landScape: false
};
sheet.down2Hwpx(param);
```

### Read More

- [down2HwpxBuffer method](./down-to-hwpx-buffer)
- [down2Excel method](./down-to-excel)
- [down2Pdf method](./down-to-pdf)
- [down2Text method](./down-to-text)
- [onBeforeExport event](/docs/events/on-before-export)
- [onExportFinish event](/docs/events/on-export-finish)


### Since

|product|version|desc|
|---|---|---|
|core|8.1.0.85|Down2Hwpx 기능 추가|
|excel|1.1.2|Down2Hwpx 기능 추가|
|jar|1.0.0|Down2Hwpx 기능 추가|

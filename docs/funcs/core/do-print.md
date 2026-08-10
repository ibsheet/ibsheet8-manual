# doPrint ***(method)***

<!-- synonyms: 인쇄, 프린트, 시트 인쇄, 출력, 프린트 실행, 인쇄 실행, do-print, doPrint, do print, print sheet, print, printing -->

> 시트의 내용을 원하는 규격으로 인쇄합니다.
>
> 용지 규격과 방향은 브라우저의 인쇄 설정과 동일하게 설정해 주어야 합니다.
>
> **<mark>주의</mark> : 인쇄 결과가 브라우저 별로 상이 할 수 있습니다.** 
>
> **<mark>주의</mark> : `zoomFit` 속성이 `0`일 경우 `fitPage` 속성은 동작하지 않습니다** 
>
> **<mark>주의</mark> : 멀티레코드([MultiRecord](/docs/props/cfg/multi-record)) 기능을 사용하는 시트에서는 제약이 있습니다**

### Syntax
```js
void doPrint( prefix, postfix, pagePrefix, pagePostfix, fitPage, zoomFit, menu, pageOrient, firstPrintHead );
```

### Parameters

|Name|Type|Required|Description|
|----------|-----|---|----|
|prefix|`string`|<span class='optional'>선택</span>|첫 페이지 상단에 표시될 문자열 (HTML 형식 가능)|
|postfix|`string`|<span class='optional'>선택</span>|마지막 페이지 하단에 표시될 문자열 (HTML 형식 가능)|
|pagePrefix|`string`|<span class='optional'>선택</span>|각 페이지 상단(머릿말)에 표시될 문자열 (HTML 형식 가능)|
|pagePostfix|`string`|<span class='optional'>선택</span>|각 페이지 하단(꼬릿말)에 표시될 문자열 (HTML  형식 가능)|
|fitPage|`number`|<span class='optional'>선택</span>|인쇄할 시트의 크기가 페이지보다 클 경우, 페이지에 맞춤 옵션<br/>`0`:없음<br/>`1`:너비에 맞춤 <i>(`default`)</i><br/>`2`:높이에 맞춤<br/>`3`:한 페이지에 맞춤|
|zoomFit|`number`|<span class='optional'>선택</span>|시트의 크기가 페이지보다 작을 경우, 페이지에 맞춤 옵션<br/>`0`:없음<br/>`1`:한 페이지에 맞춤 <i>(`default`)</i>|
|menu|`number`|<span class='optional'>선택</span>|프린트 다이얼로그 사용 여부<br/>`0`:사용안함 <i>(`default`)</i><br/>`1`:행열 선택 옵션만 보기<br/>`2`:전체 옵션 보기|
|pageOrient|`number`|<span class='optional'>선택</span>|인쇄 용지 방향 설정<br/>`0`:세로 <i>(`default`)</i><br/>`1`:가로<br/><br/>**<mark>주의</mark> : 해당 속성은 Chrome 브라우저에서만 동작합니다**|
|firstPrintHead|`boolean`|<span class='optional'>선택</span>|인쇄시 용지 첫 페이지만 시트의 헤더가 인쇄<br/>`0(false)`:모든 페이지에서 시트의 헤더 표시 <i>(`default`)</i><br/>`1(true)`:첫 페이지만 시트의 헤더 표시<br/>|

#### `pagePrefix`, `pagePostfix`에서의 예약어 사용

* `%1`: 가로 페이지 인덱스
* `%2`: 세로 페이지 인덱스
* `%3`: 페이지 인덱스
* `%4`: 가로 페이지 개수
* `%5`: 세로 페이지 개수
* `%6`: 페이지 개수

### Return Value
***none***

### Browser Constraint

|Browser|Constraint|
|-------|----------|
|Chrome|제약 없음|
|Edge(Chrominu)|제약 없음|
|Firefox|시트 스타일, Html 스타일 적용 안됨<br/>`pageOrient` 사용 불가|
|Opera|`pageOrient` 사용 불가|
|IE11|시트 스타일, Html 스타일 적용 안됨<br/>`pageOrient` 사용 불가|

### Examples

#### 옵션객체만 사용하는 경우

```js
var options = {
  prefix: "<div style='background-color:#EDEDED;padding:10px'>사용자 : 홍길동</div>",
  pagePostfix: "<div style='text-align:center;font-size:20px'>[%2 / %5]</div>",
  fitPage: 1
};

sheet.doPrint(options);
```

#### CSS와 함께 사용하는 경우

`prefix`, `pagePrefix`, `pagePostfix`, `postfix` 클래스명은 고유하므로 변경 불가, 이외의 클래스명으로 크기와 관련된 속성을 정의할 경우 출력 페이지의 레이아웃에 반영되지 않습니다.

##### HTML

```html
<!-- ... -->
<head>
  <!-- ... -->
  <link href="ibsheet-print.css" rel="stylesheet" type="text/css" />
  <!-- ... -->
</head>
```

##### SCSS (ibsheet-print.scss)

```scss
BODY[class*=BodyPrint] > DIV[class*=PrintPage] DIV[class*=PaddingWrapper] {
  > .prefix {
    font-size: 2rem;
    font-weight: bold;
    padding: 1.5rem 0 1rem;
    text-align: center;
  }
  > .pagePrefix {
    text-align: right;
    padding: 1rem 0;
  }
  > .pagePostfix {
    font-size: .5rem;
    text-align: center;
  }
  > .postfix {
    font-size: .8rem;
    text-align: center;
  }
}
```

##### CSS (ibsheet-print.css)

```css
BODY[class*=BodyPrint] > DIV[class*=PrintPage] DIV[class*=PaddingWrapper] > .prefix {
  font-size: 2rem;
  font-weight: bold;
  padding: 1.5rem 0 1rem;
  text-align: center;
}
BODY[class*=BodyPrint] > DIV[class*=PrintPage] DIV[class*=PaddingWrapper] > .pagePrefix {
  text-align: right;
  padding: 1rem 0;
}
BODY[class*=BodyPrint] > DIV[class*=PrintPage] DIV[class*=PaddingWrapper] > .pagePostfix {
  font-size: .5rem;
  text-align: center;
}
BODY[class*=BodyPrint] > DIV[class*=PrintPage] DIV[class*=PaddingWrapper] > .postfix {
  font-size: .8rem;
  text-align: center;
}
```

##### JavaScript

`prefix`, `pagePrefix`, `pagePostfix`, `postfix` 값의 형식이 HTML이 아닐 경우, DIV 엘리먼트에 해당 속성의 클래스명이 자동으로 추가되어 적용됩니다.

```js
var options = {
  prefix: '문서 제목',
  pagePrefix: 'IB Leaders',
  pagePostfix: '[ %3 / %6 ]',
  postfix: 'Powered by IBSheet8'
};

sheet.doPrint(options);
```

### Read More

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.0.0.17|`pageOrient` 기능 추가|
|core|8.1.0.51|`firstPrintHead` 기능 추가|
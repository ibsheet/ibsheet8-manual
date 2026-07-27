# Format ***(appendix)***
> 셀 값이 IBSheet에 표시될 때 적용되는 **표시 포맷(display format)** 을 정의합니다.  
> Format은 **데이터 표시 방식만 변경하며 실제 데이터 값은 변경하지 않습니다.**  
> 값을 읽을 때([getValue](/docs/funcs/core/get-value))나 저장([doSave](/docs/funcs/core/do-save), [getSaveString](/docs/funcs/core/get-save-string)) 시에는 포맷이 적용되지 않은 **실제 값**이 사용됩니다. 
> 
> `Format`은 열의 [Type](./type)에 따라 정의 방식이 달라집니다.

### 포맷 종류 (Format Types)

다음 링크를 클릭하면 해당 포맷 설명으로 바로 이동합니다.

- <a href="#text-lines-format">Text / Lines 타입 포맷</a>
- <a href="#date-format">Date 타입 포맷</a>[](#)
- <a href="#number-format">숫자 타입 포맷(Int / Float)</a>
- <a href="#html-format">Html 타입 포맷</a>
- <a href="#link-format">Link 타입 포맷</a>
- <a href="#img-format">Img 타입 포맷</a> 
- <a href="#file-format">File 타입 포맷</a> 

---

<a id="text-lines-format"></a>
## 1. 타입이 Text, Lines 인 경우 
Text 타입에서는 **문자열 변환, 문자열 치환, 값 매핑 방식의 Format**을 사용할 수 있습니다.  
실제 값의 앞뒤에 문자열을 추가하거나 문자열 일부를 다른 문자열로 변경하여 표시할 수 있습니다.  
또한 **Object(JSON) 형식으로 실제 값과 화면에 표시될 값을 매핑할 수 있습니다.**  

`주민등록번호`나, `카드번호`와 같이 숫자와 구분자로 연결된 형식의 Format을 적용하고자 하실 경우에는 [CustomFormat](/docs/props/col/custom-format) 속성을 사용하세요.

### 1) 구분자 활용 방식
첫 번째 문자를 **구분자(delimiter)** 로 사용하여 여러 설정 값을 정의합니다.
* 첫 문자를 구분자로 사용하여 구분된 설정 값들의 나열로 정의됩니다.  
* 구분자로 사용된 문자는 설정할 내용에 포함되면 안됩니다.

##### Syntax
```javascript
// 구분자 활용 방식 첫문자 '|'이 구분자
Format: "|LetterType|Prefix|Postfix|Search|Flags|Replace"
```

|Value|Description|
|---|---|
|LetterType|대소문자를 구분할지 여부 및 기타 설정<br/>0 : 대소문자 구분 없음<br/>1 : 영문을 소문자로 표현<br/>2 : 영문을 대문자로 표현<br/>3 : 각 지역 문자의 소문자 사용<br/>4 : 각 지역 문자의 대문자 사용|
|Prefix|셀 값 앞에 붙일 문자열|
|Postfix|셀 값 뒤에 붙일 문자열|
|Search|정규 표현식으로 찾을 문자열|
|Flags|자바스크립트 정규식 Flag (i,g,m 가능)<br/>i : 대소문자 구분 없음<br/>g : 전체 변경<br/>m : 줄넘김 포함 검색|
|Replace|Search로 찾은 문자열을 대체할 문자열|

##### Example

```javascript
//열 설정
options.Cols = [
    {
        Name:"sTitle",
        Type:"Text",
        // 셀의 값을 모두 대문자로 보여줍니다. 또한 앞에 '☜☜☜', 뒤에 '☞☞☞' 문자를 추가하고, 
        // 셀 값에 있는 "=" 문자열을 ":::" 로 대체합니다.
        Format:"|2|☜☜☜|☞☞☞|=|ig|:::"
    }
    
]

//조회 데이터
{"Data":[
    {"sTitle":"붉은 악마=Red Devils"}
]}
```
*시트내에 보여지는 데이터*<br>
![보여지는 데이터](/assets/imgs/textFormat2.png "보여지는 데이터")

<br><br>

### 2) 객체 방식
  * JSON 형태로 실제 값과 화면에 표시될 값의 쌍으로 구성됩니다.
  * 표시 문자열에는 HTML을 사용할 수 있습니다.
 
##### Syntax
```javascript
// 객체 방식
Format: {
    'Key1':'Value1', 
    'Key2':'Value2', 
    'key3':'Value3'
}
```
|Value|Description|
|---|---|
|Key|셀의 실제 값|
|Value|화면에 표시될 값|

##### Example
```javascript
// 열설정
options.Cols = [
    {
        Name:"sCountry",
        Type:"Text",
        // 셀 값이 A인 경우 한국으로, B인 경우 일본으로, C인 경우 중국으로 대체되어 화면에 보입니다.
        Format:{
          'A':'<b>한국</b>',
          'B':'일본',
          'C':'중국'
        }
    }
    
]

// 조회 데이터
{"Data":[
    { "sCountry":"A"}
]}
```

*시트내에 보여지는 데이터*<br>
![보여지는 데이터](/assets/imgs/textFormat4.png "보여지는 데이터")


<br><br><br><br>

---
<a id="date-format"></a>
## 2. 타입이 Date 인 경우  
Date 타입에서는 **예약어의 조합을 사용하여 날짜 표시 형식**을 정의합니다.
다음 세 가지 속성을 함께 사용하여 날짜 형식을 정의할 수 있습니다.

|속성|설명|
|---|---|
|Format|IBSheet에 표시되는 날짜 형식|
|EditFormat|셀 편집 시 입력되는 날짜 형식|
|DataFormat|서버와 주고받는 날짜 데이터 형식|

* 예약어의 조합
  * `y`(년), `M`(월), `d`(일), `H`/`h`(시간), `m`(분), `s`(초), `t`(오전/오후)등의 예약어와 일반 문자를 조합하여 사용할 수 있습니다.
  * 포맷이 비어있는 경우 기본 날짜 형식인 **yyyy/MM/dd**가 사용됩니다.
  
<!--!
  * `[비공개 설명]` H는 24시간제를, h는 12시간제를 의미합니다.
!-->
<!--!
* 메시지 파일에 따른 자동 포맷 설정 기능 
  * d, h 등의 한 자리 예약어를 사용해서 메시지 파일에 따라 자동적으로 컬럼 포맷을 설정하도록 처리하실 수 있습니다. <br>

|Value|Description|
|---|---|
|m|월, 일 데이터를 포함해서 포맷 형성("M/d")|
|d|년, 월, 일 데이터를 포함해서 포맷 형성("M/d/yyyy")|
|h|년, 월, 일, 시, 분 데이터를 포함해서 포맷 형성("M/d/yyyy H:mm")|
|t|시, 분 데이터를 포함해서 포맷 형성("H:mm")|
|T|시, 분, 초 데이터를 포함해서 포맷 형성("H:mm:ss")|
|Y|년, 월 데이터에 문자 포함해서 포맷 형성("4월 2013")|
|D|년, 월, 일 데이터에 문자 포함해서 포맷 형성("23일 4월 2013")|
|l|년, 월, 일 데이터에 문자 포함하고, 시, 분 데이터 덧붙여 포맷 형성("23일 4월 2013 9:10")|
|L|년, 월, 일 데이터에 문자 포함하고, 시, 분, 초 데이터 덧붙여 포맷 형성("23일 4월 2013 9:10:20")|
!-->

### Syntax
```javascript
    // 예약어의 조합
    Format: "yyyy.MM.dd"
```
|Format|Description|Example|
|---|---|---|
|yyyy|4자리 년도|2018|
|yy|2자리 년도|2018 → 18|
|y|1~2자리 년도|2018 → 18, 2008 → 8|
|MMMM|월 이름(전체)|April / 4월|
|MMM|월 이름(축약)|Apr / 4월|
|MM|2자리 월|04|
|M|1~2자리 월|12 → 12, 04 → 4|
|dddd|요일(전체)|Friday / 금요일|
|ddd|요일(축약)|Fri / 금|
|dd|2자리 일|05|
|d|1~2자리 일|12 →12, 04 →4|
|HH|24시간 (00~23)|12|
|H|24시간 (0~23)|12 → 12, 04 → 4|
|hh|12시간 (01~12)|03|
|h|12시간 (1~12)|12 → 12, 03 → 3|
|mm|분 (00~59)|08|
|m|분 (0~59)|12|
|ss|초 (00~59)|09|
|s|초 (0~59)|12 → 12, 03 → 3|
|tt|오전 / 오후 표시|AM, PM |
|t|오전 / 오후 표시(축약)|A, P |

※ `h`, `hh`는 12시간 형식이므로 `t` / `tt`(오전/오후 표시자)와 함께 사용하는 것이 일반적입니다.


### Example

```javascript
// 열 설정
options.Cols = [
    {
        "Name" : "startDate",
        "Type" : "Date",
        "Format" : "yyyy.MM.dd (ddd)",    //화면에 보이는 데이터의 형식
        "EditFormat" : "dd-MM-yyyy",//편집시 사용자에게 보여질 데이터 형식
        "DataFormat" : "yyyyMMdd"   //서버에서 데이터를 받거나 보낼때 데이터 형식
    }
]    

//조회 데이터
{"Data":[
    {"startDate":"20190725"} //2019년 7월 25일
]}
```

*실제 보여지는 데이터(Format)*<br>
![보여지는 데이터](/assets/imgs/dateFormat1.png "보여지는 데이터")<br>

*편집시 보여지는 데이터(EditFormat)*<br>
![편집시 보여지는 데이터](/assets/imgs/dateFormat2.png "편집시 보여지는 데이터")


***Date타입과 그에 따른 포맷들(Format,EditFormat,DateFormat)을 [Extend](/docs/props/col/extend) 속성을 통해 한번에 정의할 수 있습니다.***

*Extend 사용 설정*

```
javascript
    options.Cols = [
        {
            "Name" : "startDate",
            // Type, Format, EditFormat등이 미리 정의된 변수 사용
            // ibsheet-common.js 파일에 IB_Preset으로 정의되어 있음
            "Extend" : IB_Preset.YMD 
        }
    ]
```



<br><br><br><br>

---
<a id="number-format"></a>
## 3. 타입이 Int, Float 인 경우 
Int, Float 타입에서는 **숫자 표시 형식을 지정하기 위해 Format을 사용합니다.**  
숫자 포맷은 **예약어와 일반 문자를 조합하여 정의**할 수 있습니다.

### 기본 포맷
|Type|기본 Format|
|---|---|
|Int|#,##0|
|Float|#,##0.######|

### 예약어

|예약어|설명|
|---|---|
|0|값이 없으면 0으로 채움|
|#|값이 있을 때만 표시|
|,|천 단위 구분자|
|.|소수점 구분자|
|%|값에 100을 곱하여 퍼센트로 표시|

<!--  * "0" : 값이 없는 경우 0을 기본값으로 채웁니다.
  * "#" : 값이 있을때만 표현됩니다.
  * "%" : 값에 100을 곱한 값이 표현됩니다.-->

### 예약어 사용 규칙
* `%`는 `#` 또는 `0`과 함께 사용해야 합니다.
  * #,##0.##%
* `%` 기호만 표시하고 싶을 경우 `\\`를 사용하여 escape 처리합니다.
   *  "#,###`\\`%"
* 예약어와 함께 일반 문자를 조합하여 사용할 수 있습니다.
  *  "#,###원" 또는 "$ #,##0.00"

### 값에 따라 다른 형식 표시
`;`(세미콜론)을 사용하면 **양수 / 음수 / 0 값에 따라 다른 포맷을 지정할 수 있습니다.**

#### Syntax
```javascript
   Format: "양수포맷;음수포맷;0포맷"
```

#### Example
```javascript
//열 설정
options.Cols = [
    {
       Name:"sNum",
       Type:"Int",
       // 양수이면 플러스 (값), 음수이면 마이너스 (값) 0은 없음 으로 표시
       Format:"플러스 #,###;마이너스 #,###;없음" 
        }
    ]

// 조회 데이터
{"Data":[
    { "sNum":1000}
]}
```
*실제 보여지는 데이터*<br>
![보여지는 데이터](/assets/imgs/intFormat.png "보여지는 데이터")

### Escape 문자
* 다음 문자는 예약 문자로 사용되므로 문자를 그대로 표시하려면 `\\`를 앞에 붙여야 합니다.
  *  '%', '_', 'e', '8', '?', '*', '@'
<!--
  %는 #또는 0과 같이 사용해야합니다. ex: "#,##0.##%"<br/>
  100을 곱한 계산값이 아닌 원래값의 뒤에 "%"기호만 추가하고자 하실 때는,`"#,###\\%"` 로 설정하시면 됩니다.<br>
  위의 예약어와 예약어를 제외한 문자를 조합해서 사용 가능합니다. ex:"$ #,##0.00"<br/>
`;(세미콜론)`으로 구분해서 값이 양수, 음수, 0일 때에 따라 화면에 보일 형식을 다르게 설정할 수 있습니다.<br>
<b>'_', 'e', '8', '?', '*' '@'에 해당하는 문자는 사용하시려면 반드시 문자 앞에 `"\\"`을 덧붙여주셔야 합니다. </b> <br>


  <mark>Type이 "Int"인 컬럼은 "#,##0", "Float"인 컬럼은 "#,##0.######"를 기본 포멧으로 갖습니다.</mark>
-->

### 참고 (자주 사용하는 숫자 Format)

|Format|데이터|표시 결과|
|---|---|---|
|#,###|1234|1,234|
|#,##0|1234|1,234|
|#,##0.00|1234.5|1,234.50|
|#,##0.###### \\\\%|0.150|0.15%|
|#,###원|1234|1,234원|

### 천 단위 구분자 / 소수점 구분자
천 단위 구분자(`GroupSeparator`)와 소수점 구분자(`DecimalSeparator`)는
메시지 파일(ko.js, en.js 등) 설정을 통해 변경할 수 있습니다.

<br><br><br><br>

---
<a id="html-format"></a>
## 4. 타입이 Html 인 경우
Html 타입에서는 **실제 값과 화면에 표시될 HTML 문자열을 매핑하여 표시할 수 있습니다.**

Format은 **JSON 형태로 실제 값(Key)과 화면에 표시될 값(Value)의 쌍으로 구성됩니다.**  
Text 타입의 **객체 방식 Format과 동일한 방식**으로 동작합니다.

### Syntax

```javascript
    // 객체 방식
    Format: {
      'Key1':'Value1', 
      'Key2':'Value2', 
      'key3':'Value3'
    }
```

|Value|Description|
|---|---|
|Key|셀의 실제 값(서버에서 조회되거나 저장시 서버로 전송됨)|
|Value|화면에 표시될 HTML 문자열|

### Example
```html
<style>
    .alertCircle{
        position:relative;
        left:30%;
        width:30px;
        height:25px; 
        border-radius:50px;
        color:#FFFFFF;
        line-height:25px;
        font-size:12px
    }
</style>

<script>
options.Cols = [
    {

        Name:"ALERT",
        Type:"Html",
        Width:80,
        Format:{
                "0":"<div class='alertCircle' style='background-color:#009688;'>안전</div>"
                ,"1":"<div class='alertCircle' style='background-color:#ff9800;'>주의</div>"
                ,"2":"<div class='alertCircle' style='background-color:#db4437;'>위험</div>"
            }
    }
 
]
</script>
```
|조회된 데이터|실제 보여지는 데이터|
|---|---|
|![조회데이터](/assets/imgs/htmlFormat1.png "조회 된 데이터")|![보여지는 데이터](/assets/imgs/htmlFormat2.png "보여지는 데이터")

<br><br><br><br>

---
<a id="link-format"></a>
## 5. 타입이 Link 인 경우
Link 타입에서는 **셀 값을 링크 형태로 표시할 수 있습니다.**  
Format을 사용하여 **실제 링크 URL과 화면에 표시될 HTML을 설정할 수 있습니다.**

### 1) 구분자 활용 방식
  * 첫 문자를 **구분자(delimiter)** 로 사용하여 설정 값을 나열하는 방식입니다.
  * 구분자는 반드시 `|`일 필요는 없으며 **첫 번째 문자가 구분자로 사용됩니다.**
  * 구분자로 사용된 문자는 설정 값 안에 포함될 수 없습니다.

#### Syntax
```javascript
    // 구분자 활용 방식 '|'이 구분자
    Format: "|UrlPrefix|UrlPostfix|HtmlPrefix|HtmlPostfix"
```

|Value|Description|
|---|---|
|UrlPrefix|실제 링크 url의 앞에 추가될 문자열|
|UrlPostfix|실제 링크 url의 뒤에 추가될 문자열|
|HtmlPrefix|화면에 표시될 링크 텍스트 앞에 추가될 HTML 코드|
|HtmlPostfix|화면에 표시될 링크 텍스트 뒤에 추가될 HTML 코드|

#### Example
```javascript
    options.Cols = [
        {
            Name:"sLink",
            Type:"Link",
            // 1. 링크 URL 앞에 추가될 문자열
            // 2. 링크 URL 뒤에 추가될 문자열
            // 3. 화면에 표시될 HTML 앞부분
            // 4. 화면에 표시될 HTML 뒷부분

            Format:"|/EMS/gm1/board.do?contents=|&group=USER4"
            +"|<img src='./assets/imgs/hot.svg' style='width:20px;height:20px;'>"
            +"|<img src='./assets/imgs/new.jpg' style='width:20px;height:20px;'>"
        }
    ]
```
조회된 데이터 ([Link 타입에 대한 데이터 구조 참고](./type))
```json
{"Data":[
    { "sLink":"|487141|Best way to save and edit text data without a database|_self "}
]}
```
|실제 보여지는 데이터|link 된 내용|
|---|---|
|![보여지는 데이터](/assets/imgs/linkFormat1.png "보여지는 데이터")|![보여지는 데이터](/assets/imgs/linkFormat2.png "보여지는 데이터")|


<br><br>

### 2) 객체 방식
 * 객체(JSON) 형태로 **옵션 이름과 값을 직접 지정하는 방식**입니다.

#### Syntax

```javascript
    // 객체 방식
    Format: {
        'UrlPrefix':'Value1', 
        'UrlPostfix':'Value2', 
        'HtmlPrefix':'Value3', 
        'HtmlPostfix':'Value4'
    }
```

|Value|Description|
|---|---|
|UrlPrefix|실제 링크 url의 앞에 추가될 문자열|
|UrlPostfix|실제 링크 url의 뒤에 추가될 문자열|
|HtmlPrefix|화면에 표시될 링크 텍스트 앞에 추가될 HTML 코드|
|HtmlPostfix|화면에 표시될 링크 텍스트 뒤에 추가될 HTML 코드|

#### Example
```javascript
    options.Cols = [
       {
           Name: "sLink",
           Type: "Link",
           Format: {
                    UrlPrefix:"/EMS/gm1/board.do?contents=",
                    UrlPostfix:"&group=USER4",
                    HtmlPrefix:"<img src='./assets/imgs/hot.svg' style='width:20px;height:20px;'>",
                    HtmlPostfix:"<img src='./assets/imgs/new.jpg' style='width:20px;height:20px;'>"
                },
        }
    ]
```
조회된 데이터 ([Link 타입에 대한 데이터 구조 참고](./type))
```json
{"Data":[
    { "LinkData":"|487141|Best way to save and edit text data without a database|_self " }
]}
```
|실제 보여지는 데이터|link 된 내용|
|---|---|
|![보여지는 데이터](/assets/imgs/linkFormat1.png "보여지는 데이터")|![보여지는 데이터](/assets/imgs/linkFormat2.png "보여지는 데이터")|


<br><br><br><br>

---

<a id="img-format"></a>
## 6. 타입이 Img 인 경우
Img 타입에서는 **셀에 이미지를 표시하거나 이미지 클릭 시 특정 링크로 이동하도록 설정할 수 있습니다.**  
Format을 사용하여 **이미지 경로, HTML 요소, 클릭 링크 등을 설정할 수 있습니다.**

### 1) 구분자 활용 방식
* 첫 문자를 **구분자(delimiter)** 로 사용하여 설정 값을 나열하는 방식입니다.
* 구분자는 반드시 `|`일 필요는 없으며 **첫 번째 문자가 구분자로 사용됩니다.**
* 구분자로 사용된 문자는 설정 값 안에 포함될 수 없습니다.

#### Syntax
```javascript
    // 구분자 활용 방식 '|'이 구분자
    Format: "|UrlPrefix|UrlPostfix|HtmlPrefix|HtmlPostfix|LinkPrefix|LinkPostfix"
```

|Value|Description|
|---|---|
|UrlPrefix|이미지 src 앞에 추가될 문자열|
|UrlPostfix|이미지 src 뒤에 추가될 문자열|
|HtmlPrefix|이미지 태그 앞에 추가될 HTML 코드|
|HtmlPostfix|이미지 태그 뒤에 추가될 HTML 코드|
|LinkPrefix|이미지 클릭 시 이동할 링크 앞에 추가될 URL|
|LinkPostfix|이미지 클릭 시 이동할 링크 뒤에 추가될 URL|

#### Example
```javascript
    options.Cols = [
        {
            Name: "sImg",
            Type: "Img",
            //1. img 태그의 src 값의 앞에 추가될 경로
            //2. img 태그의 src 값의 뒤에 추가될 경로
            //3. img 태그 앞에 넣고 싶은 text나 html
            //4. img 태그 뒤에 넣고 싶은 text나 html
            //5. 이미지를 클릭시 연결될 URL의 앞에 추가될 경로
            //6. 이미지를 클릭시 연결될 URL의 뒤에 추가될 경로
            Format: "|http://ibsheet.com/demo/images/icons/|.jpg|<button cls='imgMBtn'>|</button>|/EMS/gm1/board.do?contents=|&group=USER4"
        }
        
    ]
```
([Image 타입에 대한 데이터 구조 참고](./type))

<br><br>

### 2) 객체 방식
 * 객체(JSON) 형태로 `옵션 이름과 값을 직접 지정하는 방식`입니다.

#### Syntax

```javascript
    // 객체 방식
    Format: {
        'UrlPrefix':'Value1', 
        'UrlPostfix':'Value2', 
        'HtmlPrefix':'Value3', 
        'HtmlPostfix':'Value4', 
        'LinkPrefix':'Value5', 
        'LinkPostfix':'Value6'
    }
```

|Value|Description|
|---|---|
|UrlPrefix|이미지 src 앞에 추가될 문자열|
|UrlPostfix|이미지 src 뒤에 추가될 문자열|
|HtmlPrefix|이미지 태그 앞에 추가될 HTML 코드|
|HtmlPostfix|이미지 태그 뒤에 추가될 HTML 코드|
|LinkPrefix|이미지 클릭 시 이동할 링크 앞에 추가될 URL|
|LinkPostfix|이미지 클릭 시 이동할 링크 뒤에 추가될 URL|

### Example
```javascript
    options.Cols = [
       {
           Name: "sImg",
           Type: "Img",
           Format: { 
                    UrlPrefix: "http://ibsheet.com/demo/images/icons/", 
                    UrlPostfix: ".jpg",
                    HtmlPrefix: "<button cls='imgMBtn'>", 
                    HtmlPostfix: "</button>",
                    LinkPrefix: "/EMS/gm1/board.do?contents=",
                    LinkPostfix: "&group=USER4"
           }
        }
       
    ]
```
<br><br><br><br>

---

<a id="file-format"></a>
## 7. 타입이 File 인 경우

File 타입에서는 `Format` 속성을 사용하여 업로드된 파일 이름이나 이미지 미리보기(thumbnail)를 표시할 수 있습니다.

### Syntax

```javascript
Format: "*Name* <img src='*Url*'>"
```

|값|설명|
|---|---|
|*Name*|파일 이름|
|*Url*|업로드된 파일의 URL (이미지 미리보기 등에 사용)|

※ 서버에 저장된 파일을 표시하려면 셀의 [Path](/docs/props/cell/path) 속성 또는 [Export.FilePath](/docs/props/cfg/export) 설정을 통해 파일 경로가 지정되어 있어야 합니다.

### Example
```javascript
//컬럼 설정
options.Cols = [
    {
        Name: "attach",
        Type: "File",
        Accept: "image/*", //업로드를 허용할 파일 형식을 지정
        Format: "*Name* <br> <img src='*Url*' height='200' width='200'>"
    }
]

//조회 데이터
{"Data":[
    {
     "attach":"image.png", //파일명
     "attachPath":"https://demo.ibsheet.com/ibsheet/v8/samples/customer-sample/assets/imgs/" //파일위치
    }
]}

```

### Read More
- [Type appendix](./type)
- [CustomFormat col](/docs/props/col/custom-format)
- [DataFormat col](/docs/props/col/data-format)
- [EditFormat col](/docs/props/col/edit-format)
- [Format col](/docs/props/col/format)
- [Path cell](/docs/props/cell/path) 
- [Export cfg](/docs/props/cfg/export)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.2.0.9|File 타입 Format 기능 추가|

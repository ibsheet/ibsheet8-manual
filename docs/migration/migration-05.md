# 마이그레이션 차이점/유의사항

## 5. 마이그레이션시 차이점,유의사항 <a name="chapter-5"></a>

1. 객체 접근,렌더링 시점 변화 <a name="mig-approach"></a>
IBSheet8에서는 기존 버전의 제품과 달리 시트 내부의 각 객체에 직접 접근하여 값을 확인하거나 수정하는 방식으로 변경되었습니다.<br/>
또한 각 함수의 수행 후에 즉시 렌더링이 일어나던 IBSheet7과 달리 렌더링이 필요한 순간 렌더링 함수를 호출하여 실제 화면에 반영하는 방식으로 루프를 돌면서 하는 작업들에 있어서 성능이 개선되었습니다.<br/>
아래 예제는 "TOTAL"라는 열에 대해 전체 데이터를 확인하여 열의 값이 100보다 큰 경우, 해당 셀의 배경색을 붉은색으로 표시하게 끔 로직을 구성하는 예제를 참고해 주세요.<br/>

```javascript
//AS-IS
//첫번째 데이터 행부터 마지막 데이터 행까지 루프를 돈다.
for (var i = sheet.GetDataFirstRow(); i <= sheet.GetDataLastRow(); i++) {
    if (sheet.GetCellValue(i,"TOTAL") > 100){ //셀 내의 값을 clone해서 가져옴.
        sheet.SetCellBackColor(i,"TOTAL", "#FF0000"); //해당 셀에 배경색을 붉은색으로 변경한다. (함수 호출시마다 렌더링이 발생함.)
    }
}
```

```javascript
//TO-BE
//전체 데이터행 객체를 배열로 얻음
var rows = sheet.getDataRows();
for (var i = 0; i < rows.length; i++) {
    //한 행 객체를 얻음
    var row = rows[i];
    //row 객체 내에서 값을 비교하고 설정한다.
    //이렇게 수정해도 실제 화면에 반영(렌더링)되지는 않는다.
    if (sheet.getValue(row, "TOTAL") > 100) {
        sheet.setAttribute(row, "TOTAL", "Color", "#FF0000", 0);//render 속성을 0
    }
}
//전체 수정된 내용을 화면에 반영
sheet.renderBody();
```
IBSheet7의 경우 빈번한 렌더링 발생과 값에 대한 핸들링 방식의 차이로 인해 성능을 저해해 왔습니다.<br/>
IBSheet8에서는 객체에 대한 직접 접근 및 렌더링 시점 조절을 통해 이러한 작업에 있어서 강점이 있습니다.<br/>
실제로 위 예제는 IBSheet7과의 로직 차이를 설명하기 위해 작성된 것으로 IBSheet8에 [Formula](./formula) 기능을 이용하면 보다 간단하고 빠르게 해당 기능을 구현하실 수 있습니다.

2. Tree(트리)데이터 파싱 <a name="mig-parse-tree-data"></a>
IBSheet7에서는 트리를 사용하는 경우 두가지 데이터 구조를 지원하였습니다.

1) `Items` 속성을 이용한 단계적인 구조 트리 데이터
```javascript
{Data:[
    {ID:1,sName:"할아버지",Items:[
        {ID:2,sName:"큰아버지"},
        {ID:3,sName:"아버지",Items:[
            {ID:5,sName:"형"},
            {ID:6,sName:"나"}
        ]},
        {ID:4,sName:"작은아버지"}
    ]}
]}
```
2) `Level` 속성을 이용한 Depth지정 트리 데이터
```javascript
{Data:[
    {ID:1 ,Level:1,sName:"할아버지"},
    {ID:2 ,Level:2,sName:"큰아버지"},
    {ID:3 ,Level:2,sName:"아버지"},
    {ID:5 ,Level:3,sName:"형"},
    {ID:6 ,Level:3,sName:"나"},
    {ID:4 ,Level:2,sName:"작은 아버지"},
]}
```

IBSheet8에서는 기본적으로 위에 1) `Items` 속성을 이용한 트리데이터 구조를 지원합니다.
그리고 이전과 마찬가지로 `Level` 속성을 이용한 파싱을 사용하시려면 `ibsheet-common.js` 안에 `v7.convertTreeData` 함수를 이용하여야 합니다.

**`IBSheet.v7`에 정의된 API는 시트 객체를 바인딩해줘야합니다.**

```javascript
// IBSheet7의 Level 데이터 구조를 변경해 줌.
sheet.loadSearchData( IBSheet.v7.convertTreeData(jsonData) );
```

# Menu ***(appendix)***
> 마우스 우측 버튼 클릭 시 보여지는 컨텍스트 메뉴를 설정합니다.  
> 항목을 구분자로 나열한 **문자열**(ex: `"|저장|취소|미리보기"`)로 간단히 만들거나, 체크박스, 버튼, 트리 등 복잡한 구조가 필요하면 **객체(object)**로 설정합니다.  
> 이 문서는 **객체(object) 메뉴** 설정을 다룹니다. 간단한 문자열 메뉴는 각 영역의 Menu 속성 문서([Cfg](/docs/props/cfg/menu) / [Col](/docs/props/col/menu) / [Row](/docs/props/row/menu) / [Cell](/docs/props/cell/menu))를 참고하세요.

## Menu 속성
Menu 객체는 **메뉴 전체에 적용하는 속성**(`Items`, `Buttons` 등)과, `Items`에 담기는 **각 항목(Item)에 적용하는 속성**(`Name`, `Bool`, `Value` 등)으로 구성됩니다. 아래에서 각각 다룹니다.

### 1. 메뉴 전체에 적용하는 속성
|Name|Type|Description|
|---|---|---|
|*Items*|`array[object]`|메뉴 항목들을 배열로 설정합니다.<br/>각 항목 속성은 아래 **2. 각 항목(Item)에 적용하는 속성** 참고.|
|*Default*|`object`|Items 배열 내에 설정된 모든 하위 아이템 객체에 공통으로 적용해야 할 내용을 설정합니다.<br/>ex)<br/> //하위 아이템들을 체크박스 형식으로 설정<br/>Default:{ Bool:1 },   Items:[{}, {}, {}] |
|*Buttons*|`array[string]`|메뉴 하단에 표시될 버튼을 배열로 설정합니다. <br/>설정할 수 있는 버튼은 다음과 같습니다.<br/>"Ok":선택한 값을 리턴<br/>"Clear":Bool속성 사용하는 아이템에 대해 전체 선택 혹은 선택 취소<br/>"Cancel":선택값을 무시하고 메뉴 닫기<br/>ex)<br/>"Buttons":[ "Ok", "Cancel" ]|
|*SaveType*|`number`|여러 아이템을 선택하거나 수정한 뒤 확인(Ok) 버튼을 눌러 확정할 때,<br/>최종 결과로 전달되는 값의 형식을 설정합니다. (`Buttons`에 `"Ok"`를 설정해야 하며, 확정 결과는 `OnSave`의 `data` 인자로 전달)<br/>설정에 따라 리턴되는 값은 다음과 같습니다.<br/>0 : 빈값이 아닌 아이템만 리턴됩니다. Bool속성을 사용하는 아이템은 체크된 경우 Name속성이 리턴되며, 편집 가능한 타입의 아이템은 Name:Value형태로 리턴됩니다.<br/>1 : 수정된 아이템들만 리턴됩니다. Bool속성을 사용하는 아이템은 Name: 0, Name: 1 형태로 리턴되며, 편집 가능한 타입의 아이템은  Name: Value 형태로 리턴됩니다.<br/>2 : 모든 값들이 리턴됩니다. Bool속성을 사용하는 아이템은 Name: 0, Name: 1 형태로 리턴되며, 편집 가능한 타입의 아이템은 Name: Value 형태로 리턴됩니다.<br/>3 : 모든 값들이 리턴됩니다. Bool속성을 사용하는 아이템은  0/1 형태로 리턴되며, 편집 가능한 타입의 아이템은 Value 만 리턴됩니다.<br/>4 : 모든 값들이 리턴됩니다. Bool속성을 사용하는 아이템은  0/1 대신 체크해제는 ""(공백)/체크는 Name이 리턴되며, 편집 가능한 타입의 아이템은 Value 만 리턴됩니다.<br/>(default:0)|
|*ExpandTime*|`number`|Level속성을 통해 하위 아이템을 트리 형식으로 표현할 때 상위 아이템에 마우스 호버 시 설정된 시간(ms단위) 이후에 자동으로 하위 아이템 메뉴가 펼쳐집니다.<br/>0으로 설정 시 항상 하위 아이템 메뉴가 펼쳐진 상태로 보여지며 접기 위한 아이콘도 표시되지 않습니다. (default:200)|
|*CollapseOther*|`boolean`|트리 형식 사용 시 사용자가 어떤 상위 아이템을 클릭하여 하위 아이템 메뉴가 보여지도록 펼치면, 자동으로 기존에 펼쳐져 있던 다른 상위 아이템의 하위 아이템 메뉴를 접게 합니다. (default:1)|
<!-- ShowHint: 동작/기본값 실측 미확인 (문서화된 속성만으로 재현 불가) — 개발팀 확인 후 복원
|*ShowHint*|`boolean`|메뉴 크기가 작아서 일부 내용이 안 보이는 경우, 마우스 커서 호버 시 해당 아이템의 너비를 늘려 가려진 부분을 보여줍니다.|
-->


### 2. 각 항목(Item)에 적용하는 속성
|Name|Type|Description|
|---|---|---|
|*Name*<br/>**필수**|`string`|각 아이템의 이름을 설정합니다. <br/>Text속성을 설정하지 않는 경우 Name으로 설정한 값이 아이템 리스트에 보여집니다.<br/>Value속성이 설정되지 않는 경우 Name으로 설정한 값이 전달됩니다.<br/> Name은 아이템 별로 고유해야 합니다.<br/> 메뉴 사이에 구분선이 필요한 경우 `{Name: "-"}` 를 추가합니다.|
|*Text*|`string`|메뉴에 보여질 아이템 텍스트를 설정합니다. <br/>Text속성을 설정하지 않는 경우 Name으로 설정한 값이 아이템 리스트에 보여집니다.|
|*Value*|`string`|특정 아이템을 선택시 전달할 값을 설정합니다.<br/>Value속성이 설정되지 않는 경우 Name으로 설정한 값이 전달됩니다.<br/>다만 Bool:1 로 각 아이템에 체크박스를 두는 경우에는 용도가 완전히 달라져서 체크박스에 대한 초기 선택 여부로 사용됩니다.|
|*Icon*|`string`|아이템 텍스트 왼쪽에 보여질 아이콘의 url을 설정합니다.|
|*IconWidth*|`number`|아이콘 객체의 너비를 설정합니다.|
|*LeftHtml*|`string`|아이템 텍스트 왼쪽에 원하는 HTML객체를 넣습니다.|
|*LeftWidth*|`number`|왼쪽 HTML객체의 너비를 설정합니다.|
|*RightHtml*|`string`|아이템 텍스트 오른쪽에 원하는 HTML객체를 넣습니다.|
|*RightWidth*|`number`|오른쪽 HTML객체의 너비를 설정합니다.|
|*Height*|`number`|아이템 객체의 최소 높이를 설정합니다.(설정하지 않는 경우 내용의 높이에 따라 자동 결정됩니다.)|
|*Hidden*|`boolean`|특정 아이템 객체의 감춤 여부를 설정합니다. <br/>아이템이 자식 메뉴를 갖고 있는 경우, 자식도 모두 숨겨집니다.|
|*Disabled*|`boolean`|특정 아이템을 비활성화 합니다. <br/>아이템이 보이지만 선택이 불가능한 상태가 됩니다.|
|*Default*|`object`|Items 배열 내에 설정된 모든 하위 아이템 객체에 공통으로 적용해야 할 내용을 설정합니다.<br/>ex)<br/> //하위 아이템들에게 동일한 Icon을 적용한다.<br/>Default:{ Icon:"./image/icon/bt.gif", IconWidth:24 },   Items:[{},{},{}] |
|*Caption*|`boolean`|특정 아이템을 머릿말로 사용합니다.<br/>이 기능을 설정시 해당아이템은 선택되지 않습니다.<br/><pre>Menu:{<br/>  Items:[<br/>    {Name:"N1",Text:"연령별",Caption:1},<br/>    {Name:"N2",Text:"경행대"},<br/>    {Name:"N3",Text:"성인"},<br/>    {Name:"N4",Text:"청소년"},<br/>    {Name:"N5",Text:"어린이"}<br/>  ] <br/>}</pre><br/>![Caption](/assets/imgs/menuCaption.png "Caption")|
|*Items*|`array[object]`|특정 아이템 아래 하위 아이템 객체를 설정합니다.|
|*Level*|`boolean`|하위 아이템 객체들을 Tree 형식으로 표현합니다.<br/>![Level](/assets/imgs/menuLevel.png "Level")|
|*Expanded*|`number`|Level속성을 통해 아이템을 Tree 형식으로 표현할때 아이템의 펼침 여부를 설정합니다.<br/>-1 : 펼쳐져 있고 닫기 불가<br/>1 : 펼쳐져 있고 닫기 가능<br/>0 : 닫혀 있음<br/><b>이 속성은 상위의 CollapseOther 나 ExpandTime 속성에 영향을 받습니다.</b>|
|*Menu*|`boolean`|하위 아이템 객체들을 부모아이템 우측에 메뉴 형식으로 표현합니다.<br/>![Menu](/assets/imgs/menuMenu.png "Menu")|
|*Columns*|`number`|하위 아이템 객체를 여러 개 열로 나누어 표현합니다.<br/><pre>Menu:{<br/>  Items:[<br/>    {<br/>      Columns:2,<br/>      Items:[<br/>        {Name:"안보전략"},<br/>        {Name:"군사발전"},<br/>        {Name:"국방자원"}<br/>      ] <br/>    }<br/>  ]<br/>}</pre><br/>![Columns](/assets/imgs/menuColumns.png "Columns")|
|*ColumnSizes*|`string`|열당 들어갈 아이템 개수를 ","를 구분자로 설정합니다.<br/>가령 Columns:3 이고 ColumnSizes:"3,2,4"인 경우, 다음과 같이 표시됩니다.<br/>![ColumnSizes](/assets/imgs/menuColumnSizes.png "ColumnSizes")|
|*Bool*|`boolean`|아이템 텍스트 우측에 체크박스를 표시합니다.<br/>이 속성이 적용된 아이템은 클릭 시 체크박스의 값이 변경됩니다.<br/>체크된 전체 아이템은 `Buttons`에 `"Ok"`를 설정해 확정하면 `OnSave`의 `data`로 전달됩니다.<br/>![Bool](/assets/imgs/menuBool.png "Bool")|
|*Group*|`number`|Bool속성을 사용하는 아이템들 간에 Radio 그룹을 형성하여 같은 그룹 내에서는 하나의 아이템만 선택가능하게 합니다.<br/>Group의 값은 1이상의 숫자로 설정할 수 있습니다.|
|*UnCheck*|`boolean`|Group 속성을 사용하는 아이템에서 Radio에 대한 선택을 해제할 수 있는지 여부를 설정합니다.|
|*GroupAll*<br/>*CheckAll*|`number`<br/>`boolean`|Bool 속성을 사용하는 아이템들 중에서 같은 GroupAll 속성값을 갖는 아이템들은 CheckAll설정이 되어있는 아이템이 체크될때 같이 체크 됩니다.<pre>//과일전체 아이템 선택시 사과,배,오렌지 아이템도 선택됩니다.<br/>Menu:{<br/>  Items:[<br/>    {Name:"과일전체",Bool:1,GroupAll:200,CheckAll:1},<br/>    {Name:"사과",Bool:1,GroupAll:200},<br/>    {Name:"배",Bool:1,GroupAll:200},<br/>    {Name:"오렌지",Bool:1,GroupAll:200},<br/>  ] <br/>}</pre>|
|*NoAll*|`boolean`|설정한 아이템은 "전체취소(Clear)/전체선택(All)"버튼의 영향을 받지 않게 됩니다.|
|*Enum*|`boolean`|하위 아이템을 부모아이템 우측에 콤보 형태로 표현할지 여부를 설정합니다.<br/>![Enum](/assets/imgs/menuEnum.png "Enum")|
|*Edit*|`boolean`|아이템 텍스트 우측에 편집 가능한 input 객체를 표시합니다.<br/>{Name:"이름",Edit:1,Width:150} 설정 시<br/>![Edit](/assets/imgs/menuEdit.png "Edit")|
|*Width*|`number`|Enum속성 사용시 콤보 박스의 너비를 설정합니다.<br/>Edit 속성 사용시 input 객체의 너비를 설정합니다.|
|*Left*|`boolean`|Bool속성 사용시 체크박스를 왼쪽에 위치시킵니다.<br/>Enum속성을 사용시 콤보박스를 왼쪽에 위치시킵니다.<br/>Edit속성을 사용시 input 객체를 왼쪽에 위치시킵니다.|

위 속성을 사용한 **체크박스형 메뉴** 예입니다. 아이템에 `Bool:1`을 주면 체크박스가 표시되어 여러 항목을 동시에 선택할 수 있고, `Value`는 초기 체크 상태(`1`=체크, `0`=해제)입니다. `Ok`를 누르면 `OnSave`의 `data`에 체크된 항목 이름 배열이 전달됩니다.

```js
  {
    "Menu":{
      "Buttons":[ "Ok", "Cancel" ],
      "Items":[
        {"Name":"미국","Value":1,"Bool":1},
        {"Name":"일본","Value":0,"Bool":1},
        {"Name":"중국","Value":0,"Bool":1},
        {"Name":"북한","Value":1,"Bool":1}
      ],
      "OnSave":function(item,data) {
        // this.Sheet / this.Row / this.Col 로 메뉴가 열린 위치 접근 가능
        alert("["+data.join(",")+"]를 선택하셨습니다.");
      }
    }
  }
```
![메뉴기능](/assets/imgs/menuBasic.png)

---

## Menu 이벤트
전역으로 발생하는 onShowMenu나 onSelectMenu 이벤트 외에 메뉴별로 각각 이벤트를 설정할 수 있습니다.
메뉴에 설정되는 이벤트도 속성과 마찬가지로 전역 이벤트와 특정 아이템에 설정하는 이벤트로 나뉩니다.

이벤트 콜백 안에서 `this`(메뉴 또는 아이템 객체)를 사용하려면, 화살표 함수 대신 일반 함수(`function(){}`)로 작성하세요. 화살표 함수는 `this`가 바뀝니다.

### 1. 메뉴 전체 이벤트

#### OnSave
메뉴에서 선택을 확정했을 때 발생합니다. (메뉴가 닫힌 뒤 발생)

- 항목을 **바로 클릭**하면 결과가 **`item`** 으로 넘어옵니다.
- 체크박스(Bool)나 편집(Edit)을 쓰고 하단 **`Ok` 버튼**(`Buttons`에 `"Ok"` 지정)을 누르면 결과가 **`data`** 로 넘어옵니다.

|파라미터|유형|설명|
|---|---|---|
|item|`object`|클릭한 메뉴 아이템 객체 (`item.Name`, `item.Value`). `Ok` 버튼을 누른 경우에는 `undefined`|
|data|`array`|`Ok` 버튼을 누른 경우 선택한 값들의 배열 (`SaveType` 형식). 항목을 바로 클릭한 경우에는 `[]`|

`this`는 **메뉴 객체**라 `this.Sheet` / `this.Row` / `this.Col`로 메뉴가 열린 시트, 행, 열에 접근할 수 있습니다.

일반 항목을 클릭하면 전역 `onSelectMenu` 이벤트도 함께 발생하므로, 둘 중 하나에서만 처리하세요. ([onSelectMenu](/docs/events/on-select-menu) 참고)

#### OnButton
하단 버튼을 클릭할 때 발생합니다. (`OnSave`보다 먼저 발생하며, `false`를 리턴하면 이후 처리를 막습니다.)

|파라미터|유형|설명|
|---|---|---|
|button|`string`|눌린 버튼 문자열 (`"Ok"`, `"Cancel"`). `Buttons`의 `"Clear"` 버튼은 전체선택/해제 토글이라, 동작에 따라 `"All"`(전체선택) 또는 `"Clear"`(전체해제)로 전달됩니다.|

`this`는 **메뉴 객체**라 `this.Sheet` / `this.Row` / `this.Col`로 메뉴가 열린 시트, 행, 열에 접근할 수 있습니다.

```js
Menu: {
  Buttons: ["Ok", "Clear", "Cancel"],
  Items: [ { Name: "월요일", Bool: 1 }, { Name: "화요일", Bool: 1 } ],
  OnButton: function (button) {
    // button 값: "Ok" / "Cancel" / "All"(전체선택) / "Clear"(전체해제)
    if (button === "Ok") {
      // 확인 버튼 후처리 ...
    }
    // 필요 시 false를 리턴하면 해당 버튼의 기본 후처리를 막습니다.
  }
}
```

### 2. 아이템 개별 이벤트
#### OnClick
특정 아이템을 클릭할 때 발생합니다. 리턴값으로 이후 동작을 제어합니다.
- `false` : 기본 동작을 실행하지 않고 메뉴를 계속 엽니다.
- `true` : 기본 동작을 실행하지 않고 메뉴를 닫습니다.
- `null` (또는 리턴 없음) : 기본 동작(아이템 선택)을 실행합니다.

|파라미터|유형|설명|
|---|---|---|
|menu|`object`|메뉴 객체|
|item|`object`|클릭한 아이템 객체|

`this`는 **클릭한 아이템**입니다. `this.Name`으로 이름, `this.Owner`로 메뉴 객체, `this.Parent`로 부모 아이템이나 메뉴에 접근합니다. 메뉴가 열린 시트, 행, 열은 `this.Owner.Sheet` / `this.Owner.Row` / `this.Owner.Col`로 접근할 수 있습니다.

```js
Menu: {
  Items: [
    { Name: "새로고침",
      OnClick: function (menu, item) {   // this = 클릭한 아이템
        var sheet = this.Owner.Sheet;
        var row   = this.Owner.Row;      // 메뉴가 열린 행
        // ... row/sheet 로 원하는 처리 ...
        return true;   // 기본 동작 없이 메뉴 닫기 (false=계속 열림, null=기본 선택)
      }
    }
  ]
}
```

#### OnChanged
수정 가능한 아이템(`Bool`, `Enum`, `Edit`)의 값이 바뀔 때, 값이 적용되기 전에 발생합니다.

|파라미터|유형|설명|
|---|---|---|
|value|`mixed`|변경될 새 값|

`this`는 **해당 아이템**입니다. `this.Value`는 변경 전 값, `this.Name`은 이름이며, 메뉴가 열린 시트, 행, 열은 `this.Owner.Sheet` / `this.Owner.Row` / `this.Owner.Col`로 접근합니다.
새 값을 적용하려면 그 값을 리턴하고, 변경을 취소하려면 `this.Value`(이전 값)를 리턴합니다.

```js
Menu: {
  Items: [
    { Name: "사용여부", Bool: 1, Value: 0,
      OnChanged: function (value) {   // this = 해당 아이템, value = 변경될 새 값
        // this.Value = 변경 전 값
        return value;   // 새 값 적용 (변경을 취소하려면 this.Value 리턴)
      }
    }
  ]
}
```

---

## Example
```js
{
  Menu:{
    Buttons:["Ok","Cancel"],
    Items:[
      {
      Menu:1,
      Name:"과일",
        Items:[
          {Name:"과일이름",Caption:1},
          {Name:"사과",Bool:1},
          {Name:"배",Bool:1},
          {Name:"오렌지",Bool:1}
        ]
      },
      {
        Enum:1,
        Name:"채소",
        Items:[
          {Name:"당근"},
          {Name:"오이"},
          {Name:"가지"},
          {Name:"토마토"}
        ]
      },
      {
        Level:1,
        Expanded:1,
        Default:{OnClick:ItemClickHandler},
        Name:"나물",
        Items:[
          {Name:"도라지"},
          {Name:"더덕"},
          {Name:"미나리"}
        ]
      }
    ],
    OnButton:function(button){
      if(button == "Cancel"){
        if(!confirm("정말로 취소하시겠습니까?")){
          return false;
        }
      }
    }
  }
}
```   
![Menu](/assets/imgs/menu.png "Menu")


### Read More
- [Menu row](/docs/props/row/menu)
- [EnumMenu col](/docs/props/col/enum-menu)
- [Menu col](/docs/props/col/menu)
- [Menu cell](/docs/props/cell/menu)
- [onSelectMenu event](/docs/events/on-select-menu)
- [onShowMenu event](/docs/events/on-show-menu)
- [showMenu static](/docs/static/show-menu)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|

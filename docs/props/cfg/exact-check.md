# ExactCheck ***(cfg)***

<!-- synonyms: 체크박스 정확 클릭, 셀 빈 공간 체크 방지, 체크 정확도, exact check -->

> `Bool`, `Radio` 타입 컬럼에서 체크박스/라디오 버튼이 아닌 셀의 빈 공간을 클릭해도 체크/체크해제되지 않도록 설정합니다.  
> `Type:"Radio"`로 설정하고 `Enum`도 함께 설정한 컬럼은 라디오 버튼과 항목명 텍스트가 한 단위로 표시되므로 `ExactCheck` 설정이 동작하지 않습니다.  
> [HeaderCheck](/docs/props/cfg/header-check)로 표시되는 헤더 전체 체크박스에도 적용되며, 이때는 `"Header": {"Value": "", "IconAlign": "Center"}`처럼 **헤더 텍스트(`Value`)를 비우고 아이콘 정렬(`IconAlign`)을 `"Center"`로 반드시 설정**해야 합니다.  
> 텍스트가 있거나 아이콘 정렬이 가운데가 아니면 헤더 전체 체크박스가 동작하지 않습니다.


### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|셀의 빈 공간 클릭으로도 체크/체크해제 가능 (`default`)|
|`1(true)`|체크박스/라디오 버튼 클릭으로만 체크/체크해제 가능|


### Example
```javascript
options.Cfg = {
    ExactCheck: true        // 체크박스 클릭에만 체크/체크해제가 동작
};
```

### Read More
- [HeaderCheck cfg](./header-check)
- [HeaderCheck col](/docs/props/col/header-check)
- [Type appendix](/docs/appx/type)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.19|기능 추가|
|core|8.1.0.6|헤더 체크 기능 적용|

# Visible ***(col)***

<!-- synonyms: 열 보임, 열 감춤, 컬럼 숨김, 컬럼 표시, showCol hideCol, visible, hidden, column visibility, show hide column -->

> 열의 보임 감춤/여부를 설정합니다.
>
> 시트 생성시 `Visible:0`으로 설정 후, 나중에 컬럼에 보여주고자 할때는 `setAttribute()`를 통해 속성값을 변경하기 보다는, [showCol()](/docs/funcs/core/show-col)함수를 사용하시기 바랍니다.

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|열 감춤|
|`1(true)`|열 보임 (`default`)|

### Example
```javascript
//특정 열를 감춤
options.Cols = [
    ...
    {Type: "Int", Name: "Pvt_TSum", Visible: 0, ...},
    ...
];
```

### Read More
- [showCol method](/docs/funcs/core/show-col)
- [hideCol method](/docs/funcs/core/hide-col)
- [onShowCol event](/docs/events/on-show-col)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|

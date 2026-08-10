# onAfterColAdd ***(event)***

<!-- synonyms: 열 추가 후, 컬럼 추가 완료, 컬럼 생성 후, addCol 이후, on-after-col-add, after column add, column added -->

> 시트에 새로운 열이 추가되어 렌더링된 후 호출되는 이벤트입니다.

### Syntax

```
    onAfterColAdd : function(paramObject) {

    }
or
    sheet.bind("onAfterColAdd" , function(paramObject) {});
```

### Parameters
| Name | Type | Description |
|----------|-----|-------|
|sheet|`object`|시트 객체|
|col|`string`|시트에 추가된 열이름|

### Return
***none***

### Example
```javascript
options.Events = {
    onAfterColAdd:function(evtParam){
        console.log(evtParam.col);
    }
}
```

### Read More

- [addCol method](/docs/funcs/core/add-col)

### Since

|product|version|desc|
|---|---|---|
|core|8.2.0.12|기능 추가|

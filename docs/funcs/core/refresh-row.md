# refreshRow ***(method)***
> 특정 행의 변경된 내용을 화면에 반영합니다.
>
> 반영이 이루어질 때 화면이 깜빡이지 않습니다.

### Syntax
```javascript
void refreshRow( row );
```

### Parameters

|Name|Type|Required| Description |
|----------|-----|---|----|
|row |`object`|<span class='required'>필수</span>|[데이터 로우 객체](/docs/appx/row-object)|

### Return Value
***none***

### Example
```javascript
//특정 행에 변경된 내용(값,속성)을 화면에 반영한다.
sheet.refreshRow( row );
```

### Read More

- [refreshCell method](./refresh-cell)
- [rerender method](./rerender)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|

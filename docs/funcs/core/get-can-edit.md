# getCanEdit ***(method)***

> 특정 셀에 적용된 `CanEdit` 값을 확인합니다.  
> `Cell`, `Row`, `Col`, `Cfg` 설정이 모두 반영된 **최종 적용 상태**를 반환합니다.  

### Syntax
```javascript
number getCanEdit( row, col );
```

### Parameters

|Name|Type|Required|Description|
|----------|-----|---|----|
|row |`object`|<span class='required'>필수</span>|[데이터 로우 객체](/docs/appx/row-object)|
|col|`string`|<span class='required'>필수</span>|열이름|

### Return Value
***number***

|value|설명|
|-----|-----|
|`0`|편집 불가(읽기 전용)<br/>![CanEdit](/assets/imgs/canEdit0.png "CanEdit")|
|`1`|편집 가능<br/>![CanEdit](/assets/imgs/canEdit1.png "CanEdit")|
|`2`|편집 불가 + 편집 미리보기 제공<br/>![CanEdit](/assets/imgs/canEdit2.png "CanEdit")|
|`3`|편집 불가 + 배경색 표시 없음|
|`4`|편집 불가 + 배경색 표시 없음 + 아이콘 표시|

### Example
```javascript
//특정 셀에 편집 가능 여부를 확인.
var edit = sheet.getCanEdit(sheet.getFocusedRow(), "RES_ENDDATE");
if (edit === 0) {
    alert("마감되었습니다");
}
```

### Read More
- [CanEdit cell](/docs/props/cell/can-edit)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|

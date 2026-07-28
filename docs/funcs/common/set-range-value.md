# setRangeValue ***(method)***

> setValue, 혹은 setString를 이용하여 범위 내의 셀 값을 일괄적으로 변경합니다. 

### Syntax
```javascript
void setRangeValue( val, startRow, startCol, endRow, endCol, colSeparator, rowSeparator, type );
```

### Parameters

|Name|Type|Required|Description|
|----------|-----|---|----|
|val|`mixed`|<span class='optional'>선택</span>|설정하고자 하는 값|
|startRow|`object`|<span class='optional'>선택</span>|값 일괄 변경 시작 데이터 로우 객체|
|startCol|`object`|<span class='optional'>선택</span>|값 일괄 변경 시작 열이름|
|endRow|`object`|<span class='optional'>선택</span>|값 일괄 변경 종료 데이터 로우 객체|
|endCol|`object`|<span class='optional'>선택</span>|값 일괄 변경 종료 열이름|
|colSeparator|`object`|<span class='optional'>선택</span>|컬럼 구분자 사용시 사용할 컬럼 구분자|
|rowSeparator|`object`|<span class='optional'>선택</span>|행 구분자 사용시 사용할 행 구분자|
|type|`object`|<span class='optional'>선택</span>|setValue를 사용할지, setString을 사용할지 여부 1: setValue 사용 2: setString 사용|

### Return Value
***none***

### Example
```javascript
// AR1행 ~ AR3행, Col1 ~ Col2 열 범주 셀의 TextColor 값을 '사과'로 일괄 변경합니다.
sheet.setRangeValue("사과", sheet.getRowById("AR1"), "Col1", sheet.getRowById("AR3"), "Col2",);
```

### Read More

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|

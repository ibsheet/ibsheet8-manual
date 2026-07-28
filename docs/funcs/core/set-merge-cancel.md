# setMergeCancel ***(method)***
> 특정 셀의 병합을 해제합니다.  
> [SearchMode](/docs/props/cfg/search-mode):0에서는 스크롤 시 병합 상태가 유지되지 않아 정상 지원되지 않습니다.

### Syntax
```javascript
void setMergeCancel( row, col );
```

### Parameters
|Name|Type|Required| Description |
|----------|-----|---|----|
|row |`object`|<span class='required'>필수</span>|병합 된 [데이터 로우 객체](/docs/appx/row-object)|
|col |`string`|<span class='required'>필수</span>|병합 된 열이름|


### Return Value
***none***

### Example
```javascript
//병합된 셀을 다시 분리(split) 함
sheet.setMergeCancel( sheet.getRowById("AR2"), "deptCd");
```

### Read More
- [setMergeRange method](./set-merge-range)
- [setAutoMergeCancel method](./set-auto-merge-cancel)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|

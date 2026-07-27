# setMergeRange ***(method)***
> 특정 영역을 하나의 셀로 병합(`span`)합니다.  
> 시작셀(`row1, col1`)부터 종료셀(`row2, col2`)까지를 사각형 형태로 병합합니다.  
> `row2`는 반드시 `row1`보다 아래, `col2`는 반드시 `col1`보다 우측에 위치해야 합니다.  
> [SearchMode](/docs/props/cfg/search-mode):0에서는 스크롤 시 병합 상태가 유지되지 않아 정상 지원되지 않습니다.

### 동작 이미지
![병합](/assets/imgs/setMergeRange.png)


### Syntax
```javascript
void setMergeRange( row1, col1, row2, col2 );
```

### Parameters
|Name|Type|Required| Description |
|----------|-----|---|----|
|row1 |`object`|<span class='required'>필수</span>|병합시작 [데이터 로우 객체](/docs/appx/row-object)|
|col1 |`string`|<span class='required'>필수</span>|병합시작 열이름|
|row2 |`object`|<span class='required'>필수</span>|병합종료 [데이터 로우 객체](/docs/appx/row-object)|
|col2 |`string`|<span class='required'>필수</span>|병합종료 열이름|

### Return Value
***none***

### Example
```javascript
//AR2행부터 AR4행까지 deptCd열부터 empNm열까지 병합
sheet.setMergeRange( sheet.getRowById("AR2"), "deptCd", sheet.getRowById("AR4"), "empNm");
```

### Read More
- [setMergeCancel method](./set-merge-cancel)
- [getMergeRange method](./get-merge-range)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|

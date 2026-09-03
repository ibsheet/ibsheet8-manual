# fitColWidth ***(method)***

<!-- synonyms: 열 너비 조정, 컬럼 너비 맞춤, 열 너비 재설정, 너비 비율 조정, 자동 너비, 컬럼 폭 조정, fit-col-width, fitColWidth, fit column width, adjust column width, resize column, auto width -->

> 각 컬럼의 너비를 시트 전체 너비에 맞게 다시 배분합니다.  
> 컬럼이 넘쳐 가로 스크롤이 생기지 않도록 줄이거나, 오른쪽에 빈 공간이 남지 않도록 늘려 시트 폭에 꽉 차게 맞춥니다.   
> `ratio` 인자를 설정하지 않으면 현재 컬럼 너비 비율을 유지한 채 시트 너비에 맞추고, `ratio` 인자를 설정하면 그 비율대로 재설정합니다.  
> `ratio`를 설정할 때는 컬럼 수만큼 값을 넣고, 값들의 합이 100이 되도록(남는 비율이 없게) 배분해야 정상적으로 동작합니다.  
> **<mark>주의</mark> : [RelWidth](/docs/props/col/rel-width) 사용하는 경우 해당 기능이 정상적으로 지원되지 않습니다.**



### Syntax
```javascript
boolean fitColWidth(ratio);
```


### Parameters


|Name|Type|Required| Description |
|----------|-----|---|----|
|ratio |`array[number]`|<span class='optional'>선택</span>|컬럼의 너비 비율|


### Return Value
***boolean*** : 적용 여부 (너비의 변경이 이루어지면 true, 변화가 없으면 false 리턴)

### Example
```javascript
// 각 컬럼의 현재 너비 비율을 유지하며 시트 너비에 맞게 재설정
sheet.fitColWidth();

// 컬럼이 4개인 시트에서 첫 번째 컬럼부터 10%, 50%, 30%, 10% 비율로 재설정
// (배열의 개수는 컬럼 수와 같아야 하고, 합은 100이 되어야 함)
sheet.fitColWidth([10, 50, 30, 10]);
```

### Read More
- [AutoFitColWidth cfg](/docs/props/cfg/auto-fit-col-width)

### Since

|product|version|desc|
|---|---|---|
|core|8.1.0.41|기능 추가|

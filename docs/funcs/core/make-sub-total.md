# makeSubTotal ***(method)***

<!-- synonyms: 소계, 누계, 합계, subtotal, 그룹 합계, 소계행 -->

> `stdCol`(기준 열)의 같은 값끼리 그룹으로 묶어 합계, 평균, 건수 등을 계산한 소계행을 추가합니다.(`SearchMode` `0`, `2`만 지원)  
> 데이터 조회 후 사용하며, [onDataLoad](/docs/events/on-data-load)에서 호출을 권장합니다.  
> [onSearchFinish](/docs/events/on-search-finish)에서 호출하면 데이터가 많을 경우 성능이 저하될 수 있습니다.  
> 머지된 행을 1건으로 계산하려면 [CalcMergeMode](/docs/props/cfg/calc-merge-mode)를 설정해야 합니다.

### Syntax
```javascript
void makeSubTotal( subTotalRows, usermerge, excludeSubTotalRowCount );
```

### Parameters
|Name|Type|Required|Description|
|----------|-----|---|----|
|subTotalRows|`array[object]`|<span class='required'>필수</span>|소계 행 설정 배열. 아래 `subTotalRows` 표 참고|
|usermerge|`boolean`|<span class='optional'>선택</span>|머지 방식 설정<br/>`0(false)`:`stdCol` 기준으로 자동 머지 (`default`) — 사용자의 `DataMerge`, `PrevColumnMerge` 설정 무시<br/>`1(true)`:사용자가 설정한 `DataMerge`, `PrevColumnMerge`에 따라 머지|
|excludeSubTotalRowCount|`boolean`|<span class='optional'>선택</span>|소계, 누계 행을 `SEQ` 컬럼과 `InfoRow` 행의 개수 카운트에서 제외 여부<br/>`0(false)`:소계, 누계 행을 `SEQ` 컬럼과 `InfoRow` 행의 개수 카운트에 포함 (`default`)<br/>`1(true)`:소계, 누계 행을 `SEQ` 컬럼과 `InfoRow` 행의 개수 카운트에서 제외|

### subTotalRows
|Name|Type|Required|Description|
|----------|-----|---|----|
|stdCol|`string`|<span class='required'>필수</span>|기준 열|
|sumCols|`string`|<span class='optional'>선택</span>|소계가 계산(합)되어야 할 열이름들을 '\|'로 연결한 문자열|
|countCols|`string`|<span class='optional'>선택</span>|소계 행에 데이터 행의 수로 계산되어야 할 열이름들을 '\|'로 연결한 문자열|
|avgCols|`string`|<span class='optional'>선택</span>|소계가 계산(평균값)되어야 할 열이름들을 '\|'로 연결한 문자열|
|color|`string`|<span class='optional'>선택</span>|소계 행의 배경색|
|showCumulate|`boolean`|<span class='optional'>선택</span>|소계에 대한 누계 행 표시 여부<br>`0(false)`:소계에 대한 누계 행 표시 안함(`default`)<br>`1(true)`:소계에 대한 누계 행 표시|
|cumulateColor|`string`|<span class='optional'>선택</span>|누계 행의 배경색|
|sort|`string`|<span class='optional'>선택</span>|기준 열의 정렬 처리 방법 <br/>`""`:사용안함 (`default`)<br/>`"asc"`:오름차순 정렬<br/>`"desc"`:내림차순 정렬|
|position|`string`|<span class='optional'>선택</span>|소계행 생성 위치<br/>`"bottom"`:각 그룹의 하단에 표시 (`default`)<br/>`"top"`:각 그룹의 상단에 표시<br/>`"bottomAll"`:소계행을 시트 최하단에 모아서 표시<br/>`"topAll"`:소계행을 시트 최상단에 모아서 표시|
|captionCol|`array[object]`|<span class='optional'>선택</span>|소계행에서 계산 컬럼(`sumCols`, `countCols`, `avgCols`) 외의 컬럼에 표시할 내용을 설정합니다.<br/>설정하면 기본 텍스트(“소계: 값”)는 표시되지 않으며, 명시한 항목만 표시됩니다.<br/>`"col"`:대상 열이름<br/>`"val"`:소계행에 표시할 값 (문자열 또는 함수)<br/>`"cumVal"`:누계행에 표시할 값<br/>`"span"`:해당 `col` 기준으로 열머지할 컬럼 수 (`val`에 값이 있어야 병합됨)<br/><br/>**사용 가능한 예약어**<br/>`%s`:소계(누계) 텍스트<br/>`%col`:소계 기준값<br/>`%cnt`:소계(누계) 건수<br/>`%capCol`:`col`에 설정된 컬럼의 마지막 행 값<br/><br/>(default: `[{ col: "기준 열", val: "%s: %col" }]`)|
|mode|`number`|<span class='optional'>선택</span>|소계행 표시 방법을 설정<br/>`0`:모든 그룹에 소계행 표시 (`default`)<br/>`1`:소계 계산 대상 행이 2건 이상인 그룹만 소계행 표시<br/>`2`:`NoCalculate` 사용 시 소계 계산 대상 행이 1건 이상인 그룹만 소계행 표시<br/>(소계행은 생성되며, 화면에서만 숨김 처리됩니다.)|
|hidden|`boolean`|<span class='optional'>선택</span>|감춰진 행(`Visible:0`)을 소계 계산에 포함할지 여부<br/>`0(false)`:감춰진 행 제외 (`default`)<br/>`1(true)`:감춰진 행 포함|

### Return Value
***none***

### Example

#### 단일 컬럼 소계
![단일 컬럼 소계](/assets/imgs/makeSubTotal_single.png)
```javascript
// captionCol 미설정 — 기본 캡션("소계: 값")이 자동 표시
sheet.makeSubTotal([
  {
    stdCol: 'sPolicy',
    sumCols: 'A|B|C|D',
    position: 'bottom',
    color: '#dbe2eb'
  }
]);
```

#### 단일 컬럼 소계 (mode:1)
![단일 컬럼 소계 mode:1](/assets/imgs/makeSubTotal_single_mode1.png)
```javascript
// mode:1 — 소계 계산 대상 행이 2건 이상인 그룹만 소계행 표시
sheet.makeSubTotal([
  {
    stdCol: 'sPolicy',
    sumCols: 'A|B|C|D',
    position: 'bottom',
    color: '#dbe2eb',
    mode: 1
  }
]);
```

#### 단일 컬럼 소계/누계
![단일 컬럼 소계/누계](/assets/imgs/makeSubTotal_single_cumulate.png)
```javascript
// captionCol 설정 시 기본 캡션("소계: 값")은 사라지므로,
// 표시하려면 captionCol에 { col: 'stdCol명', val: '%s: %col' }을 직접 지정해야 합니다.
sheet.makeSubTotal([
  {
    stdCol: 'sPolicy',
    sumCols: 'A|B|C|D',
    color: '#dbe2eb',
    cumulateColor: '#b2c4d9',
    showCumulate: 1,
    position: 'bottom',
    captionCol: [
      { col: 'sPolicy', val: '%s: %col', cumVal: '%s: %col' }
    ]
  }
]);
```

#### captionCol 함수형 val 사용
![captionCol 함수형 val](/assets/imgs/makeSubTotal_captionCol_func.png)
```javascript
// captionCol의 val에 함수를 사용하여 소계 값을 동적으로 계산
// 소계행은 Text 타입이므로 숫자 포맷이 필요하면 함수에서 직접 처리해야 합니다.
sheet.makeSubTotal([
  {
    stdCol: 'sPolicy',
    sumCols: 'A|B|C|D',
    position: 'bottom',
    captionCol: [
      {
        col: 'E',
        val: function (fr) {
          // Type과 Format을 직접 설정하면 숫자 포맷 적용 가능
          var ratio = (fr.Row["B"] / fr.Row["A"] * 100).toFixed(1);
          var type = fr.Sheet.getAttribute("", fr.Col, "Type");
          fr.Row[fr.Col + "Type"] = type;
          fr.Row[fr.Col + "Format"] = "#,##0.##### \\%";
          return ratio;
        }
      },
      {
        col: 'F',
        val: function (fr) {
          var val = fr.Row["A"] + fr.Row["B"];
          var type = fr.Sheet.getAttribute("", fr.Col, "Type");
          fr.Row[fr.Col + "Type"] = type;
          fr.Row[fr.Col + "Format"] = "#,##0";
          return val;
        }
      }
    ]
  }
]);
```

#### 소계 그룹 데이터 접근
```javascript
// captionCol function에서 소계 그룹의 데이터 행에 접근
sheet.makeSubTotal([
  {
    stdCol: 'sPolicy',
    sumCols: 'A',
    avgCols: 'B',
    countCols: 'C',
    captionCol: [
      {
        col: 'sUnit',
        val: function (fr) {
          // 현재 소계행의 그룹 데이터를 가져옴
          var subSumSet = fr.Sheet.SubSumRowsArray.filter(function(rowSet) {
            return rowSet.SubSumRow == fr.Row;
          });
          // SubSumGroupedRows: 소계 그룹에 속한 데이터 행 배열
          return subSumSet[0].SubSumGroupedRows.length;
        }
      }
    ]
  }
]);
```

#### 소계 그룹 데이터 접근 — 시간 데이터 합산
![소계 시간 합산](/assets/imgs/makeSubTotal_time_sum.png)
```javascript
// 시간 데이터는 합산 시 24시간을 초과할 수 있으므로,
// SubSumGroupedRows로 그룹 데이터에 접근하여 직접 계산
sheet.makeSubTotal([
  {
    stdCol: 'weekOdr',
    captionCol: [
      {
        col: 'wkTm',
        val: function (fr) {
          var subSumSet = fr.Sheet.SubSumRowsArray.filter(function(rowSet) {
            return rowSet.SubSumRow == fr.Row;
          });
          var rows = subSumSet[0].SubSumGroupedRows;

          // Date 타입은 timestamp로 저장되므로 dateToString으로 변환 후 파싱
          var totalMin = 0;
          rows.forEach(function(row) {
            var hm = IBSheet.dateToString(row.wkTm, "HHmm");
            var h = parseInt(hm.substring(0, 2)) || 0;
            var m = parseInt(hm.substring(2)) || 0;
            totalMin += h * 60 + m;
          });

          var days = Math.floor(totalMin / (24 * 60));
          var hours = Math.floor((totalMin % (24 * 60)) / 60);
          var mins = totalMin % 60;
          return days + "일 " + hours + "시간 " + mins + "분";
        }
      }
    ]
  }
]);
```

#### Def.SubSum으로 소계행 스타일 설정
소계행은 CSS로 스타일 변경이 안 됩니다.  
배경색, 글자색, 포맷 등은 `Def.SubSum`에서 설정하며, `makeSubTotal`의 `color` 속성으로 배경색을 덮어쓸 수 있습니다.
```js
Def: {
  SubSum: {
    Color: '#f0f0f0',           // 소계행 기본 배경색 (makeSubTotal의 color로 덮어쓰기 가능)
    TextColor: 'red',           // 소계행 전체 글자 색상
    ATextColor: 'green',        // A컬럼 소계행 글자 색상
    // Format은 sumCols, avgCols, countCols로 계산된 컬럼만 적용 가능 (8.0.0.25~)
    // captionCol의 function으로 생성된 소계행은 Text 타입이라 Format이 적용되지 않음
    AFormat: '합계 : #,##0.##', // A컬럼 소계행 포맷
    BFormat: '#,##0'            // B컬럼 소계행 포맷
  }
}
```

#### 다중 컬럼 소계
![다중 컬럼 소계](/assets/imgs/makeSubTotal_multi.png)
```javascript
sheet.makeSubTotal([
  {
    stdCol: 'sPolicy',
    sumCols: 'B|C',
    position: 'bottom',
    color: '#b2c4d9'
  },
  {
    stdCol: 'sUnit',
    avgCols: 'B|C',
    position: 'bottom',
    color: '#dbe2eb',
    captionCol: [
      { col: 'sUnit', val: '%s: %col' }
    ]
  }
]);
```

#### usermerge 사용
![usermerge](/assets/imgs/makeSubTotal_usermerge.png)
```javascript
// Cfg.DataMerge:0 (머지 없음) 설정일 때

// usermerge:0 (기본값) — DataMerge:0 이어도 stdCol 기준으로 자동 머지
sheet.makeSubTotal([
  { stdCol: 'sPolicy', sumCols: 'A|B|C|D', position: 'bottom', color: '#dbe2eb' }
]);

// usermerge:1 — DataMerge:0 설정을 따르므로 머지 없이 소계행만 추가
sheet.makeSubTotal([
  { stdCol: 'sPolicy', sumCols: 'A|B|C|D', position: 'bottom', color: '#dbe2eb' }
], 1);
```

### Read More
- [SearchMode cfg](/docs/props/cfg/search-mode)
- [CalcMergeMode cfg](/docs/props/cfg/calc-merge-mode)
- [onDataLoad event](/docs/events/on-data-load)
- [removeSubTotal method](./remove-sub-total)
- [getSubTotalRows method](./get-sub-total-rows)
- [NoCalculate row](/docs/props/row/no-calculate)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.0.0.7|`mode` 속성 기능 추가|
|core|8.0.0.11|`usermerge` 기능 추가|
|core|8.0.0.11|`%capCol` 예약어 추가|
|core|8.0.0.18|`onDataLoad` 이벤트에서 호출 권장|
|core|8.0.0.22|`hidden` 속성 추가|
|core|8.1.0.78|`excludeSubTotalRowCount` 기능 추가|

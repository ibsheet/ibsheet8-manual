# makePivotTable ***(method)***

<!-- synonyms: 피벗 테이블, 피봇 테이블, 피봇 생성, pivot table, 집계 테이블, 다이얼로그 없이 피벗 -->

> 대상 시트의 모든 데이터를 기준으로 피벗 테이블을 생성합니다.  
> 다이얼로그 UI 없이 코드로 직접 피벗 시트를 만들 때 사용하며, 다이얼로그 형태가 필요하면 [showPivotDialog](/docs/funcs/dialog/show-pivot-dialog)를 사용하세요.  
> 피벗 생성 시점에 대상 시트가 필터링되어 있으면 필터가 취소된 후 피벗이 생성됩니다.  
> 생성된 피벗 시트의 id는 `"pivotSheet_" + 원본시트id` 입니다. (예: 원본 id `"sheet"` → 피벗 id `"pivotSheet_sheet"`)  
> 피벗 시트에서는 [DataMerge](/docs/props/cfg/data-merge) 기능을 지원하지 않습니다.

> **주의:** 행 5,000개 또는 열 200개를 초과하는 피벗 테이블은 브라우저 성능을 보장할 수 없습니다.  
> `init` 설정 시 기준 행·열이 그 미만이 되도록 권장합니다.

### Syntax
```javascript
object makePivotTable(criterias, init, format, type, callback, hideTotal);
```

### Parameters
|Name|Type|Required|Description|
|----------|-----|---|----|
|criterias|`object`|<span class='optional'>선택</span>|피벗 시트에서 행/열/데이터 구성에 쓸 수 있는 컬럼들<br/>`null` 또는 `""` 설정시 시트의 전체 컬럼이 자동으로 사용됩니다|
|init|`object`|<span class='required'>필수</span>|피벗 테이블의 실제 구성(행/열/데이터 컬럼)|
|format|`string`|<span class='optional'>선택</span>|피벗 셀에 표시할 숫자 포맷 (예: `"#,###"`, `"#,### 만원"`)|
|type|`string`|<span class='optional'>선택</span>|`init.data` 컬럼별 집계 방법<br/>지원 값: `"Sum"`, `"Count"`, `"Max"`, `"Min"`, `"Avg"`<br/>`init.data`가 1개이면 생략 가능 (`default: "Sum"`)<br/>`init.data`가 여러 개이면 같은 개수만큼 쉼표로 연결 (예: `data: "sSalary,sBonus"` → `type: "Sum,Sum"`)<br/>피벗 결과 컬럼명은 **`{type 대문자}{원본컬럼명}`** 형식 (예: `"Sum"` + `"sSalary"` → `SUMsSalary`)|
|callback|`function`|<span class='optional'>선택</span>|피벗 시트 생성 완료 후 호출되는 콜백. 피벗 시트의 [onRenderFirstFinish](/docs/events/on-render-first-finish) 시점에 발생|
|hideTotal|`object`|<span class='optional'>선택</span>|총합계 행/열 숨김 여부|

### criterias (선택)
|Name|Type|Description|
|----------|-----|----|
|row|`string`|행 레이블에 선택 가능한 컬럼명을 쉼표로 연결한 문자열|
|col|`string`|열 레이블에 선택 가능한 컬럼명을 쉼표로 연결한 문자열|
|data|`string`|계산 대상으로 선택 가능한 컬럼명(`Int`/`Float`)을 쉼표로 연결한 문자열|

### init (필수)
|Name|Type|Description|
|----------|-----|----|
|row|`string`|행 레이블에 실제 사용할 컬럼명 (쉼표로 다중 가능, 빈 문자열 가능)|
|col|`string`|열 레이블에 실제 사용할 컬럼명 (쉼표로 다중 가능, 빈 문자열 가능)|
|data|`string`|계산 대상 컬럼명(`Int`/`Float`)을 쉼표로 연결|

### hideTotal
|Name|Type|Description|
|----------|-----|----|
|hideTotalRow|`boolean`|각 행의 합계 컬럼(우측 끝) 숨김 여부 (`default: false`)|
|hideTotalCol|`boolean`|각 열의 합계 행(하단) 숨김 여부 (`default: false`)|

### Return Value
***object*** — 생성된 피벗 시트 객체

### Example

```javascript
// 1. 가장 단순한 케이스 — 부서별 급여 합계 (열 분류 없음)
//    → 행 레이블(부서) 1개 컬럼 + 합계: 급여 1개 컬럼
sheet.makePivotTable(null, {
    row:  'sDept',
    col:  '',
    data: 'sSalary'
});

// 2. 행 × 열 교차표 — 부서 × 직급별 급여 합계
//    → 부서(행) × 직급(열) 매트릭스 + 우측에 행별 합계 컬럼
sheet.makePivotTable(null, {
    row:  'sDept',
    col:  'sPosition',
    data: 'sSalary'
}, '#,###');

// 3. 여러 데이터 컬럼 + 다른 집계 방식 — 부서×직급별 (급여 합계, 인원수)
//    → 각 직급마다 '합계: 급여' / '개수: 성명' 두 서브 컬럼 생성
sheet.makePivotTable(null, {
    row:  'sDept',
    col:  'sPosition',
    data: 'sSalary,sName'
}, '#,###', 'Sum,Count');

// 4. 콜백으로 생성 후 후처리 — 부서별 급여 합계가 2천만 넘는 행은 빨간색
sheet.makePivotTable(null, {
    row:  'sDept',
    col:  'sPosition',
    data: 'sSalary'
}, '#,###', 'Sum', function (evt) {
    var rows = evt.sheet.getDataRows();
    for (var i = 0; i < rows.length; i++) {
        if (evt.sheet.getValue(rows[i], 'SUMsSalary') > 20000000) {
            evt.sheet.setAttribute(rows[i], 'SUMsSalary', 'TextColor', '#FF0000');
        }
    }
});

// 5. 합계 숨김 — 우측 행별 합계 컬럼 숨기기
//    → hideTotalRow: 각 행의 합계 컬럼(우측), hideTotalCol: 각 열의 합계 행(하단)
sheet.makePivotTable(null, {
    row:  'sDept',
    col:  'sPosition',
    data: 'sSalary'
}, '#,###', 'Sum', null, { hideTotalRow: true });

// 6. criterias 사용 — UsePivot 모드에서 피벗 고정행 드래그 제한
//    → 'sSalary'를 col에만 넣어두면 고정행에서 '급여' 항목은 '세로행 기준'으로만 드롭 가능
options.Cfg = { UsePivot: true };  // 피벗 고정행 활성화

var criterias = {
    row:  'sDept,sTeam,sPosition,sGender,sAgeRanges,sAddr',
    col:  'sDept,sTeam,sPosition,sGender,sAgeRanges,sAddr,sSalary',
    data: 'sAge'
};
var init = {
    row:  'sDept',
    col:  'sPosition,sTeam',
    data: 'sSalary'
};
sheet.makePivotTable(criterias, init);
```

### Try it
- [Demo of makePivotTable](https://jsfiddle.net/gh/get/library/pure/ibsheet/ibsheet8-manual-sample/tree/master/samples/method/makePivotTable/)

### Read More
- [showPivotDialog method](/docs/funcs/dialog/show-pivot-dialog)
- [switchPivotSheet method](./switch-pivot-sheet)
- [onAfterPivot event](/docs/events/on-after-pivot)
- [UsePivot cfg](/docs/props/cfg/use-pivot)
- [PivotFunc cfg](/docs/props/cfg/pivot-func)
- [PivotFormat cfg](/docs/props/cfg/pivot-format)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.0.0.17|`callback` 기능 추가|
|core|8.1.0.46|`type` 옵션 `Max`, `Min` 추가|
|core|8.1.0.94|`criterias` 인자 선택으로 변경 (`null`/`""` 사용 가능)|
|core|8.2.0.15|`pivotType` 관련 기능 개선|
|core|8.3.0.9|`hideTotal` 인자 기능 추가|

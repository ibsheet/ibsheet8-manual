# ResponsiveCol ***(cfg)***

<!-- synonyms: 반응형 컬럼, 반응형 그리드, 모바일 대응, 열 접기, 열 자동 숨김, 열 접힘, responsive column, mobile grid, collapse column -->

> 그리드 폭이 좁아질 때 표시되지 못한 열을 숨기고, 숨겨진 열의 값은 행 아래 확장 영역에 라벨-값 형태로 표시하는 반응형 레이아웃을 활성화합니다.  
> 각 행 좌측에 자동으로 토글 아이콘 열이 생성되며, 클릭 시 해당 행의 숨겨진 열 값들이 펼쳐집니다.  
> `제약사항`: [SearchMode](./search-mode) `2`(단순 조회용) 시트에서만 사용 가능하며, 아래 경우에는 사용할 수 없습니다.
> - `MultiRecord`(멀티레코드), 그룹핑, 트리 시트
> - [FitWidth](/docs/props/cfg/fit-width) 사용
> - 소계/누계 사용, `Foot`/`Solid` 고정 행 사용
> - [setFixedTop](/docs/funcs/core/set-fixed-top) / [setFixedBottom](/docs/funcs/core/set-fixed-bottom) 메소드로 고정된 행 사용
> - `RelWidth` 속성 사용

### Type
mixed( `boolean` \| `object` )

### Options
|Value|Description|
|-----|-----|
|`0(false)`|반응형 레이아웃 사용 안 함 (`default`)|
|`1(true)`|반응형 레이아웃 사용|
|`object`|반응형 레이아웃 사용 + 세부 옵션 지정 (아래 세부 옵션 참조)|

### object 세부 옵션
|Name|Type|Description|
|---|---|---|
|`Expanded`|`boolean`|접힌 열이 있을 때 모든 행을 기본적으로 펼친 상태로 렌더링할지 여부 (`default: 0`)|
|`HeaderColor`|`string`|확장 영역 라벨 셀의 배경색 (예: `"#F5F5F5"`)|
|`HeaderWidth`|`number`|확장 영역 라벨 셀의 너비 (px 단위)|


### Example
```javascript
// 1) 기본 활성화
options.Cfg = {
    ResponsiveCol: 1
};

// 2) 세부 옵션과 함께 사용
options.Cfg = {
    ResponsiveCol: {
        Expanded: 1,             // 처음부터 모든 행을 펼친 상태로 시작
        HeaderColor: "#F5F5F5",  // 라벨 배경색
        HeaderWidth: 100         // 라벨 너비 100px
    }
};
```

### Read More


### Since

|product|version|desc|
|---|---|---|
|core|8.4.0.12|기능 추가|

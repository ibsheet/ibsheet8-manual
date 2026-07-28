# ClipTextOverflow ***(col)***

<!-- synonyms: 말줄임, 말줄임표, 생략부호, 텍스트 넘침, 텍스트 자르기, ellipsis, text-overflow, clip -->

> 열의 셀 내용이 열 너비보다 길 때 끝에 말줄임표(...)를 붙일지 여부를 설정합니다.  
> 이 속성은 데이터 영역에만 적용되며 헤더에는 적용되지 않습니다. 헤더를 포함한 개별 셀에 지정하려면 [ClipTextOverflow (cell)](/docs/props/cell/clip-text-overflow)을 사용하세요.

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|말줄임표(...) 기능을 사용합니다. (`default`)|
|`1(true)`|말줄임표(...) 기능을 사용하지 않습니다.|

### Example
```javascript
options.Cols = [
  {
    Header: '정수(Int)',
    Type: 'Int',
    Name: 'IntData',
    Width: 80,
    Align: 'Right',
    CanEdit: 1,
    Format: '####,0원',
    ClipTextOverflow: true
  }
];
```

### Read More

### Since

|product|version|desc|
|---|---|---|
|core|8.1.0.86|기능 추가|

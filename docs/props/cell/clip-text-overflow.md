# ClipTextOverflow ***(cell)***

<!-- synonyms: 말줄임, 말줄임표, 생략부호, 텍스트 넘침, 텍스트 자르기, ellipsis, text-overflow, clip, 헤더 말줄임 -->

> 개별 셀의 내용이 셀 너비보다 길 때 끝에 말줄임표(...)를 붙일지 여부를 설정합니다.  
> [ClipTextOverflow (col)](/docs/props/col/clip-text-overflow)는 데이터 영역에만 적용되고 헤더에는 적용되지 않으므로, 헤더를 포함한 특정 셀에 적용할 때 이 속성을 사용합니다.

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
    // 헤더 셀에 적용 (헤더 텍스트가 길어도 말줄임표(...)를 표시하지 않음)
    Header: { Value: '아주 긴 헤더 제목입니다', ClipTextOverflow: true },
    Type: 'Text',
    Name: 'DATA',
    Width: 80
  }
];
```

### Read More
- [ClipTextOverflow col](/docs/props/col/clip-text-overflow)

### Since

|product|version|desc|
|---|---|---|
|core|8.4.0.7|기능 추가|

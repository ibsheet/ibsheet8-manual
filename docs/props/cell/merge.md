# Merge ***(cell)***
> 여러 컬럼의 값을 한 셀에 모아서 표시합니다.  
> 표시만 할 뿐 실제 셀의 값은 각 컬럼에 별도로 관리됩니다.  
> `row`에 [Spanned](/docs/props/row/spanned) 속성이 `1`로 설정되어야 동작합니다.

### 동작 이미지
![Merge속성](/assets/imgs/Merge.png)
[empinfoMerge:"empno,empNm,pstnGbn" 으로 설정]

### Type
`string`

### Options
|Value|Description|
|-----|-----|
|`string`|열이름 (","구분자로 여러개 지정 가능)|

### Example
```javascript
//Spanned가 설정되어 있어야 함.
options.Def.Row = {Spanned: 1};

//empinfo 열에서 empno,empNo,pstnGbn 열의 값을 모두 표시
options.Def.Row["empinfo"] = {"Merge": "empno,empNm,pstnGbn"}

```
### Read More
- [Span cell](./span)
- [Spanned row](/docs/props/row/spanned)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|

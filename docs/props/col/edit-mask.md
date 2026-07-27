# EditMask ***(col)***

<!-- synonyms: 입력 제한, 입력 마스크, 정규식 입력 제한, 입력 가능 문자 제한, 숫자만 입력, 소수점 자리수 입력 제한, edit mask, input mask -->

> 셀에 입력 가능한 문자를 자바스크립트 정규식으로 설정합니다.  
> 입력한 글자는 정규식의 `search()` 함수로 입력 허용 여부가 결정됩니다.  
> `"입력값".search(EditMask) >= 0`  
> `true`인 경우 입력 허용  
> `false`인 경우 입력 제한  
> 정규식에 맞지 않는 글자는 입력되지 않습니다.
>
> 정규식 예시
> - 띄어쓰기를 제외한 모든 글자 입력 허용: `"^\\S*$"`
> - 숫자만 입력 가능: `"^\\d*$"`
> - 알파벳만 가능: `"^\\w*$"`
> - 숫자 10자리까지만 가능: `"^\\d{0,10}$"`


### Type
`string`

### Options
|Value|Description|
|-----|-----|
|`string`|자바스크립트 정규식 문자|

### Example
```javascript
options.Cols = [
    // 띄어쓰기를 제외한 모든 글자 입력 가능
    {Type: "Text", Name: "CN_Code", EditMask: "^\\S*$", Width: 120},

    // 소수점 둘째 자리까지만 입력 허용 (정수/음수 포함)
    {Type: "Float", Name: "sFloat", EditMask: "^-?\\d*(\\.\\d{0,2})?$", Format: "#,##0.00"},

    // 마이너스 제외(양수만), 소수 입력 허용
    {Type: "Float", Name: "sPos", EditMask: "^\\d*(\\.\\d*)?$"}
];
```

### Read More

<!--!
- `[비공개]` [MaskColor col](./mask-color)
!-->
- [ResultMask col](./result-mask)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|

# FilterValueList ***(cfg)***

<!-- synonyms: FilterValueList, filter value list, filter empty label, filter blank text, filter empty display, 필터 빈값 표시, 필터 값 목록, 필터 빈값 문자열, FilterEmptyValue, 필터 빈값 라벨, Enum 필터 빈값 -->

> 필터행의 특정셀에 값 목록이 있을때 처리하는 방법을 설정합니다.


### Type
`number`


### Options
|Value|Description|
|-----|-----|
|`0`|필터 값이 빈값일때 빈값 그대로 보여줌 (`default`) |
|`1`|`Button: "Defaults"`, `Defaults`를 `*Row`로 설정할 경우 필터 값이 빈값일때 메시지 파일에 `Lang.Text.FilterEmptyValue`에 정의된 문자열로 표시 |
|`2`|`Enum` 타입일 경우 필터 값이 빈값일때 메시지 파일에 `Lang.Text.FilterEmptyValue`에 정의된 문자열로 표시 |
|`3`|`1번 설정`과 `2번 설정`을 동시에 적용 |

### Example
```javascript
options.Cfg = {
   FilterValueList: 1
   ...
};
```

### Read More
- [Type appendix](/docs/appx/type)
- [Button col](/docs/props/col/button)
- [Defaults col](/docs/props/col/defaults)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|

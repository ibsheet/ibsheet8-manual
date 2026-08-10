# RemoveCustomFormatDelimiter ***(cfg)***

<!-- synonyms: RemoveCustomFormatDelimiter, remove custom format delimiter, custom format strip, load format delimiter, CustomFormat 구분자 제거, 데이터 로드 구분자 제거, 커스텀 포맷 구분자, 로드 시 구분자 제거, 데이터 치환 -->

> 데이터 로드시 설정된 CustomFormat 과 동일한 포멧일시 구분자를 제거하는 기능을 추가합니다.  
>
> 동일한 CustomFormat 이 제대로 적용되도록 하기 위해 원본데이터를 구분자를 제거한 데이터로 치환합니다. 

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|구분자를 제거하지 않음 (`default`)|
|`1(true)`|설정된 CustomFormat 과 동일한 포멧일시 구분자를 제거|

### Example
```javascript
options.Cfg = {
  RemoveCustomFormatDelimiter: true      // 웹 접근성 모드 사용
};
```

### Read More


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.24|기능 추가|

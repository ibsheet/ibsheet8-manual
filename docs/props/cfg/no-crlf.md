# NoCRLF ***(cfg)***

<!-- synonyms: 복사 줄바꿈, 후행 줄바꿈, 마지막 줄바꿈, 빈 줄, 개행, CRLF 제거, copy trailing newline, 복사 붙여넣기 줄바꿈, Ctrl C Ctrl V 줄바꿈 -->

> 셀이나 행을 복사할 때 맨 마지막 행 뒤에 붙는 줄바꿈(CRLF)을 제거할지 설정합니다.

### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|복사 시 마지막 행 뒤에도 줄바꿈(CRLF)이 붙습니다. (`default`)|
|`1(true)`|복사 시 맨 마지막 행 뒤에 붙는 줄바꿈(CRLF)만 제거합니다. <br/>행과 행 사이 구분자는 유지되므로 여러 행을 복사해 붙여넣어도 행 구분은 정상입니다.|

### Example
```javascript
options.Cfg = {
    "NoCRLF": 1     //복사 시 마지막 행 뒤에 붙는 줄바꿈(CRLF) 제거
};
```

### Read More
- [CopyEdit cfg](/docs/props/cfg/copy-edit)
- [CopyCols cfg](/docs/props/cfg/copy-cols)

### Since

|product|version|desc|
|---|---|---|
|core|8.3.0.54|기능 추가|

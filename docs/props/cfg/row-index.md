# RowIndex ***(cfg)***

<!-- synonyms: RowIndex, row index, seq column, sequence column, seq replacement, custom seq, 순번 컬럼, SEQ 대체, 행 번호 컬럼, 인덱스 컬럼, 시퀀스 컬럼, SEQ 컬럼명 변경 -->

> `SEQ`의 기능을 대신할 컬럼명을 지정합니다.  
> 지정한 컬럼명을 넣으면 그 컬럼이 `SEQ` 기능(자동 증가 순번)을 대신합니다.


### Type
`string`

### Options
|Value|Description|
|-----|-----|
|`string`|`SEQ` 기능을 대신 사용할 컬럼명|

### Example
```javascript
options.Cfg = {
    RowIndex: "AAA" // SEQ의 기능을 대신할 컬럼명
};

```

### Read More


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.10|기능 추가|

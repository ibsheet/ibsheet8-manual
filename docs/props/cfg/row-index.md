# RowIndex ***(cfg)***

<!-- synonyms: RowIndex, row index, seq column, sequence column, seq replacement, custom seq, 순번 컬럼, SEQ 대체, 행 번호 컬럼, 인덱스 컬럼, 시퀀스 컬럼, SEQ 컬럼명 변경 -->

> `SEQ`의 기능을 대신할 컬럼명을 변경할 수 있습니다. <br/> 해당 기능에 컬럼명을 넣어주면, `SEQ`기능을 해당 컬럼에서 대신 사용할 수 있습니다. 


### Type
`string`


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

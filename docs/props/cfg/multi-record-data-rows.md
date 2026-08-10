# MultiRecordDataRows ***(cfg)***

<!-- synonyms: MultiRecordDataRows, multi record data rows, multirecord data rows, record data rows, 멀티레코드 데이터행, 멀티레코드 데이터 행 개수, MultiRecord 데이터 행, 데이터 행 개수 조절, 멀티레코드 행 수 -->

> 멀티레코드([MultiRecord](/docs/props/cfg/multi-record)) 기능을 사용하는 시트에서 데이터행의 행 개수를 조절하는 기능입니다.  
> 생성된 행 개수보다 많게 설정할 수 없습니다. (단위데이터행 개수가 3개인데 데이터행의 개수는 4개로 설정 할 수 없음)  
> 멀티레코드 레이아웃은 엑셀 다운로드/업로드, `doPrint`, `down2Pdf` 등 출력 시에는 기본적으로 유지되지 않습니다. (`down2Excel`은 [MultiRecordShape](/docs/props/cfg/multi-record-shape):`1`로 화면 모양 그대로 받을 수 있으나 머지가 많으면 느립니다.)

### Type
`number`


### Options
|Value|Description|
|-----|-----|
|`number`|화면에 표시할 멀티레코드 시트의 데이터행 개수|


### Example
```javascript
options.Cfg = {
   MultiRecord: 1,  // 멀티레코드 전용 시트로 설정
   MultiRecordDataRows: 2 // 멀티레코드의 데이터행 개수를 2개로 조정합니다.
   ...
};
```

### Read More

- [MultiRecord cfg](/docs/props/cfg/multi-record)
- [MultiRecordHeaderRows Cfg](/docs/props/cfg/multi-record-header-rows)
- [MultiRecordShape cfg](/docs/props/cfg/multi-record-shape)

### Since

|product|version|desc|
|---|---|---|
|core|3.0.53|기능 추가|

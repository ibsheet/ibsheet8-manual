# MultiRecordDataRows ***(cfg)***

> 멀티레코드([MultiRecord](/docs/props/cfg/multi-record)) 기능을 사용하는 시트에서 데이터행의 행 개수를 조절하는 기능입니다.
>
> 생성된 행 개수보다 많게 설정할 수 없습니다. (단위데이터행 개수가 3개인데 데이터행의 개수는 4개로 설정 할 수 없음)

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

### Since

|product|version|desc|
|---|---|---|
|core|3.0.53|기능 추가|

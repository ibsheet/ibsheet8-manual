# MultiRecordShape ***(cfg)***

> 멀티레코드([MultiRecord](/docs/props/cfg/multi-record)) 기능을 사용하는 시트에서 엑셀 파일 다운로드를 화면에 보이는 그대로 나타나게 하는 설정입니다.  
> 서버 모듈 다운로드([down2Excel](/docs/funcs/excel/down-to-excel))에서만 지원됩니다. 클라이언트 모듈 다운로드([exportData](/docs/funcs/core/export-data))는 지원하지 않습니다.  
> 다이얼로그 다운로드([showDownloadDialog](/docs/funcs/dialog/show-download-dialog))에서는 지원되지 않습니다.


### Type
`number`


### Options
|Value|Description|
|-----|-----|
|`0`|열을 일렬로 표시해서 다운로드 (`default`)|
|`1`|열을 시트에서 보이는대로 표시해서 다운로드|
<!--!
|`[비공개]` `2`|Select 시 멀티레코드 모양으로 동작|
|`[비공개]` `4`|복사/붙여넣기 시 멀티레코드 모양으로 동작|
!-->

> `1`은 화면 모양(머지 포함)을 그대로 재현하므로 머지 셀이 많으면 다운로드가 느릴 수 있습니다.  
> 형태를 유지한 채로 속도를 높이긴 어려우므로, 속도가 중요하면 `0`으로 받거나 [down2Excel](/docs/funcs/excel/down-to-excel)의 `merge:0` 또는 `onlyHeaderMerge:1`로 머지를 줄여 받으세요.

### Example
```javascript
options.Cfg = {
   MultiRecord: 1,  // 멀티레코드 전용 시트로 설정
   MultiRecordShape: 1,  // 멀티레코드 시트의 모양대로 엑셀 파일 다운로드
   ...
};

// API 사용
sheet.down2Excel({ sheetDesign: 1, merge: 1 }); // 엑셀 다운로드 실행
```

### Read More

- [MultiRecord cfg](/docs/props/cfg/multi-record)
- [down2Excel method](/docs/funcs/excel/down-to-excel)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|excel|0.0.0|기능 추가|
<!--!
|`[비공개]` core|8.0.0.17|`2(Select)`, `4(Copy/Paste)` 기능 추가|
!-->

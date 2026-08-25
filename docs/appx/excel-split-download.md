# 엑셀 그룹별 나눠 다운로드 ***(appendix)***

<!-- synonyms: 여러 엑셀 파일 다운로드, 엑셀 파일 나눠 다운로드, 그룹별 엑셀 다운로드, 사용자별 엑셀, 부서별 엑셀, 거래처별 엑셀, 여러 파일로 나눠 받기, 그룹별 워크시트, 사용자별 워크시트, 한 시트에서 여러 파일, split excel files, one sheet multiple files, exportData 여러 파일, down2Excel 여러 파일, down2ExcelBuffer 워크시트 분리 -->

> 한 시트에 조회해 둔 데이터를 특정 컬럼(예: 사용자, 부서, 거래처) 값 기준으로 나눠, **그룹마다 별도의 엑셀 파일**로 받거나 **한 파일 안의 그룹별 워크시트**로 받는 방법을 정리합니다.  
> 클라이언트 다운로드([exportData](/docs/funcs/core/export-data))와 서버 다운로드([down2Excel](/docs/funcs/excel/down-to-excel)) 각각을 다룹니다.

## 공통 주의사항

- **같은 시트로 연달아 다운로드하지 않습니다.**  
  `exportData`는 뒤 호출이 앞 호출을 덮어쓰므로 그룹마다 **임시 시트**를 만들고, `down2Excel`은 마지막 파일만 내려오므로 `useXhr: 1` 또는 `onExportFinish`로 하나씩 호출합니다.

## 클라이언트 다운로드 (exportData)

### 그룹마다 별도 파일

그룹마다 그 그룹의 데이터만 담은 임시 시트를 만들어 각각 `exportData` 합니다.  
시트를 비동기로 생성하고, 생성이 끝나면(`onRenderFirstFinish`) 자기 자신을 내보낸 뒤, 완료되면(`onExportFinish`) 정리합니다.

```javascript
// USER 값으로 데이터를 그룹화
var groups = {};
sheet.getSaveJson({ saveMode: 0 }).data.forEach(function (row) {
  (groups[row.USER] = groups[row.USER] || []).push(row);
});
var srcCols = sheet.getUserOptions().Cols;   // 원본 컬럼 정의

Object.keys(groups).forEach(function (key) {
  var box = document.createElement("div");
  box.style.display = "none";
  document.body.appendChild(box);
  var cols = JSON.parse(JSON.stringify(srcCols));   // 컬럼 정의는 시트마다 새로 복제 (공유하면 2번째 시트부터 헤더 유실)

  IBSheet.create({
    el: box,
    options: {
      Cols: cols,
      Events: {
        onRenderFirstFinish: function (evtParam) {
          evtParam.sheet.exportData({ fileName: key + ".xlsx", sheetName: key, downHeader: true });
        },
        onExportFinish: function (evtParam) { evtParam.sheet.dispose(); box.remove(); }
      }
    },
    data: groups[key]
  });
});
```

### 한 파일에 그룹별 워크시트

[exportDataBuffer](/docs/funcs/core/export-data-buffer)로 시작하면 각 시트의 `exportData`가 파일이 아니라 워크시트로 버퍼에 쌓여, 한 엑셀 파일로 묶여 다운로드됩니다.

```javascript
var groups = {};
sheet.getSaveJson({ saveMode: 0 }).data.forEach(function (row) {
  (groups[row.USER] = groups[row.USER] || []).push(row);
});
var srcCols = sheet.getUserOptions().Cols;

var made = [];
Object.keys(groups).forEach(function (key) {
  var box = document.createElement("div"); box.style.display = "none"; document.body.appendChild(box);
  var cols = JSON.parse(JSON.stringify(srcCols));   // 시트마다 복제 (공유하면 2번째 시트부터 헤더 유실)
  var s = IBSheet.create({ el: box, options: { Cols: cols }, data: groups[key], sync: 1 });
  made.push({ sheet: s, key: key, box: box });
});

made[0].sheet.exportDataBuffer(true);               // 버퍼 시작
made.forEach(function (m, i) {
  var param = { sheetName: m.key, downHeader: true };
  if (i === 0) param.fileName = "가계부.xlsx";       // 파일명은 첫 호출에만
  m.sheet.exportData(param);                         // 워크시트로 누적
});
made[0].sheet.exportDataBuffer(false);              // 버퍼 종료 (한 파일로 다운로드)
setTimeout(function () { made.forEach(function (m) { m.sheet.dispose(); m.box.remove(); }); }, 1500);
```

## 서버 다운로드 (down2Excel)

### 그룹마다 별도 파일

서버 다운로드는 임시 시트 없이, 한 시트에서 `downRows`로 사용자별 행을 골라 받을 수 있습니다.  
각 호출에 `useXhr: 1`을 주면 연달아 호출해도 각 파일이 모두 내려옵니다.

```javascript
// USER 값별로 데이터 행 번호(1부터)를 모은다
var rowsByUser = {};
sheet.getSaveJson({ saveMode: 0 }).data.forEach(function (row, i) {
  (rowsByUser[row.USER] = rowsByUser[row.USER] || []).push(i + 1);
});

// 그룹마다 그 행만 골라(downRows) 파일로 다운로드
Object.keys(rowsByUser).forEach(function (user) {
  sheet.down2Excel({ fileName: user + ".xlsx", downRows: rowsByUser[user].join("|"), useXhr: 1 });
});
```

**서버가 다른 도메인일 때**는 `useXhr`가 CORS 제약으로 막힐 수 있습니다.  
이때는 `useXhr` 없이, 한 파일이 끝날 때(`onExportFinish`)마다 다음 파일을 호출해 하나씩 받습니다.

```javascript
var rowsByUser = {};
sheet.getSaveJson({ saveMode: 0 }).data.forEach(function (row, i) {
  (rowsByUser[row.USER] = rowsByUser[row.USER] || []).push(i + 1);
});
var files = Object.keys(rowsByUser).map(function (user) {
  return { fileName: user + ".xlsx", downRows: rowsByUser[user].join("|") };
});

// 한 파일이 끝나면 다음 파일 (onExportFinish 로 하나씩)
var idx = 0;
sheet.bind("onExportFinish", function (evtParam) {
  if (++idx < files.length) evtParam.sheet.down2Excel(files[idx]);
});
sheet.down2Excel(files[0]);   // 첫 파일부터 시작
```

### 한 파일에 그룹별 워크시트

[down2ExcelBuffer](/docs/funcs/excel/down-to-excel-buffer)로 그룹별 임시 시트를 한 파일의 워크시트로 묶습니다. (임시 시트는 원본과 같은 서버 경로 `Cfg.Export.Url`이 필요합니다.)

```javascript
var exportUrl = "./servermodule/";   // 원본 시트와 동일한 서버 경로
var srcCols = sheet.getUserOptions().Cols;
var groups = {};
sheet.getSaveJson({ saveMode: 0 }).data.forEach(function (row) {
  (groups[row.USER] = groups[row.USER] || []).push(row);
});

var made = [];
Object.keys(groups).forEach(function (key) {
  var box = document.createElement("div"); box.style.display = "none"; document.body.appendChild(box);
  var cols = JSON.parse(JSON.stringify(srcCols));   // 시트마다 복제 (공유하면 2번째 시트부터 헤더 유실)
  var s = IBSheet.create({ el: box, options: { Cfg: { Export: { Url: exportUrl } }, Cols: cols }, data: groups[key], sync: 1 });
  made.push({ sheet: s, key: key, box: box });
});

made[0].sheet.down2ExcelBuffer(true);               // 버퍼 시작
made.forEach(function (m, i) {
  var param = { sheetName: m.key };
  if (i === 0) param.fileName = "가계부.xlsx";       // 파일명은 첫 호출에만
  m.sheet.down2Excel(param);                         // 워크시트로 누적
});
made[0].sheet.down2ExcelBuffer(false);              // 버퍼 종료 (한 파일로 다운로드)
setTimeout(function () { made.forEach(function (m) { m.sheet.dispose(); m.box.remove(); }); }, 2000);
```

## Try it

- [Demo of exportData 그룹별 나눠 다운로드 (여러 파일 / 워크시트)](https://jsfiddle.net/gh/get/library/pure/ibsheet/ibsheet8-manual-sample/tree/master/samples/method/exportData/splitByGroup/)
- [Demo of down2Excel 그룹별 나눠 다운로드 (여러 파일 / 워크시트)](https://jsfiddle.net/gh/get/library/pure/ibsheet/ibsheet8-manual-sample/tree/master/samples/method/down2Excel/splitByGroup/)

## Read More

- [exportData method](/docs/funcs/core/export-data)
- [exportDataBuffer method](/docs/funcs/core/export-data-buffer)
- [down2Excel method](/docs/funcs/excel/down-to-excel)
- [down2ExcelBuffer method](/docs/funcs/excel/down-to-excel-buffer)

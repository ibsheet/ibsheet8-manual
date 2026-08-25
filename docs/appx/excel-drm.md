# 엑셀 DRM 처리 ***(appendix)***

<!-- synonyms: DRM, 문서보안, DRM 복호화, DRM 해제, DRM 적용, 엑셀 DRM, 엑셀 문서보안 -->

> 엑셀 업로드/다운로드 시 DRM(문서보안)이 적용된 파일을 처리하는 방법입니다.  
> DRM은 IBSheet 자체 옵션이 아니라 서버(백엔드) 처리 단계에서 적용하며, 서버 모듈(jsp/aspx)에 로직을 직접 넣어 구현합니다.  
> 서버 모듈([loadExcel](/docs/funcs/excel/load-excel))과 클라이언트 모듈([importData](/docs/funcs/core/import-data))은 동작 방식이 다르므로 DRM 처리 방법도 다릅니다.

## 서버 모듈 파일 위치

`LoadExcel.jsp`, `Down2Excel.jsp` 등 서버 모듈 파일은 시트 생성 시 지정한 `Cfg.Export.Url` 경로에 있습니다.

```javascript
options.Cfg = {
    Export: { Url: "/assets/ibsheet/jsp" }   // 이 경로 아래에 LoadExcel.jsp, Down2Excel.jsp 등이 위치
};
```

## 1. loadExcel / directLoadExcel 업로드 시 DRM 해제 (서버 모듈)

DRM이 걸린 파일이 서버로 전송되므로, `LoadExcel.jsp`(또는 `DirectLoadExcel.jsp`)의 `/** ~ **/` 부분을 주석 해제하고 `TODO` 위치에 DRM 복호화 로직을 삽입한 뒤, `loadFile` 함수로 DRM이 해제된 파일을 읽도록 처리합니다. 두 jsp 모두 동일한 파일 가공 구간이 제공됩니다.

```java
/** 서버로 전송된 파일을 가공해서 사용해야 할 경우. (예, DRM 복호화 등)
    // 서버에 저장된 파일 객체
    File uploadFile = load.getUploadFile();
    String uploadFileName = uploadFile.getName();
    String uploadFilePath = uploadFile.getAbsolutePath();

    // TODO
    // 업로드된 엑셀 파일을 가공함 (예, 엑셀문서를 DRM 처리함)

    // 가공된 파일을 ibSheet에서 읽을 수 있도록 처리. 2번째 인자를 true로 설정하면 파일을 읽은 후 파일 삭제
    load.loadFile(uploadFile, true);
**/

// 브라우저에 데이터를 전달하여 시트에 로드
load.writeToBrowser();
```

## 2. importData 업로드 시 DRM 해제 (클라이언트 모듈)

프론트엔드에서 DRM이 해제된 엑셀 파일의 Blob 데이터를 확보한 경우, `importData` 함수의 `file` 인자에 그 Blob 객체를 전달하여 시트에 데이터를 로드합니다.

```javascript
sheet.importData({
    file: blob   // DRM 해제된 엑셀 파일의 Blob 객체
});
```

## 3. down2Excel / directDown2Excel 다운로드 시 DRM 적용 (서버 모듈)

생성된 엑셀 문서를 DRM 처리하려면, `Down2Excel.jsp`(또는 `DirectDown2Excel.jsp`)의 기본 방식인 "다운로드 1"(`down.downToBrowser()`)을 주석 처리하고, "다운로드 2"(서버에 저장 후 전송) 방식으로 변경합니다.  
`down.saveToFile()`로 저장된 파일을 DRM 처리한 뒤 스트림으로 전송합니다.  
두 jsp 모두 동일한 "다운로드 2" 구간이 제공됩니다.

```java
// 다운로드 1. 생성된 문서를 브라우저를 통해 다운로드
//down.downToBrowser();   // DRM 적용 시 주석 처리

// 다운로드 2. 생성된 엑셀 문서를 서버에 저장
String fileName = down.getFileName();
down.setFileHeader();
down.saveToFile("d:/");

// 저장된 엑셀 문서를 DRM 처리 (이 위치에서 DRM 적용)
File file = new File("d:/" + fileName);

// 서버에 저장된(DRM 처리된) 파일을 스트림으로 전송하여 다운로드
FileInputStream fileIn = null;
ServletOutputStream out3 = null;
try {
    if (file.isFile()) {
        response.setContentLength((int) file.length());
        fileIn = new FileInputStream(file);
        out3 = response.getOutputStream();
        byte[] buffer = new byte[8192];
        int bytesRead;
        while ((bytesRead = fileIn.read(buffer)) != -1) {
            out3.write(buffer, 0, bytesRead);
        }
        out3.flush();
    }
} finally {
    if (fileIn != null) { try { fileIn.close(); } catch (Exception e) {} }
    if (out3 != null)   { try { out3.close(); }   catch (Exception e) {} }
    if (file != null && file.exists()) { file.delete(); }
}
```

> DRM 복호화/적용 로직 자체는 사용 중인 DRM 솔루션에 따라 다르므로, DRM 업체에 문의하여 소스 코드를 받아 적용합니다.

### Read More
- [loadExcel method](/docs/funcs/excel/load-excel)
- [down2Excel method](/docs/funcs/excel/down-to-excel)
- [importData method](/docs/funcs/core/import-data)
- [엑셀파일 업로드/다운로드 appendix](/docs/appx/import-export)

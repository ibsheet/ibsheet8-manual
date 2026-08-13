# 엑셀파일 업로드/다운로드  ***(appendix)***

<!-- synonyms: 엑셀 다운로드, 엑셀 업로드, 엑셀 파일 저장, 서버 엑셀, down2Excel, loadExcel, directDown2Excel, directLoadExcel, 텍스트 다운로드, PDF 다운로드, 한글 hwpx, POI, 서버 모듈, 서버 모듈 설치, 환경 설정, 환경 셋팅, 서버 셋팅, jar 설치, 라이브러리 설정, Maven 설정, pom 설정, 필요 파일, excel download upload, server setup -->

> 시트의 내용을 엑셀이나 텍스트 파일로 다운로드하거나, 반대로 파일의 내용을 읽어 시트에 업로드하는 방법과 이를 위한 **서버 환경 셋팅**을 설명합니다.  
> **이 내용은 서버 기반 파일 다운로드/업로드 방법입니다.**  
> **클라이언트 기반 다운로드/업로드는 [exportData](/docs/funcs/core/export-data) / [importData](/docs/funcs/core/import-data) 함수를 참고하세요.**

## 필수 파일 요소
업로드/다운로드 작업을 **서버(백엔드)에서 처리**하려면 다음과 같은 파일이 필요합니다. 서버모듈이 브라우저가 보낸 시트 데이터를 실제 엑셀/텍스트/PDF 파일로 생성하거나, 업로드된 파일을 파싱해 시트로 넘깁니다.

### 1. 서버모듈 (엑셀 모듈)

- Java 이용시 필요 파일 (POI 5.4.1 기준)

> **서버모듈 사양**: JDK `1.8` 이상, Dynamic Web Module `3.1` 이상

|파일명|용도|
|---|---|
|ibsheet8-x.x.x.jar|엑셀 서버코어모듈|
|ibsheet8-hwpx-x.x.x.jar|`down2Hwpx` 서버코어모듈|
|poi-5.4.1, poi-ooxml-5.4.1, poi-ooxml-lite-5.4.1|엑셀 파일 생성/파싱 모듈|
|commons-collections4-4.4.jar, commons-compress-1.27.1.jar<br/>commons-math3-3.6.1.jar, curvesapi-1.08.jar, servlet-api.jar<br/>SparseBitSet-1.3.jar, xmlbeans-5.3.0.jar |poi 이용시 필요 파일|
|commons-codec-1.18.0.jar|엑셀 업로드 관련 인코딩 모듈, `down2Hwpx`시 필요|
|log4j-api-2.24.3.jar|로그 모듈|
|ib-itext.jar|pdf 다운로드 모듈|
|batik-all-1.17.jar, commons-io-2.18.0.jar<br/>xml-apis-ext-1.3.04.jar, xmlgraphics-commons-2.9.jar<br/>|이미지 처리 관련 모듈, `down2Hwpx`시 필요|

- dotnet 4.0 이용시 필요 파일

|파일명|용도|
|---|---|
|IBSheet8-4.0.dll|엑셀 서버코어모듈|
|IBSheet8-4.0.resources.dll|엑셀 서버코어 서브모듈|
|Syncfusion.Compression.Base.dll, Syncfusion.Core.dll,<br/>Syncfusion.XlsIO.Base.dll|엑셀 생성/파싱 모듈|
|wkhtmltopdf.exe|pdf생성 모듈|

### 2. jsp, aspx 파일

각 기능은 대응하는 jsp(닷넷은 aspx) 파일이 서버에 있어야 동작합니다. 이 파일들은 서버코어모듈(Java `ibsheet8-x.x.x.jar`, 닷넷 `IBSheet8-x.x.dll`)을 사용해 구현되어 있습니다.  Java 서버모듈의 API(`IBSheetDown` / `IBSheetLoad` / `Print2Pdf`)와 커스터마이즈 방법은 [서버모듈 함수](/docs/appx/server-module-functions)를 참고하세요.  
제공받은 파일을 웹 서버 폴더에 복사하고 `Cfg.Export.Url`로 경로를 지정합니다. (설정은 아래 **준비 과정** 참고)

|파일명|용도|
|---|---|
|Down2Excel.jsp(aspx)|화면 시트 데이터를 엑셀로 다운로드|
|LoadExcel.jsp(aspx)|엑셀파일을 화면 시트로 업로드|
|DirectDown2Excel.jsp(aspx)|DB에서 조회한 데이터를 서버에서 바로 엑셀로 다운로드|
|DirectLoadExcel.jsp(aspx)|업로드한 엑셀 데이터를 서버(DB 등)에 바로 적용|
|Down2Text.jsp(aspx)|텍스트파일 다운로드|
|LoadText.jsp(aspx)|텍스트파일 업로드|
|Down2Pdf.jsp(aspx)|PDF파일 다운로드|
|Down2Hwpx.jsp|한글(Hwpx) 파일 다운로드 (닷넷 미지원)|

## Maven 의존성 설정

Maven을 사용하는 경우 `pom.xml`에 아래 의존성을 추가합니다. (POI `5.4.1` 기준) POI 계열과 이미지 처리 라이브러리를 명시적으로 지정하며, IBSheet 코어 모듈(`ibsheet8`)과 PDF 다운로드용 `ib-itext`는 공개 Maven 저장소에 없으므로 `system` scope로 `WEB-INF/lib`의 jar 경로를 직접 지정합니다.

```xml
<dependencies>
    <!--이미지 처리 관련 JAR-->
    <dependency>
        <groupId>org.apache.xmlgraphics</groupId>
        <artifactId>batik-all</artifactId>
        <version>1.17</version>
        <type>pom</type>
    </dependency>
    <dependency>
        <groupId>commons-io</groupId>
        <artifactId>commons-io</artifactId>
        <version>2.18.0</version>
    </dependency>
    <dependency>
        <groupId>xml-apis</groupId>
        <artifactId>xml-apis-ext</artifactId>
        <version>1.3.04</version>
    </dependency>
    <dependency>
        <groupId>org.apache.xmlgraphics</groupId>
        <artifactId>xmlgraphics-commons</artifactId>
        <version>2.9</version>
    </dependency>

    <!--엑셀 처리 관련 JAR-->
    <dependency>
        <groupId>commons-codec</groupId>
        <artifactId>commons-codec</artifactId>
        <version>1.18.0</version>
    </dependency>
    <dependency>
        <groupId>org.apache.commons</groupId>
        <artifactId>commons-collections4</artifactId>
        <version>4.4</version>
    </dependency>
    <dependency>
        <groupId>org.apache.commons</groupId>
        <artifactId>commons-compress</artifactId>
        <version>1.27.1</version>
    </dependency>
    <dependency>
        <groupId>org.apache.logging.log4j</groupId>
        <artifactId>log4j-api</artifactId>
        <version>2.24.3</version>
    </dependency>
    <dependency>
        <groupId>org.apache.commons</groupId>
        <artifactId>commons-math3</artifactId>
        <version>3.6.1</version>
    </dependency>
    <dependency>
        <groupId>com.github.virtuald</groupId>
        <artifactId>curvesapi</artifactId>
        <version>1.08</version>
    </dependency>
    <dependency>
        <groupId>org.apache.poi</groupId>
        <artifactId>poi</artifactId>
        <version>5.4.1</version>
    </dependency>
    <dependency>
        <groupId>org.apache.poi</groupId>
        <artifactId>poi-ooxml</artifactId>
        <version>5.4.1</version>
    </dependency>
    <dependency>
        <groupId>org.apache.poi</groupId>
        <artifactId>poi-ooxml-lite</artifactId>
        <version>5.4.1</version>
    </dependency>
    <dependency>
        <groupId>com.zaxxer</groupId>
        <artifactId>SparseBitSet</artifactId>
        <version>1.3</version>
    </dependency>
    <dependency>
        <groupId>org.apache.xmlbeans</groupId>
        <artifactId>xmlbeans</artifactId>
        <version>5.3.0</version>
    </dependency>

    <!--IBSheet 코어 모듈 (공개 저장소에 없음 → system scope)-->
    <dependency>
        <groupId>ibsheet.ui</groupId>
        <artifactId>ibsheet8</artifactId>
        <version>x.x.x</version>
        <scope>system</scope>
        <systemPath>${basedir}/src/main/webapp/WEB-INF/lib/ibsheet8-x.x.x.jar</systemPath>
    </dependency>
    <dependency>
        <groupId>ib-itext</groupId>
        <artifactId>ib-itext</artifactId>
        <version>1.0</version>
        <scope>system</scope>
        <systemPath>${basedir}/src/main/webapp/WEB-INF/lib/ib-itext.jar</systemPath>
    </dependency>
</dependencies>
```

IBSheet 코어(`ibsheet8`)와 `ib-itext`의 `version`, `systemPath`는 실제 사용 중인 jar 파일명과 경로에 맞게 지정하세요.

## 준비 과정

### 플러그인 파일 include
다운로드/업로드 작업을 하는 모든 페이지에 `/plugins/ibsheet-excel.js`를 include 해야 합니다.

### jsp 파일경로 설정
시트 생성시 Cfg 프로퍼티에 `Export.Url` 속성을 통해 jsp 파일이 위치한 경로를 설정해야 합니다.

```json
options.Cfg = {
    "Export":{
        "Url":"/assets/ibsheet/jsp"
    }
}
```

## 기능 구현
[down2Excel](/docs/funcs/excel/down-to-excel)이나 [loadText](/docs/funcs/excel/load-text)함수를 통해 시트의 내용을 다운로드/업로드 하실 수 있습니다.<br>

```javascript
sheet.down2Excel({"fileName":"boardList.xlsx","sheetDesign":1,"merge":1});
```
![down2Excel](/assets/imgs/down2Excel.png)<br>

업로드/다운로드 함수에 대한 자세한 기능은 해당 함수에 대한 메뉴얼 파트를 참고해 주세요.

## 서버모듈 확인 방법(엑셀 모듈)

서버모듈과 관련 라이브러리(POI 등)가 정상적으로 로드됐는지는, 다운로드 처리 jsp(예: `Down2Excel.jsp`)에 아래 구문을 추가한 뒤 화면에서 `down2Excel`을 호출해 서버 콘솔 출력으로 확인합니다.

```jsp
<%
System.out.println(com.ibleaders.ibsheet8.util.Version.getVersion());
%>
```

정상이면 서버 콘솔에 다음과 같이 서버모듈 버전과 로드된 jar의 경로/버전이 출력됩니다. (각 jar의 버전 정보를 확인하세요.)

```console
********************************************************************************
# ibsheet8-x.x.X
# IBSheet(H) 8.0.0.0~
# IBChart(H) 7.3.0.1~
********************************************************************************
Class Info  : org.apache.poi.ss.usermodel.Workbook
jar path    : /D:/tomcat/tomcat-8.5_servertest/webapps/ibsheet8_demo_test/WEB-INF/lib/poi-5.4.1.jar
jar Version : Apache POI 5.4.1
Required Version : POI 3.8 beta3 or later
********************************************************************************
Class Info  : org.apache.poi.ooxml.POIXMLDocument
jar path    : /D:/tomcat/tomcat-8.5_servertest/webapps/ibsheet8_demo_test/WEB-INF/lib/poi-ooxml-5.4.1.jar
jar Version : Apache POI 5.4.1
Required Version : POI 3.8 beta3 or later
********************************************************************************
Class Info  : org.openxmlformats.schemas.spreadsheetml.x2006.main.CTWorkbookPr
jar path    : /D:/tomcat/tomcat-8.5_servertest/webapps/ibsheet8_demo_test/WEB-INF/lib/poi-ooxml-lite-5.4.1.jar
jar Version : Apache POI 5.4.1
Required Version : POI 3.8 beta3 or later
********************************************************************************
Class Info  : org.openxmlformats.schemas.spreadsheetml.x2006.main.CTWorkbook
jar path    : /D:/tomcat/tomcat-8.5_servertest/webapps/ibsheet8_demo_test/WEB-INF/lib/poi-ooxml-lite-5.4.1.jar
jar Version : Apache POI 5.4.1
Required Version : POI 3.8 beta3 or later
********************************************************************************
Class Info  : org.apache.xmlbeans.XmlBeans
jar path    : /D:/tomcat/tomcat-8.5_servertest/webapps/ibsheet8_demo_test/WEB-INF/lib/xmlbeans-5.3.0.jar
jar Version :
Required Version : XMLBeans 2.3.0 or later
********************************************************************************
POI Core Library file:/D:/tomcat/tomcat-8.5_servertest/webapps/ibsheet8_demo_test/WEB-INF/lib/poi-5.4.1.jar
POI OOXML Library file:/D:/tomcat/tomcat-8.5_servertest/webapps/ibsheet8_demo_test/WEB-INF/lib/poi-ooxml-5.4.1.jar
```

또한 다운로드 처리 jsp의 `IBSheetDown`에 `setLog(true)`를 설정하면, 실제 다운로드가 실행될 때 서버 콘솔에 처리 로그(처리 시점의 JVM 메모리, 파일 정보, 소요 시간 등)가 출력됩니다. 로그에 **`excel mode=POI`** 가 보이면 POI 라이브러리가 정상 로드되어 동작 중인 것입니다.

```console
Debug: ibsheet8-x.x.X
Debug: Down2Excel start...
Debug: [2026.08.11 12:50:43] Max:7,574,388,736, Total:3,020,947,456, Free:697,302,304, Used:2,323,645,152
Debug: fileName=Excel.xlsx, fileType=xlsx
Debug: excel mode=POI
Debug: ##  전문분석 소요시간 : 0.002초
Debug: ##  다운로드 총 소요시간 : 0.003초
Debug: Down2Excel End...
```

### Read More
- [서버모듈 함수 appendix](/docs/appx/server-module-functions)
- [Export cfg](/docs/props/cfg/export)
- [DirectDown2Excel method](/docs/funcs/excel/direct-down-to-excel)
- [DirectLoadExcel method](/docs/funcs/excel/direct-load-excel)
- [down2Excel method](/docs/funcs/excel/down-to-excel)
- [Down2Hwpx method](/docs/funcs/excel/down-to-hwpx)
- [loadExcel method](/docs/funcs/excel/load-excel)
- [down2Text method](/docs/funcs/excel/down-to-text)
- [loadText method](/docs/funcs/excel/load-text)
- [down2Pdf method](/docs/funcs/excel/down-to-pdf)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.1.0.85|Down2Hwpx 기능 추가|
|excel|1.1.2|Down2Hwpx 기능 추가|
|jar|1.0.0|Down2Hwpx 기능 추가|

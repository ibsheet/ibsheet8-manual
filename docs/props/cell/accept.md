# Accept ***(cell)***

<!-- synonyms: Accept, 파일 형식 제한, 업로드 허용 형식, 파일 확장자 제한, MIME 타입, 파일 필터, 업로드 필터, 첨부 파일 형식, file type filter, upload accept, mime type, file extension -->

> [File Type](/docs/appx/file-type-upload) 셀에 업로드를 허용할 파일 형식을 지정하는 속성입니다.
>
> `input type="file"` 의 accept 속성과 동일하게 동작합니다.


### Type
`string`

### Options
|Value|Description|
|-----|-----|
|`string`|[File Type](/docs/appx/file-type-upload) 셀에 업로드를 허용할 파일 형식을 지정|


### Example
```javascript
// Type: File인 셀에 이미지 파일만 업로드 하도록 설정
sheet.setAttribute(sheet.getRowById("AR99"), "FileUpload", "Accept", 'image/*');
```

### Read More
* [File Type 업로드](/docs/appx/file-type-upload)
* [Accept Col](/docs/props/col/accept)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|

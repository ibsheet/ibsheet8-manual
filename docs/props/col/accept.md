# Accept ***(col)***

<!-- synonyms: 파일 형식, 업로드 허용 형식, 확장자 제한, 파일 타입 제한, MIME 타입, 파일 필터, file accept, upload filter, file extension, mime type, allowed files -->

> [File Type](/docs/appx/file-type-upload) 컬럼에 업로드를 허용할 파일 형식을 지정하는 속성입니다.
>
> `input type="file"` 의 accept 속성과 동일하게 동작합니다.


### Type
`string`

### Options
|Value|Description|
|-----|-----|
|`string`|[File Type](/docs/appx/file-type-upload) 컬럼에 업로드를 허용할 파일 형식을 지정|


### Example
```javascript
// Type: File인 컬럼에 이미지 파일만 업로드 하도록 설정
options.Cols = [
    ...
    {Type: "File", Name: "CarName", Width: 120, Accept: 'image/*' ...},
    ...
];
```

### Read More
* [File Type 업로드](/docs/appx/file-type-upload)
* [Accept Cell](/docs/props/cell/accept)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|

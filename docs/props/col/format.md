# Format ***(col)***

<!-- synonyms: 표시 포맷, 화면 표시 형식, 데이터 포맷, 셀 포맷, 표시 형식, display format, cell format, number format, date display format -->

> 데이터를 IBSheet에 표시할 때 적용되는 **표시 포맷**(display format)을 설정합니다.  
> 원본 데이터 값은 변경되지 않으며 화면에 표시되는 값에만 적용됩니다.  
> `Format`은 열의 [Type](./type)에 따라 다양한 방식으로 정의할 수 있습니다.  
> **자세한 내용은 appendix의 [Format](/docs/appx/format)을 참고해 주세요.**

### Type
`mixed`( `string` \| `object` )

### Options
|Value|Description|
|-----|-----|
|`string` \| `object`|열의 `Type`에 따른 다양한 포맷 설정 문자열|


### Example
```javascript
//1. 날짜 포맷을 정의합니다.
options.Cols = [
    {
     Type: "Date", 
     Name: "Edate", 
     Format: 'MM-dd-yyyy'
    }
    
];

//2. 메소드를 통해 특정 셀의 Format 변경
sheet.setAttribute("", "EDate", "Format", "MM-dd-yyyy");

```

### Read More
- [Format appendix](/docs/appx/format)
- [CustomFormat col](./custom-format)
- [EditFormat col](./edit-format)
- [DataFormat col](./data-format)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|

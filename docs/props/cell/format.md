# Format ***(cell)***
> 데이터를 IBSheet에 표시할 때 적용되는 **표시 포맷(display format)** 을 설정합니다.  
> 원본 데이터 값은 변경되지 않으며 화면에 표시되는 값에만 적용됩니다.  
> `Format`은 셀의 [Type](/docs/appx/type)에 따라 다양한 방식으로 정의할 수 있습니다.  
> **자세한 내용은 appendix의 [Format](/docs/appx/format)을 참고해 주세요.**

### Type
`mixed`( `string` \| `object` )

### Options
|Value|Description|
|-----|-----|
|`string` \| `object`|셀의 `Type`에 따라 정의되는 포맷 설정 값|


### Example
```javascript
//1. 메소드를 통해 특정 셀의 Format 변경
sheet.setAttribute( sheet.getRowById("AR9") , "EDate" , "Format" ,"dd.MM.yyyy");


//2. 객체에 직접 접근하여 Format 변경
var ROW = sheet.getRowById("AR10");
ROW["EDateFormat"] = "dd.MM.yyyy";

//변경내용 반영
sheet.refreshCell({row:ROW, col:"EDate"});


//3. 조회 데이터 내에서 Format 변경
{
    data:[
        { "EDateFormat":"dd.MM.yyyy" }
    ]
}
```

### Read More
- [Format appendix](/docs/appx/format)
- [DataFormat cell](./data-format)
- [EditFormat cell](./edit-format)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|

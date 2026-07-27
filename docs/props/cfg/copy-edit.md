# CopyEdit ***(cfg)***
> `Ctrl + C`로 셀 값을 복사할 때,
> **화면에 보이는 값**(`Format`) 기준으로 복사할지,  
> **편집 시 실제 값**(`EditFormat`) 기준으로 복사할지 설정합니다.  
>
> IBSheet 내부에서 복사한 값을 다시 IBSheet에 붙여넣는 경우에는
> `EditFormat` 기준 복사가 적합합니다.


<!-- synonyms: copy format, copy edit format, clipboard format, 복사 포맷 설정, 화면 표시값 복사, 편집값 복사 -->



### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`0`|화면에 보이는 값(`Format`) 기준으로 복사<br/>`CustomFormat`이 설정된 경우 우선 적용|
|`1`|편집 시 실제 값(`EditFormat`) 기준으로 복사 (`default`)|


### Example
```javascript
options = {
    "Cfg":{
      "CopyEdit": 0,  // 화면에 보이는 값 기준으로 복사
    }
};
```

### Read More
- [Format col](/docs/props/col/format)
- [CustomFormat col](/docs/props/col/custom-format)
- [EditFormat col](/docs/props/col/edit-format)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|

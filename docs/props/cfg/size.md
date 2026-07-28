# Size ***(cfg)***

> 각 행의 최소 높이와 폰트 크기, 그리고 달력이나 드롭다운 같은 기본 컨트롤 아이콘 크기를 함께 설정합니다.  
> 시트 생성 시 기본 행 높이는 `30px` 이며, 이보다 줄이려면 `Size` 속성을 통해 더 작게 설정해야 합니다.  
> 표의 높이는 각 `Size`의 최소 높이이며, 이보다 크게 만들려면 [Height](/docs/props/row/height)로 늘릴 수 있습니다(데이터 행은 `Def.Row`, 헤더 행은 `Def.Header`에 지정).  
> 다만 `Height`로도 지정한 `Size`의 최소 높이보다 작게는 줄일 수 없습니다(예: `Small`은 `22px` 미만 불가).


### Type
`string`

### Options
|Value|Description|
|-----|-----|
|`Tiny`|최소 행 높이 `20px`, 폰트 크기 `13px`|
|`Small`|최소 행 높이 `22px`, 폰트 크기 `13px`|
|`Low`|최소 행 높이 `27px`, 폰트 크기 `13px`|
|`Normal`|최소 행 높이 `30px`, 폰트 크기 `13px` (`default`)|
|`High`|최소 행 높이 `42px`, 폰트 크기 `21px`|
|`Big`|최소 행 높이 `52px`, 폰트 크기 `21px`|

> 위 폰트 크기는 기본 테마(`main.css`) 기준입니다. 특정 폰트 크기가 필요하면 [TextSize](/docs/props/cell/text-size)로 따로 지정하세요.   
> 이때 `Def.Row`는 데이터 행에만 적용되므로, 헤더 폰트까지 바꾸려면 `Def.Header`에도 지정해야 합니다.


### Example
```javascript
options = {
    Cfg:{
      Size: "Small",  //기본보다 작게 설정
    },
    Def:{
      Row:{
        Height: 25  //원래 설정(22px)보다 약간 늘림
      }
    }
};
```

### Try it
- ["Normal" by default with setSize](https://jsfiddle.net/gh/get/library/pure/ibsheet/ibsheet8-manual-sample/tree/master/samples/properties/Cfg/Size/)

### Read More
- [Height row](/docs/props/row/height)
- [setSize](/docs/funcs/core/set-size)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.1|기능 추가|

# FitWidth ***(cfg)***

<!-- synonyms: FitWidth, fit width, dummy column, scroll bar right, full width, fill width, 너비 맞춤, 더미 컬럼, 스크롤바 우측, 시트 폭 맞춤, 가로 여백 채움, 세로 스크롤바 위치, 마지막 컬럼 여백 -->

> 마지막 컬럼 뒤에 더미 컬럼을 두어 세로 스크롤바를 우측 끝에 붙게 합니다. <br/>
> **주의 :`(Col)RelWidth`와 함께 설정 시 해당 속성은 무시되고 `RelWidth`가 우선 적용됩니다.**

###
[`FitWidth: false` 설정시]<br>
![FitWidth: false](/assets/imgs/fitWidth0.png "FitWidth: false")<br>

[`FitWidth: true` 설정시]<br>
![FitWidth: true](/assets/imgs/fitWidth1.png "FitWidth: true")<br>


### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|기능 사용 안함 (`default`)|
|`1(true)`|기능 사용|


### Example
```javascript
options.Cfg = {
    FitWidth: true    //더미 헤더를 추가하여 스크롤바를 우측 끝에 붙인다.
};

```

### Try it
- [True](https://jsfiddle.net/gh/get/library/pure/ibsheet/ibsheet8-manual-sample/tree/master/samples/properties/Cfg/FitWidth-true/)

### Read More


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|

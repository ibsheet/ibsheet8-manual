# StandardTip ***(cfg)***

<!-- synonyms: StandardTip, standard tip, native tooltip, browser tooltip, sheet tooltip, tip mode, 툴팁 방식, 브라우저 툴팁, 시트 내장 툴팁, 팁 다이얼로그, TipPosition TipClass, 툴팁 렌더링 방식 -->

> 툴팁을 시트 내장 다이얼로그로 보여줄지, 브라우저의 툴팁으로 보여줄지 설정합니다.
>
> 시트 내장 다이얼로그로 설정한 경우 [TipPosition](/docs/props/col/tip-position), [TipClass](/docs/props/col/tip-class) 들을 적용할 수 있습니다.


### Type
`boolean`


### Options
|Value|Description|
|-----|-----|
|`0(false)`|시트 내장 다이얼로그로 툴팁 표시 (`default`)|
|`1(true)`|표준 브라우저 툴팁으로 표시|


### Example
```javascript
options.Cfg = {
   StandardTip: true
};
```

### Read More
- [TipPosition col](/docs/props/col/tip-position)
- [TipClass col](/docs/props/col/tip-class)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|

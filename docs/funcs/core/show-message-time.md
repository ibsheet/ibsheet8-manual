# showMessageTime ***(method)***
> 시트 영역 가운데에 특정 시간동안 메세지 `Dialog`를 띄웁니다.
> <br/>특정 시간 이후에는 자동으로 메세지가 `Dialog` 가 닫힙니다.
> <br/>**`time` 속성을 설정하지 않으면 메세지 아래 반투명 레이어가 생기고 확인 버튼을 누를때까지 닫히지 않습니다. (alert같이 동작)**
> <br/>`type` 속성은 `time` 속성을 설정하지 않으면 `1(true)`이 기본으로 동작하고, `time` 속성을 설정하면 `0(false)`이 기본으로 동작한다
> 메세지 `Dialog` 오픈 전에 [onShowMessage event](/docs/events/on-show-message) 이벤트가 발생합니다.

###
![showMessageTime](/assets/imgs/showMessageTime.png "showMessageTime")

### Syntax
```javascript
void showMessageTime( message, time, func, buttons, importance, type );
```

### Parameters
|Name|Type|Required| Description |
|----------|-----|---|----|
|message|`string`|<span class='required'>필수</span>|시트 위에 다이얼로그 형태로 보여질 메세지 내용|
|time|`number`|<span class='optional'>선택</span>|메세지가 보여질 시간(ms단위). 설정을 안하거나 `0`으로 설정시 계속 보여짐|
|func|`function`|<span class='optional'>선택</span>|메세지에서 표시되는 버튼을 눌렀을 때 콜백함수<br>버튼의 순서대로 `1,2,3,4` 숫자가 `args`로 넘어옴<br>ex)<br> `func`:function(args) {<br>&nbsp;&nbsp;if(args===1){alert('첫번째버튼 클릭'}<br> }|
|buttons|`array[string]`|<span class='optional'>선택</span>|메세지가 표시될때 같이 보여질 버튼들 정의<br>ex)<br> `buttons`:['계속', '중단']|
|importance|`number`|<span class='optional'>선택</span>|메세지 중요도 (시트 초기화시 `Cfg`설정에 `SuppressMessage`(`default: 3`) 속성값보다 커야만 화면에 보여짐)|
|type|`number`|<span class='optional'>선택</span>|메세지 다이얼로그 생성시 시트 위에 반투명한 레이어로 덮을지 여부<br>`0`:안덮음 (`default`)<br>`1`:덮음|


### Return Value
***none***

### Example
```javascript
function popup() {
    sheet.showMessageTime({
        message: "<span style='color:black'>상신하시겠습니까?</span>",
        time: 10000,
        buttons: ["OK", "취소"],
        func: function (args) {
            if (args==1) {
                //OK에 대한 처리
            } else if (args==2) {
                //취소에 대한 처리
            }
        }
    });
}
```
### Read More
- [CenterMessage](/docs/props/cfg/center-message) 
- [SuppressMessage cfg](/docs/props/cfg/suppress-message)
- [showMessage method](./show-message)
- [hideMessage method](./hide-message)
- [onShowMessage event](/docs/events/on-show-message)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.0.0.27|`type` 기능 추가|

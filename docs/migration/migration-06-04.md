# AcceptKeys/ExceptKeys 마이그레이션

`AcceptKeys`와 `ExceptKeys`는 둘다 특정 문자에 대한 입력만 허용하거나 불허하는 기능입니다.
IBSheet7에서는 `E(영문)`, `N(숫자)`, `K(한글)` 와 같은 예약어와 함께 특정 원하는 문자를 다음과 같이 설정하였습니다.

```javascript
//AS-IS
var Cols = [
    //AcceptKeys 예          영문자,숫자,-(기호)만 허용
    {Type:"Text", Name:"SA_NO", AcceptKeys:"E|N|[-]" },

    //ExceptKeys 예          영문자와 !,@,# 는 입력 불가
    {Type:"Text", Name:"SA_PRT", ExceptKeys:"E|[!@#]" }
];
```

```javascript
///TO-BE
opt.Cols = [
    //AcceptKeys 대신 EditMask를 이용하여 영문자,숫자,-(기호)만 허용
    {Type:"Text", Name:"SA_NO", EditMask:"^[a-zA-Z|\\d|\\-]*$" },

    //ExceptKeys 대신 EditMask를 이용하여 영문자와 !,@,# 는 입력 불가
    {Type:"Text", Name:"SA_PRT", EditMask:"^[^a-zA-Z|^!|^@|^#]*$" }
];
```
정규식이 익숙하지 않다면 [onBeforeCreate (static)](/docs/static/on-before-create)에서 기존 `AcceptKeys`, `ExceptKeys` 설정을 [EditMask (col)](/docs/props/col/edit-mask)로 자동 변환하는 공통 로직을 둘 수도 있습니다.

아래 로직을 참고해 주세요.

```javascript
//시트 생성 직전에 발생하는 이벤트(IBSheet.create함수에 넣은 인자가 opt안에 모두 들어있음.)
IBSheet.onBeforeCreate = function(opt){
    var acceptExceptKeysMig = function(Cols){

        for(var i = 0; i < Cols.length; i++) {
            var c = Cols[i];

            //EditMask를 통해 AcceptKeys를 유사하게 구현한다.
            if (c["AcceptKeys"]) {

                var setV = c["AcceptKeys"];
                var acceptKeyArr = setV.split("|");
                var mask = "";

                for (var i = 0; i < acceptKeyArr.length; i++) {
                    switch (acceptKeyArr[i]) {
                    case "E":
                        mask += "|a-zA-Z";
                        break;
                    case "N":
                        mask += "|\\d";
                        break;
                    case "K":
                        mask += "|\\u3131-\\u314e\\u314f-\\u3163\\uac00-\\ud7a3";
                        break;
                    default:
                        if (acceptKeyArr[i].substring(0, 1) == "[" && acceptKeyArr[i].substring(acceptKeyArr[i].length-1) == "]") {
                            var otherKeys = acceptKeyArr[i].substring(1, acceptKeyArr[i].length-1);
                            for (var x = 0; x < otherKeys.length; x++) {
                                if ([".","-","$","^","*","+","|","(",")"].indexOf(otherKeys[x]) > -1) {
                                    mask += "|\\" + otherKeys[x];
                                } else {
                                    mask += "|" + otherKeys[x];
                                }
                            }
                        }
                        break;
                    }
                }
                c.EditMask = "^[" + mask.substring(1) + "]*$";

            //EditMask를 통해 ExceptKeys를 유사하게 구현한다.
            } else if(c["ExceptKeys"]) {

                var setV = c["ExceptKeys"];
                var acceptKeyArr = setV.split("|");
                var mask = "";

                for (var i = 0; i < acceptKeyArr.length; i++) {
                    switch (acceptKeyArr[i]) {
                    case "E":
                        mask += "|^a-zA-Z";
                        break;
                    case "N":
                        mask += "|^\\d";
                        break;
                    case "K":
                        mask += "|^\\u3131-\\u314e\\u314f-\\u3163\\uac00-\\ud7a3";
                        break;
                    default:
                        if (acceptKeyArr[i].substring(0, 1) == "[" && acceptKeyArr[i].substring(acceptKeyArr[i].length-1) == "]") {
                            var otherKeys = acceptKeyArr[i].substring(1, acceptKeyArr[i].length-1);
                            for (var x = 0; x<otherKeys.length; x++) {
                                if ([".","-","$","^","*","+","|","(",")"].indexOf(otherKeys[x]) > -1) {
                                    mask += "|^\\" + otherKeys[x];
                                } else {
                                    mask += "|^" + otherKeys[x];
                                }
                            }
                        }
                        break;
                    }
                }
                c.EditMask = "^[" + mask.substring(1) + "]*$";
            }
        }
    }

    acceptExceptKeysMig(opt.options.Cols);
    if(opt.options.LeftCols) acceptExceptKeysMig(opt.options.LeftCols);
    if(opt.options.RightCols) acceptExceptKeysMig(opt.options.RightCols);

    //반드시 수정된 opt를 리턴해야 시트가 만들어짐.
    return opt;
}
```

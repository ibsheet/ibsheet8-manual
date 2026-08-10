# DelCheck 타입 마이그레이션

<!-- synonyms: IBSheet7, 마이그레이션, sheet7, migration, v7, v8, ibsheet7에서 ibsheet8로, DelCheck, DelCheck 타입, DelCheck 컬럼, 삭제 체크박스, delete check, 행 삭제 체크 -->

열 생성시 [OnChange (json event)](/docs/props/event/on-change)를 통해 값에 따라 행의 상태를 변경하는 로직을 넣어 줍니다.

`IBSheet-common.js` 파일에 `IB_Preset.DelCheck`를 (Col)[Extend](/docs/props/col/extend)하시면 됩니다.

```javascript
var initSheet = {
    Cols:[
        //DelCheck 열 처럼 동작하는 열을 만든다.
        {
            Header:"삭제",
            Name:"DEL",
            Extend: IB_Preset.DelCheck
        }
    ]
};
```

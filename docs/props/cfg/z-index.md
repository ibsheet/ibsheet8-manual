# ZIndex ***(cfg)***

<!-- synonyms: z-index, z index, zindex, 겹침 순서, 쌓임 순서, stacking order, 모달 위 시트, 팝업 가림, 달력 안보임, 드롭다운 가림, 다이얼로그 안보임, 메시지 가림 -->

> 시트와 시트의 팝업 다이얼로그, 메세지, 커서들에 대한 `css z-index` 기준 값을 설정합니다.
>
> 기준 값 설정 시 시트에 속한 객체들은 `Zindex ~ Zindex+20` 까지의 `css z-index` 를 가지게 됩니다.  
> 시트를 **모달/팝업 위에 표시**할 때 특히 필요합니다. 시트의 팝업 요소(달력, `Enum` 드롭다운, 다이얼로그, 메시지, 드래그 정보 등)는 각각 **별도의 `div`로 `body` 바로 아래에 그려지므로**, `ZIndex`를 지정하지 않으면 모달보다 z-index가 낮아 가려질 수 있습니다. 이 경우 `ZIndex`를 모달보다 높게 설정하세요.


### Type
`number`


### Options
|Value|Description|
|-----|-----|
|`number`|`ZIndex`로 가질 기준 값을 설정한다. |


### Example
```javascript
options.Cfg = {
   // 시트와 시트 내부 객체들의 z-index 기준값을 300 으로 설정
   // 내부 객체들은 최대 320 까지의 z-index 를 가짐
   ZIndex: 300,
   ...
};
```

### Read More

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|

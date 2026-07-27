# SuppressMessage ***(cfg)***

<!-- synonyms: 대기이미지, 로딩, 로딩바, 로딩 이미지, 블럭, 블록, 메시지 숨김, 메시지 표시, loading -->

> 시트에서 제공하는 상태 메시지들 중 표시하지 않을 메시지 종류에 대해 설정 합니다.  
> 기본값이 `3`이므로 조회/저장 시 메시지가 표시되지 않습니다.  
> 조회/저장 시 메시지를 표시하려면 `2`로 설정하세요.  
> 메시지는 기본적으로 시트 영역 중앙에 표시됩니다. 브라우저 화면 중앙에 표시하려면 [CenterMessage](./center-message)를 설정하세요.  
> 별도의 대기 이미지를 사용하려면 조회는 [onSearchStart](/docs/events/on-search-start) + [onSearchFinish](/docs/events/on-search-finish), 저장은 [onBeforeSave](/docs/events/on-before-save) + [onAfterSave](/docs/events/on-after-save) 이벤트에서 처리하세요.  
> 엑셀 다운로드/업로드 시 메시지는 [SuppressExportMessage](./suppress-export-message)에서 설정합니다.  
> **주의**: 한 화면에 시트가 여러 개인 경우, `SuppressMessage: 0` 설정 시 성능이 저하될 수 있습니다.



### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`0`|시트 내에서 발생하는 모든 메세지 표시|
|`1`|시트 로딩 및 업데이트시 생성되는 메시지 표시 안함. 렌더링 메세지는 표시됨.|
|`2`|1번 옵션 + 정렬과 같이 시트 내부 계산에 대한 정보 메세지 표시 안함 |
|`3`|2번 옵션 + 페이지 로딩 및 렌더링, 조회, 저장 메세지 표시 안함 (`default`)|
|`4`|3번 옵션 + 시트가 정상적으로 보여지지 않을 때의 에러 메세지 표시 안함 |


### Example
```javascript
options.Cfg = {
  SuppressMessage: 2,  // 조회/저장 시 메시지 표시
};
```

### Read More
- [CenterMessage cfg](./center-message)
- [SuppressExportMessage cfg](./suppress-export-message)
- [onSearchStart event](/docs/events/on-search-start)
- [onSearchFinish event](/docs/events/on-search-finish)
- [onBeforeSave event](/docs/events/on-before-save)
- [onAfterSave event](/docs/events/on-after-save)
- [showMessage method](/docs/funcs/core/show-message)
- [showMessageTime method](/docs/funcs/core/show-message-time)
- [showProgress method](/docs/funcs/core/show-progress)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|

# 자주 사용되는 이벤트(이벤트 대응)

## 3. 이벤트 대응 <a name="chapter-3"></a>

#### 자주 사용되는 이벤트 <a name="events-favorite"></a>

IBSheet7에서 자주 사용되는 이벤트에 대해 IBSheet8에서 변경된 부분을 확인합니다.<br/>
이벤트의 발생 시점은 조금씩 차이가 있을 수 있습니다.<br/>
이벤트 명칭이 기존에 `파스칼케이스(PascalCase)`에서 `카멜케이스(camelCase)`로 변경된 점을 주의해 주세요.

|이벤트명|IBSheet8 이벤트|설명|
|---|---|---|
|OnAfterEdit|[onAfterEdit (event)](/docs/events/on-after-edit)||
|OnBeforeCheck|[onBeforeChange (event)](/docs/events/on-before-change)|별도에 `CheckBox`타입에서만 발생하는 이벤트는 없고,해당 이벤트는 모든 타입의 열에서 발생합니다.|
|OnBeforeDownload|[onBeforeDownload (event)](/docs/events/on-before-download)||
|OnBeforePaste|[onBeforePaste (event)](/docs/events/on-before-paste)||
|OnButtonClick|[onClick (event)](/docs/events/on-click)|`Button`타입에서만 발생하는 이벤트는 없고,해당 이벤트는 모든 타입의 열에서 발생합니다.<br>JSON Evnet [onClickSide (props event)](/docs/props/event/on-click-side) 를 사용할 수도 있습니다.|
|OnChange|[onAfterChange (event)](/docs/events/on-after-change)|[setValue (method)](/docs/funcs/core/set-value)와 같이 외부 함수를 통한 변경에서는 발생하지 않습니다.|
|OnClick|[onAfterClick (event)](/docs/events/on-after-click)| IBSheet8의 [onClick (event)](/docs/events/on-click)는 IBSheet7의 동일 이벤트보다 발생 시점이 앞섭니다.<br/>따라서 마이그레이션시 [onAfterClick (event)](/docs/events/on-after-click)를 사용해 주세요.|
|OnDblClick|[onDblClick (event)](/docs/events/on-dbl-click)||
|OnDownFinish|[onExportFinish (event)](/docs/events/on-export-finish)|명칭변경|
|OnKeyUp, OnKeyDown|[onKeyUp (event)](/docs/events/on-key-up), [onKeyDown (event)](/docs/events/on-key-down)||
|OnLoad|[onRenderFirstFinish (event)](/docs/events/on-render-first-finish)|이벤트의 발생시점은 IBSheet7의 OnLoad와 다르나, 최초 생성후 1회 발생하는 점에서 동일합니다.|
|OnLoadData|[onBeforeDataLoad (event)](/docs/events/on-before-data-load)|명칭변경|
|OnLoadExcel, OnLoadText|[onImportFinish (event)](/docs/events/on-import-finish)|단일 이벤트에서 공통처리|
|OnMouseDown, OnMouseUp, OnMouseMove|[onMouseDown (event)](/docs/events/on-mouse-down), [onMouseUp (event)](/docs/events/on-mouse-up), [onMouseMove (event)](/docs/events/on-mouse-move)||
|OnMovePage|[onBeforeGoToPage (event)](/docs/events/on--before-go-to-page)|명칭변경|
|OnRowSearchEnd|[onRowLoad (event)](/docs/events/on-row-load)|명칭변경|
|OnSaveEnd|[onAfterSave (event)](/docs/events/on-after-save)|IBSheet7의 OnSaveEnd는 저장 후 데이터 반영 및 렌더링 처리까지 끝난 상태에서 발생하나, [onAfterSave (event)](/docs/events/on-after-save)는 저장데이터를 서버에서 전송받은 직후 발생합니다.|
|OnSearchEnd|[onSearchFinish (event)](/docs/events/on-search-finish)|명칭변경|
|OnSelectMenu|[onSelectMenu (event)](/docs/events/on-select-menu)||
|OnSelectCell|[onFocus (event)](/docs/events/on-focus)|명칭변경|
|OnSort|[onAfterSort (event)](/docs/events/on-after-sort)|명칭변경|
|OnHScroll, OnVScroll|[onScroll (event)](/docs/events/on-scroll)|단일 이벤트에서 공통처리|

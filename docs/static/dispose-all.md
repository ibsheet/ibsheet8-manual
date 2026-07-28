# disposeAll ***(static)***

> 생성된 모든 `시트 객체`를 제거합니다.  
> 시트는 생성 시 전역 `IBSheet` 객체에 배열 형태로 등록되는데, SPA(Single Page Application) 형식의 화면에서는 페이지 이동(컴포넌트 로드) 시 DOM의 element만 제거되고 이 시트 객체는 그대로 남습니다.  
> 따라서 SPA 형식의 시스템에서는 페이지 이동(컴포넌트 로드) 중에 이 함수를 호출하여 등록된 시트 객체를 정리해야 합니다.

특정 시트 하나만 제거하려면 [dispose](/docs/funcs/core/dispose)를 사용합니다.

### Syntax
```javascript
void IBSheet.disposeAll(dialogs, unload);
```

### Parameters

|Name|Type|Required|Description|
|----------|-----|---|----|
|dialogs|`boolean`|<span class='optional'>선택</span>|`1(true)` 설정 시 시트뿐 아니라 `static` 메소드로 생성된 달력·메뉴·다이얼로그까지 함께 제거합니다.|
|unload|`boolean`|<span class='optional'>선택</span>|`1(true)` 설정 시 시트 관련 메모리까지 해제합니다. SPA 환경에서 컴포넌트마다 `ibsheet.js`를 불러오는 경우에 사용합니다.|

### Return Value
***none***

### Example
```javascript
//SPA형식으로 페이지를 로드
function movePage(url){
    //페이지 이동 전에 현재 Window의 시트를 클리어
    IBSheet.disposeAll(true);

    //새 페이지로 이동
    $("#contents").load(url, function(response, status, xhr) {
        //이동후 작업
    });
}
```

React/Vue/Angular 등 프레임워크 환경에서는 컴포넌트 언마운트(라우트 이탈) 시점에 `IBSheet.disposeAll(true)`를 호출합니다.

### Read More
- [dispose method](/docs/funcs/core/dispose)
- [IBSheet.hasSheet static](/docs/static/has-sheet)
- [IBSheet.create static](/docs/static/create)
<!-- - [IBSheetLoader](https://ibsheet.github.io/loader-manual/) 옛 링크 — 새 로더 매뉴얼 URL 확인 후 교체 -->

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|
|core|8.0.0.3|`unload` 인자 추가|

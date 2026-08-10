# clear ***(method)***

<!-- synonyms: 시트 제거, DOM 제거, 시트 삭제, 메모리 해제, 시트 지우기, 시트 클리어, clear, remove, dispose, cleanup, destroy, unload -->

> DOM 영역에서 시트 부분을 제거합니다.
>
> 구형 Internet Explorer 브라우저에서 메모리 누수에 대응하기 위한 기능입니다.
>
> 브라우저를 새로고침 하거나, 다른 페이지로 이동시 내부적으로 자동 호출됩니다.
>
> [reload](./reload)()함수를 통해 DOM에서 제거된 시트를 다시 불러올 수 있습니다.

### Syntax
```javascript
void clear();
```


### Return Value
***none***

### Example
```javascript
//시트 DOM 부분 제거
sheet.clear();
```

### Read More

- [reload method](./reload)
- [dispose mehtod](./dispose)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|

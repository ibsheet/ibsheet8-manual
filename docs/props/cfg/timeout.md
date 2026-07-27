# Timeout ***(cfg)***

> 시트에서 사용되는 서버통신의 최대 대기 시간 값을 설정합니다. 
>
> 입력 값은 `초(second)` 단위입니다. 기본값은 `60초` 입니다. 
>
> **[ajax (method)](/docs/funcs/core/ajax), [doSave (method)](/docs/funcs/core/do-save), [doSearch (method)](/docs/funcs/core/do-search), [doSearchPaging (method)](/docs/funcs/core/do-search-paging) 호출 시 timeout 인자가 설정되지 않았을 경우에 적용되며 API의 timeout 인자가 우선 적용됩니다.**
>
> 서버(WAS)의 연결 타임아웃이 이 값보다 짧으면 서버에서 먼저 연결이 종료될 수 있습니다.

### Type
`number`

### Example
```javascript
options = {
    Cfg :{
        Timeout: 120,  // 최대 대기 시간을 120초(2분)로 설정
        ...
    }
};
```

### Read More
- [ajax method](/docs/funcs/core/ajax)
- [doSave method](/docs/funcs/core/do-save)
- [doSearch method](/docs/funcs/core/do-search)
- [doSearchPaging method](/docs/funcs/core/do-search-paging)
- [onBeforeDataLoad event](/docs/events/on-before-data-load)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.5|기능 추가|

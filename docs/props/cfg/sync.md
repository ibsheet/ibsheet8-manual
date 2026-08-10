# Sync ***(cfg)***

<!-- synonyms: Sync, scroll sync, sheet scroll sync, sync scroll multiple sheets, sync scrollbar, 스크롤 동기화, 시트 스크롤 동기화, 다중 시트 스크롤, 동시 스크롤, 시트 간 스크롤 -->

> 시트의 스크롤을 동기화 하는 기능입니다. 
>
> 화면에 여러개의 시트가 존재하는 경우 `Sync` 설정 시 동시에 스크롤이 동작합니다. 
>
> 
>
> `제약사항` 다음의 경우에 정상적으로 동작하지 않습니다: 
>
> 1. 시트 간 `SearchMode`가 다른 경우 
>
> 2. 시트 간 `AutoRowHeight` 설정 여부가 다른 경우

### Type
`string`

### Options
|Value|Description|
|-----|-----|
| `Cols` | 컬럼 리사이즈 동기화 기능 설정 |
| `Vert` | 세로 스크롤 동기화 기능 설정 |
| `Horz` | 가로 스크롤 동기화 기능 설정 |

### Example
```javascript
options.Cfg = {
    Sync: 'Vert,Horz'
};
```

### Since

|product|version|desc|
|---|---|---|
|core|8.3.0.16|기능 추가|

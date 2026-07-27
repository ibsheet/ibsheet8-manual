# SearchProgress ***(cfg)***

<!-- synonyms: 대기이미지, 로딩, 로딩바, 로딩 이미지, 블럭, 블록, 진행 상태, loading, progress bar -->

> 대기이미지 대신 프로그레스바를 사용하여 데이터 조회([doSearch](/docs/funcs/core/do-search), [loadSearchData](/docs/funcs/core/load-search-data)) 시 내부 작업 과정(`"API 호출 및 응답대기"`, `"데이터 파싱"`, `"렌더링 시작"`, `"렌더링 완료"`)을 순차적으로 보여줍니다.  
> 프로그레스바가 비동기 형태로 동작하기 때문에 실제 시트에 로딩되는 속도와는 약간 차이가 있을 수 있습니다.  
> [(Cfg)SuppressMessage](/docs/props/cfg/suppress-message)를 `3` 또는 `4`로 설정해야 사용할 수 있습니다.  
> 조회 중에 오류 발생 시, 프로그레스바에서 어떤 과정에서 오류가 났는지 확인할 수 있습니다.

### 프로그레스바 구조

![프로그래스바](../../../assets/imgs/showProgress.png)

프로그래스바에 표시되는 Text는 메세지 파일(ko.js 등)의 `SearchProgressMessage`, `DataSearchingMessage` 값입니다.



### Type
`boolean`

### Options
|Value|Description|
|-----|-----|
|`0(false)`|데이터 조회 시 프로그레스바 미사용 (`default`)|
|`1(true)`|데이터 조회 시 프로그래스바 사용|


### Example
```javascript
options.Cfg = {
    SearchProgress: true
};
```

### Read More
- [SuppressMessage cfg](./suppress-message)
- [doSearch method](/docs/funcs/core/do-search)
- [loadSearchData method](/docs/funcs/core/load-search-data)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.14|기능 추가|

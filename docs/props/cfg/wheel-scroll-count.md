# WheelScrollCount ***(cfg)***

<!-- synonyms: WheelScrollCount, wheel scroll count, mouse wheel rows, scroll wheel step, wheel step count, 휠 스크롤 행 수, 마우스 휠 스크롤, 휠 이동 행, 휠 스크롤 개수, 마우스 휠 이동 행 -->

> `SearchMode` 와 상관없이, 휠 스크롤 시 이동할 행의 개수를 설정하는 기능 입니다. 
>
> 설정 하지 않으면, `SearchMode: 0` 은 3개, `SearchMode: 2` 은 `window.wheel.event` 의 `deltaY` 만큼 움직입니다.

### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`number`|휠 스크롤 시 이동할 행의 개수|


### Example
```javascript
options.Cfg = {
   WheelScrollCount: 1 // 스크롤 시 행의 개수가 1개씩 움직입니다.
};
```

### Read More
- [SearchMode cfg](/docs/props/cfg/search-mode)

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.20|기능 추가|

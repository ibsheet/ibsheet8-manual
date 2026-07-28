# EditArrowBehavior ***(cfg)***

<!-- synonyms: 방향키, 화살표키, 좌우 방향키, 편집 중 셀 이동, 커서 이동, arrow key, edit arrow, cell move, cursor move -->

> 편집 중 키보드 좌/우 방향키로 셀 이동을 할 수 있도록 설정합니다.  
> 커서가 편집 중인 텍스트의 좌/우 끝에 도달했을 때 이동합니다.


### Type
`number`

### Options
|Value|Description|
|-----|-----|
|`0`|기능 사용 안함 (`default`)|
|`1`|편집 불가 컬럼은 건너뛰고 다음 편집 가능한 셀로 이동합니다.|
|`2`|편집 불가 컬럼으로도 이동하며, 해당 셀에서는 편집 모드가 종료됩니다.|


### Example
```javascript
options.Cfg = {
    EditArrowBehavior: 2
};
```

### Read More


### Since

|product|version|desc|
|---|---|---|
|core|8.1.0.97|기능 추가|

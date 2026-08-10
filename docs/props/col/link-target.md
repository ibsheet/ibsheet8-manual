# LinkTarget ***(col)***

<!-- synonyms: 링크 타겟, 새창 열기, target 창, _blank, _self, link target, open window, target window, new tab -->

> 셀에 [Link](/docs/props/col/link)속성이 있는 경우, 클릭시 이동할 target Window를 설정합니다..

### Type
`string`

### Options
|Value|Description|
|-----|-----|
|`string`|클릭시 이동할 Target Window(_blank ,_parent ,_self ,_top, 특정 window명)|


### Example
```javascript
//열을 클릭시 특정 URL로 이동한다.
options.Cols = [
    ...
    //클릭시 새창으로 열기
    {Type: "Text", Link: "/tMIS/dcp/ConfProc.do", LinkTarget: "_blank", CanEdit: 0 , Name: "sa_cfprc", Width: 100 ...},
    ...
];
```

### Read More
- [Link col](/docs/props/col/link)
- [LinkBase col](/docs/props/col/link-base)


### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|

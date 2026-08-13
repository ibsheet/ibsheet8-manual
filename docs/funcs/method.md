# method 사용법 기초
> 시트가 제공하는 모든 메소드는 각 파라미터를 순서대로 설정하거나 하나의 `object` 형태로 설정할 수 있습니다.

아래 예제의 `sheet`는 [IBSheet.create()](/docs/static/create)로 생성한 **시트 객체(인스턴스)**입니다.  
`create` 시 지정한 `id`는 전역 변수로 등록되므로, `id`를 `"sheet"`로 생성했다면 `sheet`로 바로 접근할 수 있습니다. (또는 `create`의 리턴값을 원하는 변수에 담아 사용해도 됩니다.)

### 파라미터 설정 방법
```javascript
//addRow 행추가   (next: 행위치, visible: 보임여부, focus: 포커스 이동여부, parent: 트리사용시 부모 행객체)

//각 파라미터를 순서대로 설정
sheet.addRow(sheet.getFirstRow(), 1);

//파라미터를 object 형태로 설정
sheet.addRow({visible: 1, focus: 1});
```

### Read More

### Since

|product|version|desc|
|---|---|---|
|core|8.0.0.0|기능 추가|

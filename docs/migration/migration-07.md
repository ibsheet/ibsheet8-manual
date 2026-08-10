# ColLeft 대체 (getColLeft7 커스텀 함수)

<!-- synonyms: IBSheet7, 마이그레이션, sheet7, migration, v7, v8, ibsheet7에서 ibsheet8로, 이외 유의사항, 부가 팁, additional notes, misc -->

IBSheet7의 `ColLeft`(열의 왼쪽 끝 절대 위치 px)에 직접 대응하는 IBSheet8 함수는 없습니다.  
IBSheet8의 [getColLeft (method)](/docs/funcs/core/get-col-left)은 **틀고정 섹션(왼쪽/가운데/우측) 기준 상대 위치**를 반환하므로, 앞쪽 섹션 너비([getBodyWidth (method)](/docs/funcs/core/get-body-width))를 더해 절대 위치를 구하는 헬퍼를 아래처럼 정의해 사용합니다.

```javascript
// 열 index를 열 이름으로 변환 (SEQ 자동 생성 컬럼 보정 포함)
sheet.getColByIndex7 = function(colIndex) {
  if (colIndex === "" || colIndex === null || colIndex === undefined) return '';
  var seqAdj = (this.Cols["SEQ"] && this.Cols["SEQ"].VPos === -1) ? 1 : 0;
  if (typeof colIndex == "string") {
    if (colIndex.indexOf("|") != -1) {
      return colIndex.split("|").map(c => this.getColByIndex7(c));
    }
    if (!isNaN(colIndex)) return this.getColByIndex(parseInt(colIndex) + seqAdj, 1);
    return colIndex; // 이미 열 이름인 경우
  } else if (typeof colIndex == "number") {
    return this.getColByIndex(colIndex + seqAdj, 1); // getColByIndex: 1부터, 숨김 포함, 좌측(틀고정)부터
  }
};

// ColLeft 대체 — 열의 왼쪽 끝 절대 위치(px)
sheet.getColLeft7 = function(colIndex) {
  const colName = sheet.getColByIndex7(colIndex);
  const section = sheet.Cols[colName].Section;   // 0:왼쪽 1:가운데 2:우측 틀고정
  let iLeft = sheet.getColLeft(colName);          // 섹션 기준 상대 위치
  // getBodyWidth: 0=왼쪽, 1=가운데 섹션 너비
  switch (section) {
    case 1: iLeft += sheet.getBodyWidth(0); break;                          // 가운데: 왼쪽 너비 추가
    case 2: iLeft += sheet.getBodyWidth(0) + sheet.getBodyWidth(1); break;  // 우측: 왼쪽 + 가운데 너비 추가
  }
  return iLeft;
};

// 사용 예: 5번 열의 왼쪽 끝 절대 위치
var left = sheet.getColLeft7(5);
```

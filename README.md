# 배민 장바구니 만들기

## 페이지

### 음식 목록 페이지

- API요청을 통해 목록을 반환 해와야 함
  - 로딩 처리하기
- 카테고리에 따라 아이템이 분류 되어져 있음
  - 분식
    - 떡볶이
    - 순대
  - 튀김
    - 새우 튀김
    - 오징어 튀김
    - 고추 튀김
- 클릭시 장바구니에 담긴다.
- 장바구니 아이콘이 존재하고 누른 개수만큼 수량이 변경된다.
- 장바구니 아이콘을 누르면 아이콘 페이지로 이동됨

### 장바구니 페이지

- 선택한 음식의 수량을 변경 할 수 있다.
- 선택한 음식을 장바구니에서 제거할 수 있다.
- 할인 쿠폰을 선택 할 수 있다.
  - 할인 쿠폰은 할인할 아이템을 설정 할 수있다. (`요구사항 어려움 참고`)
- 음식이 삭제, 수량이 변경, 할인할 아이템이 변경 될 때 마다 최 하단에 결제 예정 금액이 계산되어진다.
- 뒤로가기 아이콘이 있고 클릭시 뒤로 이동 되어짐
- 할인을 제외하고 최소 주문금액(`minimum_order_price`)을 넘지못하면 결제 버튼이 비활성화 되어짐

## 요구 사항

### 기본

- 장바구니에 물품 담기
- 장바구니에서 물품 삭제하기
- 장바구니에 아이템이 선택될 때마다 총 결제 금액이 갱신되어야 함
- 금액 표기시
  - `11,000원` `,` 찍기
  - 소수점 이하는 버림
- 할인 쿠폰 선택
- 동일한 아이템이 장바구니에 들어갈 수 없음

### 어려움

할인 항목이 존재 해당 할인 항목은 품목별로 지정 할 수 있음

- 할인 항목 부분 선택
  - 김치찌개 10,000원
  - 공기밥 1,000원
  - 첫주문 할인 5% (`김치찌개`)
  
  총 결제 금액 
  
  10000 * (0.95) + 1000 = 10500
  
- 할인 항목 전체 선택시
  - 김치찌개 10,000원
  - 공기밥 1,000원
  - 첫주문 할인 5% (`김치찌개`, `공기밥`)
  
  총 결제 금액
  
  (10000 + 1000) * 0.95 = 10450
  
- 외부 API는 언제든 오류가 날것을 염두해두고 방어적으로 클라이언트 코드를 작성하여야 합니다.  물품목록 API에서 오류가 날 경우에 대한 방어코드를 작성하고 어떻게 처리할지? 또 리액트에서 에러처리는 어떻게 하는지 공부해보고 적용해보세요!
- 내가만든 리액트앱 배포해보기
  - github page
  - netlify
  - firebase hosting
- 타입스크립트로 개발하기

## 참고 사항

- 물품 목록은 아래 API를 통해서 반환 됨
  
  아래 API는 항상 목록을 반환하지 않습니다. 오류가 발생할 것에 대비하여 코드를 작성 해주세요.
~~~jsx
{
"minimum_order_price": 15000,
"merchant_name": "순두부 찌개 맛집",
"items": [
  ...
  {
    "id": "kimchi",
    "category_id": "jjigae",
    "category_name": "찌개",
    "name": "김치 찌개",
    "price": 30000
  },
],
"discounts": [
    ...
    {
      "id": "chutjumun",
      "name": "첫 주문 할인",
      "discount_rate": 3 // 3%를 할인을 의미
    }
  ]
}
~~~
  
- Redux 연습을 위해 `redux-toolkit`을 꼭 사용할 것
  - 상태 설계 고민해보기
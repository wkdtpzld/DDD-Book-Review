# 2. 아키텍처 개요

## 2.1 네 개의 영역

'표현', '응용', '도메인', '인프라스트럭처' 는 아키텍처를 설계할 때 출현하는 전형적인 네 가지 영역이다.

네 영역중 표현 영역은 사용자의 요청을 받아 응용 영역에 전달하고 응용 영역의 처리 결과를 다시 사용자에게 보여주는 역할을 한다.

웹 어플리케이션을 개발할 때 많이 사용하는 MVC 프레임워크가 표현 영역을 위한 기술에 해당한다.

REST API 를 호출하는 외부 시스템일 수도 있다.

웹 어플리케이션의 표현 영역은 HTTP 요청을 응용 영역이 필요로 하는 형식으로 변환해서 응용 영역에 전달하고 응용 영역의 응답을 HTTP 응답으로 변환하여 전송한다.

예를들어 표현 영역은 웹 브라우저가 HTTP 요청 파라미터로 전송한 데이터를 응용 서비스가 요구하는 형식의 객체 타입으로 변환, 전달

응용 서비스가 리턴한 결과를 JSON 형식으로 변환해서 HTTP 응답으로 웹 브라우저에 전송.

표현 영역을 통해 사용자의 요청을 전달받는 응용 영역은 시스템이 사용자에게 제공해야 할 기능을 구현하는데 '주문 등록', '주문 취소', '상품 상세 조회' 와 같은 기능 구현을 예로 들 수 있다.

응용 영역은 기능을 구현하기 위해 도메인 영역의 도메인 모델을 사용한다.
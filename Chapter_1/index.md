# 1. 도메인 모델 시작하기.

## 1.1 도메인이란?

책을 구매할 떄 어떤 책이 나왔는지 검색하고, 목차와 서평을 보고,

이 책은 어떤 책일지 가늠해 보고. 읽고 싶은 책이 있으면 나중에 사기 위해 장바구니에 담거나 바로 구매할 수도 있다.

싸게 살 수 있는 쿠폰이 있는지 찾아보기도 한다. 간편 결제, 외부 서비스 사용을 통해 결제하고

구매한 뒤에 언제 책을 받을 수 있는지 추적을 할 수 도 있다.

개발자 입장으로 본다면 서점은 구현해야할 소프트웨어이다. **상품 조회, 구매, 결제, 배송 추적** 등의 기능을 제공해야 한다.

![img.png](img.png)

카탈로그 하위 도메인은 고객에게 구매 가능한 상품 목록을 제공, 주문 하위 도메인은 고객의 주문을 처리.

혜택 하위 도메인은 쿠폰이나 할인과 같은 서비스를 제공한다. 한 하위 도메인은 다른 하위 도메인과 연동하여 완전한 기능을 제공.

특정 도메인을 위한 소프트웨어라고 해서 도메인이 제공해야 할 모든 기능을 직접 구현하는 것은 아니다.

외부 시스템을 사용하는 경우도 있기 떄문이다.

## 1.2 도메인 전문가와 개발자 간 지식 공유

홍보나 정산, 배송 등의 영역에는 전문가가 있고 이들 전문가는 해당 도메인에 대한 지식과 경험을 바탕으로 본인들이 원하는 기능 개발을 요구한다.

회계 담당자는 엑셀로 맞추던 정산 금액 계산을 자동화해 주는 기능을 요구할 수 있다.

AS 기사는 고객에게 보내는 문자 메세지를 빠르게 입력할 수 있는 템플릿 추천 기능을 요구할 수 있다.

개발자는 이런 요구사항을 분석하고 설계하여 코드를 작성하며 테스트, 배포가 가능하다.

만약 요구사항을 올바르게 이해하지 않으면 엉뚱한 기능을 구현하게 된다.

요구사항을 제대로 이해하기 위해서는 개발자와 전문가가 직접 대화하는 것이 중요하다.

개발자와 전문가 사이에 내용을 전파하는 전달자가 많으면 많을수록 정보가 왜곡되고 손실이 발생한다.

개발자도 어느정도의 도메인 지식을 갖춰야 한다. 제품 개발과 관련된 도메인 전문가, 관계자, 개발자가 같은 지식을 공유하가 직접 소통할수록 도메인전문가가 원하는 제품을 만들 확률이 올라간다.

### Garbage in Garbage Out

잘못된 값이 들어가면 잘못된 결과가 나온다는 뜻이다. 요구사항을 잘못 이해하면 출력값도 잘못된 값으로 나오기 떄문에 개발자와 도메인 전문가와의 의사소통이 중요하다.

## 1.3 도메인 모델

도메인 모델에는 다양한 정의가 존재한다. 기본적으로 도메인 모델은 특정 도메인을 개념적으로 표현한 것이다.

주문 모델을 객체 모델로 구성하면 밑과 같은 이미지 처럼 된다.

![img_1.png](img_1.png)

주문(Order)은 주문번호(orderNumber)와 지불할 총금액(totalAmounts)이 있고 배송정보(ShippingInfo)를 변경(changeShipping)을 할 수 있다.

또한 주문을 취소 할 수 있다는 것도 알 수 있다. 도메인 모델을 사용하면 여러 관계자들이 동일한 모습으로 도메인을 이해하고 도메인 지식을 공유하는 데 도움이 된다.

객체를 이용한 도메인 모델이다.

도메인을 이해하려면 도메인이 제공하는 기능과 도메인이 주요 데이터를 구성해야 하는데 이런 면에서 기능과 데이터를 함께 보여주는 객체 모델은
도메인 모델링하기에 적합하다.

![img_2.png](img_2.png)

객체로만 모델링을 할 수 있는 것은 아니다. 상태 다이어그램을 통해 주문의 상태 전이를 모델링하고 있다.

도메인 모델은 기본적으로 도메인 자체를 이해하기 위한 개념 모델이다. 개념 모델을 이용해서 바로 코드를 작성할 수 있는 것은 아니기에 구현 기술에 맞는 구현 모델이 따로 필요하다.

개념 모델과 구현 모델은 서로 다른 것이지만 구현 모델이 개념 모델을 최대한 따르도록 할 수는 있다.

## 1.4 도메인 모델 표현

일반적인 어플리케이션의 아키텍처는 네 개의 영역으로 구성된다.

표현 - 응용 - 도메인 - 인프라스트럭처

| 영역             | 설명                                                                |
|----------------|-------------------------------------------------------------------|
| 사용자 인터페이스 / 표현 | 사용자의 요청을 처리하고 사용자에게 정보를 보여준다. 소프트웨어를 사용하는 사람뿐만 아니라 외부 시스템일 수도 있다. |
| 응용             | 사용자가 요청한 기능을 실행한다. 업무 로직을 직접 구현하지 않아도 되며 도메인 계층을 조합해서 기능을 실행한다.   |
| 도메인            | 시스템이 제공할 도메인 규칙을 구현한다.                                            |
| 인프라스트럭처        | 데이터베이스나 메세징 시스템과 같은 외부 시스템과의 연동을 처리한다.                            |

지금까지는 도메인 자체를 이해하는 데 필요한 개념 모델을 의미한다면. 지금은 도메인 모델 패턴을 의미한다.

도메인 모델은 아키텍처 상의 도메인 계층을 객체 지향 기법으로 구현하는 패턴을 의미한다.

도메인 계층은 도메인의 핵심 규칙을 구현한다. 
주문 도메인의 경우 출고 전에 배송지를 변경 할 수 있다는 규칙과 주문 취소는 배송 전에만 할 수 있다 라는 규칙을
구현한 코드가 도메인 계층에 위치하게 된다.

이런 도메인 규칙을 객체 지향 기법으로 구현하는 패턴이 도메인 모델 패턴이다.

```java
public class Order {
    private OrderState state;
    private ShippingInfo shippingInfo;
    
    public void changeShippingInfo(ShippingInfo newShippingInfo) {
        if (!state.isShippingChangeable()) {
            throw new IllegalStateException("can`t change Shipping in " + state);
        }
        this.shippingInfo = newShippingInfo;
    }
    
}

public enum OrderState {
    PAYMENT_WAITING {
        public boolean isShippingChangeable() {
            return true;
        }
    },
    PREPARING {
        public boolean isShippingChangeable() {
            return true;
        }
    },
    SHIPPED, DELIVERING, DELIVERY_COMPLETED;

    public boolean isShippingChangeable() {
        return false;
    }
}
```

이 코드는 주문 도메인의 일부 기능을 도메인 모델 패턴으로 구현한 것이다.

OrderState 는 배송지를 변경할 수 있는지를 검사하는 isShippingChangeable() 메서드를 제공하고 있다.

큰 틀에서 보면 OrderState 는 Order 에 속한 데이터이므로 배송지 정보 변경 가능 여부를 판단하는 Order로 이동할 수 있다.

```java
public class Order {
    private OrderState state;
    private ShippingInfo shippingInfo;

    public void changeShippingInfo(ShippingInfo newShippingInfo) {
        if (!state.isShippingChangeable()) {
            throw new IllegalStateException("can`t change Shipping in " + state);
        }
        this.shippingInfo = newShippingInfo;
    }

    private boolean isShippingChangeable() {
        return state == OrderState.PAYMENT_WAITING || state == OrderState.PREPARING;
    }
}

public enum OrderState {
    PREPARING, PAYMENT_WAITING, SHIPPED, DELIVERING, DELIVERY_COMPLETED;
}
```

배송지 변경이 가능한지를 판단할 규칙이 주문 상태와 다른 정보를 함께 사용한다면 OrderState 만으로는 배송지 변경 가능 여부를 판단할 수 없으므로

Order 에서 로직을 구현해야 한다.

배송지 변경 가능 여부를 판단하는 기능이 Order 에 있든 OrderState 에 있든 중요한 점은 주문과 관련된 중요 업무 규칙을 주문 도메인 모델인
Order 나 OrderState 에서 구현한다는 점이다.

핵심 규칙을 구현한 코드는 도메인 모델에만 위치하기 때문에 규칙이 바뀌거나 규칙을 확장해야 할 때 다른 코드에 영향을 덜 주고 변경 내역만 모델에 반영할 수 있다.

두 번째 방법은 DDD 와는 잘 안맞는 느낌이다.

### 문제점.

isShippingChangeable() 메서드가 Order 클래스에 정의되어 있으며, 

이 메서드가 상태에 따른 로직을 처리하고 있습니다. 이는 상태 변화에 대한 로직이 OrderState가 아닌 Order에 포함된 것이므로,

응집성이 떨어지고 유지보수가 어려워질 수 있습니다.

### DDD 관점.

도메인 로직이 흩어져 있는 상황이므로, 상태에 따라 동작하는 로직은 상태 자체에 포함시키는 것이 더 적절합니다.

또한, 상태에 따른 변경 규칙을 OrderState에 두지 않고 Order에서 처리하는 것은 객체가 자신의 상태를 알지 못하는 것처럼 보입니다.

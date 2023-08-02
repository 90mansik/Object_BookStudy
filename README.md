# OBJECT 북스터디


## Chapter 03 역할, 책임, 협력

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/da5bae3a-b450-4c20-a267-eb1dccc8c41c/Untitled.png)

위 그림에서 다양한 객체들이 영화 예매 기능을 구현하기 위해 메시지를 주고 받으며 상호 작용 하고 있다.

객체지향 패러다임의 관점에서 핵심

- **협력(collaboration) :** 객체들이 애플리케이션의 기능을 구현하기 위해 수행하는 상호작용
- **책임(responsibility)** : 객체가 협력에 참여하기 위해 수행하는 로직
- **역할(role)** : 객체들이 협력 안에서 수행하는 책임들이 모여 구성하는 것

### 협력

- 객체지향의 세계에서 기능을 할 수 있는 유일한 방법이며, 두 객체 사이의 협력은 하나의 객체가 다른 객체에게 도움을 요청할 때 시작된다.
- 다른 객체에게 도움을 요청하는 커뮤니케이션 수단을 **메시지 전송(message sending)**이라 한다.
- 자율적인 객체는 자신에게 할당된 책임을 수행하던 중에 필요한 정보를 알지 못하거나 외부의 도움이 필요한 경우 적절한 객체에게 메시지를 전송해 협력을 요청한다.

### 협력이 설계를 위한 문맥을 결정한다

애플리케이션 안에 어떤 객체가 필요하다면 그 객체가 어떤 협력에 참여하고 있기 때문이다.

그리고 객체가 협력에 참여할 수 있는 이유는 협력에 필요한 적절한 행동을 보유하고 있기 때문.

Ex)

Movie의 행동을 결정하는 것은 영화 예매를 위한 협력이다. 협력이라는 문맥을 고려하지 않고 Movie의 행동을 결정하는 것은 의미가 없다. 협력이 존재하기 떄문에 객체가 존재한다.

객체의 행동은 협력이 결정하고, 상태는 행동이 결정한다.

```java
public class Movie{
	private Money fee;
	private DiscountPolicy discountPolicy;

	public Money calculateMovieFee(Screening screening){
		return fee.minus(discountPolicy,calculateDiscountamount(screening));
	}
}
```

결과적으로 객체가 참여하는 협력이 객체를 구성하는 행동과 상태 모두를 결정한다. 협력은 객체를 설계하는데 필요한 일종의 문맥(context)를 제공한다.

## 02) 책임

### 책임이란 무엇인가

협력에 참여하기 위해 객체가 수행하는 행동이다.

객체의 책임은 객체가 ‘무엇을 알고 있는가’와 무엇을 할 수 있는가’로 구성된다.

**크레이그 라만(Craing Larman)의 객체 세분화**

하는 것(doing)

- 객체를 생성하거나 계산을 수행하는 등의 스스로 하는 것
- 다른 객체의 행동을 시작시키는 것
- 다른 객체의 활동을 제어하고 조절하는 것

아는 것(knowing)

- 사적인 정보에 관해 아는 것
- 관련된 객체에 관해 아는 것
- 자신이 유도하거나 계산할 수 있는 것에 관해 아는 것

Ex) 영화 예매 시스템 

Screening의 책임

- 영화를 예매한다 - 하는 것
- 상영할 영화를 알고 있어야 한다 - 아는 것

Movie의 책임

- 예매 가격을 계산 한다. - 하는것
- 어떤 할인 정책이 적용 됬는지  안다 - 아는 것

객체에게 책임을 할당하기 위한 가장 기본적인 원칙

- 객체는 자신이 맡은 책임을 수행하는데 필요한 정보를 알고 있을 책임이 있다
- 자신이 할 수 없는 작업을 작업을 도와줄 객체를 알고 있을 책임이 있다.

**C(Candidate)-R(Responsibility)-C(Collaborate) 카드 (by 워드 커닝햄과 켄트 백)**

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/52cdae6e-3aab-4e20-a82f-f9b2210dad15/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/46c4bb94-26d7-4e49-99c2-ec4befae88db/Untitled.png)

- Candiate
    - 협력에 참여하는 하나의 후보를 표현한다
- Repository
    - 좌측에 객체의 대한 책임을 적는다
- Coolaborator
    - 우측에 책임을 수행하면서 함께 협력할 협력자 들을 나열한다

### 책임할당

필요한 정보를 가장 잘 알고 있는 전문가에게 그 책임을 할당해야 한다 

→ INFORMATION EXPERT(정보 전문가) 패턴

책임할당 방법

1. 책임을 할당하라 = 메시지의 이름을 결정

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7656add1-3bf6-49f5-8cd8-3efcd533f477/Untitled.png)

1. 메시지를 처리할 적절한 객체에게 책임을 할당 해라

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/65461448-a8d0-4287-9175-3e628571cac4/Untitled.png)

1. 내가 해결할 수 없는 책임에 대해서 외부 객체의 보낼 메시지를 생성해라

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b128df73-295c-438e-9516-70647bb046af/Untitled.png)

1. 메시지를 처리할 적절한 객체에게 책임을 할당 해라

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/47f69780-e7c4-4926-b260-d40ae4144841/Untitled.png)

객체지향 설계는 협력에 필요한 메시지를 찾고, 메시지에 적합한 객체를 선택하는 반복적인 과정

### 책임주도 설계

협력을 설계하기 위해서는 책임에 초첨을 맞춰야 한다.

이처럼 책임을 찾고 책임을 수행할 적절한 객체를 찾아 책임을 할당하는 방식으로 협력을 설계하는 방법을 책임 주도 설계(RDD) 라고 부른다.

### 책임할당 시 고려사항

1. 메시지가 객체를 결정한다.
    - 메시지를 먼저 식별하고 메시지를 처리할 객체를 나중에 선택 했다
    - 최소한의 인터페이스를 가질 수 있게 된다.
    - 추상적인 인터페이스를 가질 수 있게 된다.
        - 무엇을 하는지는 표현되지만, 어떻게 수행하는지는 노출이 되지 않는다
2. 행동이 상태를 결정한다
    - 객체가 존재하는 이유는 협력에 참여하기 위해서다. 객체를 객체답게 만드는 것은 객체의 상태가 아니라 객체의 다른 객체에게 제공되는 행동이다.
    - 초보자들은 먼저 객체에 필요한 상태가 무엇인지를 결정하고, 그 후에 상태에 필요한 행동을 결정한다. 이런 방식은 객체의 내부 구현이 객체의 퍼블릭 인터페이스에 노출되도록 만들기 때문에 캡슐화를 저해한다. 객체의 내부 구현에 초점을 맞춘 설계 방벙을 `데이터-주도 설계(Data-Driven Design)`이라고 부르기도 했다
    
    ## 02) 역할
    
    ### 역할과 협력
    
    객체가 어떤 특정한 협력 안에서 수행하는 책임의 집합을 역할 이라고 부른다.
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/63796e64-4cd3-40ec-b436-faedebc92ddb/Untitled.png)
    
    - 역할이라는 개념을 고려하지 않고 객체에게 책임을 할당하는 경우
    - 정액/정률 할인 두가지의 종류의 정책이 있다면 중복된 코드로 개별적인 객체를 만들어야 한다.
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1644cd31-d1e4-4edd-b157-33092ed613c1/Untitled.png)
    
    - 문제를 해결하기 위해 책임의 관점에서 “할인 요금 계산”이라는 동일한 책임을 수행한다는 사실을 알 수 있다.
    - 동일한 책임을 수행할 대표자가 **역할** 이다.
    - 역할이 두 종류의 구체적인 객체를 포괄하는 **추상화** 이다.
    
    ### 역할과 추상화
    
    추상화 계층 만을 이용하면 중요한 정책을 상위 수준에서 단순화시킬 수있다.
    
    설계가 유연해진다.
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d7faaa1a-91d0-4ef2-98f1-50cc277fe7b9/Untitled.png)
    
    - 그림 3.6 세부적인 사항으로 인해 객체들 사이의 핵심적인 관계와 관련된 큰 그림을 파악하는 것을 방해한다.
    - 그림 3.7 객체 사이의 핵심적인 상호작용이 좀 더 또렷하게 드러난다.
    
    ### 배우와 배역
    
    연극의 배역과 배우 간의 관계에 다음과 같은 특성이 존재
    
    - 배역은 연극 배우가 특정 연극에서 연기하는 역할
    - 배격은 연극이 상영되는 동안에만 존재하는 일시적인 개념
    - 연극이 끝나면 연극 배우는 배역이라는 역할을 벗어 버리고 원래의 연극 배우로 돌아온다.
    
    Ex ) 로미오라는 배역 = 역할(추상화)
    
    배역을 연기하는 연극 배우 = 책임(클래스)

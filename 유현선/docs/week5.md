# 05. 책임 할당하기 

데이터 중심 설계의 문제점
 - 캡슐화를 위반하기 쉬움
 - 요소들 사이의 결합도가 높아짐
 - 코드를 변경하기 어렵다


책임에 초점을 맞춰서 설계할 경우 => 책임 할당(트레이드 오프)의 어려움이 존재 
- 상황과 문맥에 따라 다름
- 올바른 책임 할당을 위해 다양한 관점에서 설계를 평가해야 함 


---


## 책임 주도 설계를 향해 
> - 데이터보다 행동을 먼저 결정하라  
> - 협력이라는 문맥 안에서 책임을 결정하라  

### 데이터보다 행동을 먼저 결정하라
 
1. 이 객체가 수행해야 하는 책임은 무엇인가  
2. 이 책임을 수행하는 데 필요한 데이터는 무엇인가  

### 협력이라는 문맥 안에서 책임을 결정하라 
- 메시지를 먼저 결정한 후 그 메시지가 객체를 선택하게 해야 함 
  - 메시지 : 클라이언트의 의도를 표현
  - 임의의 객체가 메시지를 수신할 것이라는 사실을 믿고 자신의 의도를 표현한 메시지를 전송할 뿐
  - 수신받는 객체 : 메시지를 처리할 '책임'을 할당받음
- 책임 중심의 설계에서는 협력이라는 문맥 안에서 객체가 수행할 책임에 초점을 맞춘다. 

### 책임 주도 설계 
- 시스템이 사용자에게 제공해야 하는 기능인 시스템 책임을 파악한다
- 시스템 책임을 더 작은 책임으로 분할한다
- 분할된 책임을 수행할 수 있는 적절한 객체 또는 역할을 찾아 책임을 할당한다
- 객체가 책임을 수행하는 도중 다른 객체의 도움이 필요한 경우 이를 책임질 적절한 객체 또는 역할을 찾는다
- 해당 객체 또는 역할에게 책임을 할당함으로써 두 객체가 협력하게 한다


---


## 책임 할당을 위한 GRASP 패턴 

> GRASP : General Responsibility Assignment Software Pattern (일반적인 책임 할당을 위한 소프트웨어 패턴)

### 도메인 개념에서 출발하기 
- 설계를 시작하기 전 도메인에 대한 개략적인 모습을 그려보는 것도 유용


### 정보 전문가에게 책임을 할당하라: INFORMATION EXPERT(정보 전문가 패턴)
- 메시지를 전송할 객체는 무엇을 원하는가?
- 메시지를 수신할 적합한 객체는 누구인가?


- INFORMATION EXPERT(정보 전문가 패턴)
  - 책임을 정보 전문가(= 책임을 수행하는 데 필요한 정보를 가지고 있는 객체)에게 할당하라 
  - 객체가 자신이 소유하고 있는 정보(≠ 데이터)와 관련된 작업을 수행한다는 일반적인 직관을 표현한 것 
  - 정보 전문가가 데이터를 반드시 저장하고 있을 필요는 없음(중요)


### 높은 응집도와 낮은 결합도: LOW COUPLING(낮은 결합도 패턴) & HIGH COHESION(높은 응집도 패턴)
- 책임을 할당할 수 있는 다양한 대안들이 존재한다면 응집도와 결합도의 측면에서 더 나은 대안을 선택할 것 


- LOW COUPLING(낮은 결합도 패턴)
  - 어떻게 하면 의존성을 낮추고 변화의 영향을 줄이며 재사용성을 증가시킬 수 있을까?
  - 설계의 전체적인 결합도가 낮게 유지되도록 책임을 할당


- HIGH COHESION(높은 응집도 패턴)
  - 어떻게 복잡성을 관리할 수 있는 수준으로 유지할 것인가? 
  - 높은 응집도를 유지할 수 있게 책임을 할당


### 창조자에게 객체 생성 책임을 할당하라: CREATOR(창조자 패턴)
- 객체 A를 생성해야 할 때 어떤 객체에게 객체 생성 책임을 할당해야 하는가?  
  (아래 조건을 최대한 많이 만족하는 B에게 객체 생성 책임을 할당할 것)
  - B가 A 객체를 포함하거나 참조한다
  - B가 A 객체를 기록한다
  - B가 A 객체를 긴밀하게 사용한다
  - B가 A 객체를 초기화하는 데 필요한 데이터를 가지고 있다(이 경우 B는 A에 대한 정보 전문가다) 


- CREATOR 패턴의 의도는 어떤 방식으로든 생성되는 객체와 연결되거나 관련될 필요가 있는 객체에 해당 객체를 생성할 책임을 맡기는 것이다. 생성될 객체에 대해 잘 알고 있어야 하거나 그 객체를 사용해야 하는 객체는 어떤 방식으로든 생성될 객체와 연결될 것이다. (=객체 결합)
- 이미 결합돼 있는 객체에 생성 책임을 할당하는 것은 설계의 전체적인 결합도에 영향을 미치지 않음
- 결과적으로 CREAOTR 패턴은 이미 존재하는 객체 사이의 관계를 이용하기 때문에 설계가 낮은 결합도를 유지할 수 있게 한다


---


## 구현을 통한 검증 

### 클래스 응집도 판단하기 
- 클래스가 하나 이상의 이유로 변경돼야 한다면 응집도가 낮은 것 -> 변경의 이유를 기준으로 클래스를 분리하라 
- 클래스의 인스턴스를 초기화하는 시점에 경우에 따라 서로 다른 속성들을 초기화하고 있다면 응집도가 낮은 것 -> 초기화되는 속성의 그룹을 기준으로 클래스를 분리하라
- 메서드 그룹이 속성 그룹을 사용하는지 여부로 나뉜다면 응집도가 낮은 것 -> 이들 그룹을 기준으로 클래스를 분리

### POLYMORPHISM(다형성 패턴)
- 객체의 타입에 따라 변하는 로직이 있을 때 변하는 로직을 담당할 책임을 어떻게 할당해야 하는가? 
- 타입을 명시적으로 정의하고 각 타입에 다형적으로 행동하는 책임을 할당할 것
- POLYMORPHISM 패턴은 객체의 타입을 검사해서 타입에 따라 여러 대안들을 수행하는 조건적인 논리 사용(if~else, switch~case)을 지양하고, 대신 다형성을 이용해 새로운 변화를 다루기 쉽게 확장하라고 권고함 

### PROTECTED VARIATIONS (변경 보호 패턴)
- 객체, 서브시스템, 그리고 시스템을 어떻게 설계해야 변화와 불안정성이 다른 요소에 나쁜 영향을 미치지 않도록 방지할 수 있을까?
- 변화가 예상되는 불안정한 지점들을 식별하고 그 주위에 안정된 인터페이스를 형성하도록 책임을 할당하라 
- PROTECTED VARIATIONS 패턴은 책임 할당의 관점에서 캡슐화를 설명한 것 
- "설계에서 변하는 것이 무엇인지 고려하고 변하는 개념을 캡슐화하라"
- 변경이 될 가능성이 높음 -> 캡슐화할 것



---

## 책임 주도 설계의 대안
- 최대한 빠르게 목적한 기능을 수행하는 코드를 작성하고 코드 상에 명확하게 드러나는 책임들을 올바른 위치로 이동 (리팩토링)
- 리팩토링 : 이해하기 쉽고 수정하기 쉬운 소프트웨어로 개선하기 위해 겉으로 보이는 동작은 바꾸지 않은 채 내부구조를 변경하는 것

### 메서드 응집도
- 몬스터 메서드 : 응집도가 낮으며 이해하기도 어렵고 재사용도 어려우며 변경하기도 어려운 긴 메서드
- 메서드를 응집도 있는 수준으로 분해할 것 : 긴 메서드를 작고 응집도 높은 메서드로 분리해라 

### 객체를 자율적으로 만들자 
- 메서드가 사용하는 데이터를 저장하고 있는 클래스로 메서드를 이동 
  - 데이터를 사용하는 메서드를 데이터를 가진 클래스로 이동시키고 나면 캡슐화와 높은 응집도, 낮은 결합도를 가지는 설계를 얻게 됨
- POLYMORPHISM 패턴 & PROTECTED VARIATIONS 패턴 


> 책임 주도 설계 방법에 익숙하지 않다면 일단 데이터 중심으로 구현한 후 이를 리팩터링하더라도 유사한 결과를 얻을 수 있다. 
> 처음부터 책임 주도 설계 방법을 따르는 것보다 동작하는 코드를 작성한 후에 리팩터링하는 것이 더 훌륭한 결과믈을 낳을 수도 있다. 캡슐화, 결합도, 응집도를 이해하고 훌륭한 객체지향 원칙을 적용하기 위해 노력한다면 책임 주도 설계 방법을 단계적으로 따르지 않더라도 유연하고 깔끔한 코드를 얻을 수 있을 것이다. 

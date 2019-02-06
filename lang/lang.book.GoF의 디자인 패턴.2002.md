# ch 1 서론

## 디자인 패턴 카탈로그
* Abstract Factory: 구체적 클래스 지정않고 관련성 갖는 객체들의 집합 생성하거나 서로 독립적 객체들 집합을 생성 가능한 인터페이스 제공
* Adaptor: 클래스 인터페이스를 다른 인터페이스로 변환. 호환성 없는 인터페이스 때문에 함께 동작할 수 없는 클래스들이 함께 작동하게
* Bridge: 구현부에서 추상층 분리하여 각자 독립적 변형
* Builder: 복합 객체 생성 과정과 표현 방법 분리하여 동일 생성 절차에서 서로 다른 표현 결과 만듦
* Chain of Responsibility(책임 연쇄): 요청 처리 기회를 하나 이상 객체에 부여하여 요청 객체와 요청 받는 객체 간 결합 회피. 요청 받는 객체를 연쇄적 묶음
* Command: 요청을 객체 형태 캡슐화. 매개변수화, 저장, 로깅, 취소 지원
* Composite: 객체들 관계를 트리 구조 구성하여 부분-전체 계층 표현. 단일/복합 객체를 동일하게 다루도록
* Decorator: 상황/용도에 따라 객체에 책임 덧붙임. 기능 확장 필요시 서브클래싱 대신 사용
* Facade: 서브시스템 인터페이스 집합에 대해 하나의 통합 인터페이스 제공(사용 편의성 위한 상위 수준 인터페이스)
* Factory Method: 객체 생성 인터페이스 미리 정의, 인스턴스 만들 클래스 결정은 서브클래스에서(클래스 인스턴스 만드는 시점을 서브클래스로 미룸)
* Flyweight: 크기 작은 여러 객체 공유
* Interpreter: 해석기 정의
* Iterator: 내부 표현부 노출 않고 객체 집합 원소들 순차적 접근
* Mediator(중재자): 집합에 속한 객체들 상호작용을 캡슐화하는 객체 정의. 객체들이 직접 서로를 참조하지 않음(소결합:loose coupling) 촉진
* Memento: 캡슗화 위배하지 않고 객체 내부 상태를 잡아 실체화하여 이후 해당 객체가 그 상태로 복귀 가능
* Observer: 객체 사이 일대 다 의존 관계 정의. 객체 상태 변경시 그 객체에 의존성 가진 다른 객체들이 변화 통지받아 자동 갱신
* Prototype: 생성 객체 종류 명세화에 원형 예시물 이용. 원형을 복사하여 새 객체 생성
* Proxy: 다른 객체 접근 통제를 위해 대리자(surrogate) 또는 자리채움자(placeholder) 제공
* Singleton: 클래스 인스턴스 하나임을 보장. 이 인스턴스에 접근하는 전역 접촉점 제공
* State: 객체 내부 상태 따라 스스로 행동 변경 허가
* Strategy: 동일 계열 알고리즘 정의, 캡슐화, 상호교환 가능
* Template Method: 객체 연산에 알고리즘 뼈대만 정의. 단계별 구체적 처리는 서브클래스로 미룸
* Visitor: 객체 구조 구성 원소에 대한 수행 연산 표현. 클래스 변경 없이 새 연산 정의 가능



# ch 3 생성 패턴

## Abstract Factory

## Builder

## Factory Method

## Prototype

## Singleton



# ch 4 구조 패턴

## Adaptor

## Bridge

## Composite

## Decorator

## Facade

## Flyweight

## Proxy



# ch 5 행동 패턴

## Chain of Responsibility(책임 연쇄)

## Command

## Interpreter

## Iterator

## Mediator(중재자)

## Memento

## Observer

## State

## Strategy

## Template Method

## Visitor

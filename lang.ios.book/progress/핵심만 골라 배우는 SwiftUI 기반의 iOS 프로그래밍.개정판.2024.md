## CHAPTER 4 Xcode 14 플레이그라운드 12


## CHAPTER 5 스위프트 데이터 타입, 상수, 그리고 변수 25
* 타입: Int, Float, Double, Boolean, 문자, 문자열, 특수문자
* 변수: var foo: Int = 10
* 상수: let foo: String
* 타입 애너테이션 혹은 타입 추론
* 튜플: let foo = (a: 10, b: 1.23, c: "bar")
  * 인덱스 혹은 키/값
* 옵셔널: var foo: Int?
  * if foo != nil {} else {}
  * foo!: force unwrapping
  * if let bar = foo { ... bar ... } else: optional binding
    * if let foo { ... foo ... } else {}
* 타입 캐스팅, 타입 검사
  * 업캐스팅: 상위 클래스로 변형: as
    * let fooBtn: UIButton = UIButton(); let fooCtl = fooBtn as UIControl
  * 다운캐스팅: 클래스를 다른 (하위)클래스로 변환: as!, as?
    * let fooView: UIScrollView = UIScrollView(); let fooTextView = fooScrollView as! UITextView
      * 실제로는 런타임 오류 발생
    * if let fooTextView = fooScrollView as? UITextView {} else {}
    * 타입검사: is 키워드: if foo is Foo {}
    * let foo = bar.object(forKey: "fee") as! String


## CHAPTER 6 스위프트 연산자와 표현식 43
* 범위연산자
  * 닫힌: x...y
  * 반 개방: x..<y
  * 단방향: x..., ...y
* 삼항연산자: (cond) ? foo : bar
* nil 병합연산자
  * let foo: String? = nil; print(foo ?? "bar")


## CHAPTER 7 스위프트의 제어 흐름 55
* for foo in foos {}; for idx in 1...5 {}
* while (cond) {}
* repeat {} while (cond)
* break: 반복문 중단
* continue
* if {} else {}
* guard (cond) {}: 조건이 false 일때 중괄호 내부가 실행되며, 중괄호 내부는 반드시 return, break, continue, throw 등이 필요


## CHAPTER 8 스위프트의 switch 구문 64
* break 없어도 case 중단됨. 결합 가능
  * switch(cond) { case 0,1,2: print(1); case 3: print(2) }
* fallthrough: 다음 case 로 이어짐
  * switch(cond) { case 0: print(0); fallthrough; case 1: print(1) }
* 범위매칭
  * switch(cond) { case 0...5: print(1); case 6...10: print(2) }
* where
  * switch(cond) { case 0...5 where cond: print(1) }


## CHAPTER 9 스위프트의 함수, 메서드, 클로저 70
* 함수: func foo (foo: String, bar: Int, ...) -> String { ... }
    * 함수 내부에 표현식이 하나일 경우 return 키워드 생략 가능
* 외부 매개변수명
  * 외부 매개변수명은 언더스코어 _ 로 제거 가능
* 여러 결과값 반환: 튜플
  * func foo() { return (fee, bee, boo) }
    * let bar = foo(); print(bar.fee)
* 가변 매개변수: 다수의 매개변수 처리: func() foo(_ fees: String...) {}
* 매개변수는 상수: 변수로 사용하기 위해서는 shadow copy 필요
  * 매개변수 변경을 유지하려면: 입출력 매개변수로 선언, 함수호출시 매개변수에 & 추가
    * func foo(_ fee: inout Int) -> Int { fee += fee; return fee }
      * foo(&bar)
* 매개변수인 함수
* 클로저 표현식: 이름이 없는 함수: 비동기 메소드 호출에 대한 완료 핸들러 선언시 사용
  * let foo = { print(1) }
  * let foo = {(_ fee: Int, _ fuu: Int) -> Int in return (fee * fuu) }
  * 클로저 표현식 시작을 in 키워드로 표시
* 클로저 단순화: 약식 인수 이름
  * let foo = { (fee: Int, fuu: Int) -> Int in (fee + fuu) }
    * let foo: (Int, Int) -> Int = { $0 + $1 }


## CHAPTER 10 스위프트의 객체지향 프로그래밍 기초 85
* 선언: class Foo: FooParent {}
  * 프로퍼티, 인스턴스 메소드, 타입 메소드
  * 인스턴스 메소드: class 키워드 없음
  * 타입 메소드: class 키워드 추가
* 클래스 인스턴스
  * var foo: Foo = Foo()
  * 초기화: 생성자: 클래스의 init() 메소드
  * 소멸자: 클래스의 deinit() 메소드
* 연산 프로퍼티: getter, setter
  * var foo: Float { get {}; set() {}; }
* 저장 프로퍼티
  * 지연 저장 프로퍼티: 프포퍼티를 최초 접근할 때만 초기화: lazy
    * lazy var foo: String = {}()
* self: 기본값을(자동으로) 간주되나
  * 프로퍼티/메소드를 클로저 표현식 내부에서 참조할때 필요
  * 함수 매개변수와 클래스 프로퍼티가 동일할 경우 필요
* 프로토콜: 클래스가 반드시 포함해야 하는 메소드, 프로퍼티 정의
  * protocol Foo { var fee: String { get }; func fuu() -> String; }
    * class Bar: Foo {}
* 불투명 반환 타입: 지정된 프로토콜을 따르는 모든 타입이 반환 가능: 키워드 some 을 프로토콜 이름 앞에 붙여 선언
  * func foo() -> some Foo {}


## CHAPTER 11 스위프트의 서브클래싱과 익스텐션 개요 100
* 스위프트는 단일상속
* 오버라이딩: 부모 클래스 메소드의 매개변수 개수/타입, 반환하는 타입이 정확히 일치해야 함
  * super.foo()
  * 하위클래스 초기화(생성자)는 부모클래스의 생성자와 개별적으로 존재 가능
    * super.init()
* 클래스 익스텐션: 하위클래스 생성 없이 기능들 추가, 언어와 sdk 프레임워크에 기능 추가시 유용
  * extension Double {}


## CHAPTER 12 스위프트 구조체와 열거형 107
* struct Foo { init() {} }
  * let foo = Foo()
  * 복사, 전달될 때: 클래스 인스턴스 타입은 참조 타입이나, 구조체 인스턴스 타입은 값 타입(복사)
  * 구조체는 상속 지원하지 않음, 소멸자 없음
* enum Foo { case fee; case fuu;  }
  * func bar(foo: Foo) { switch foo { case .fee: print(1); case .fuu: print(2) } }


## CHAPTER 13 스위프트 프로퍼티 래퍼 115


## CHAPTER 14 스위프트의 배열과 딕셔너리 컬렉션으로 작업하기 122


## CHAPTER 15 스위프트 5의 에러 핸들링 이해하기 133


## CHAPTER 16 SwiftUI 개요 140


## CHAPTER 17 SwiftUI 모드로 Xcode 이용하기 145


## CHAPTER 18 SwiftUI 아키텍처 168


## CHAPTER 19 기본 SwiftUI 프로젝트 분석 171


## CHAPTER 20 SwiftUI로 커스텀 뷰 생성하기 175


## CHAPTER 21 SwiftUI 스택과 프레임 192


## CHAPTER 22 SwiftUI 상태 프로퍼티, Observable, State, Environment 객체 205


## CHAPTER 23 SwiftUI 예제 튜토리얼 215


## CHAPTER 24 스위프트 구조화된 동시성 개요 230


## CHAPTER 25 스위프트 액터 소개 249


## CHAPTER 26 SwiftUI 동시성 및 생명 주기 이벤트 수정자 257


## CHAPTER 27 Observable 객체와 Environment 객체 튜토리얼 264


## CHAPTER 28 AppStorage와 SceneStorage를 사용한 SwiftUI 데이터 지속성 272


## CHAPTER 29 SwiftUI 스택 정렬과 정렬 가이드 281


## CHAPTER 30 SwiftUI List와 내비게이션 298


## CHAPTER 31 SwiftUI List와 NavigationStack 튜토리얼 314


## CHAPTER 32 분할 뷰 내비게이션 개요 333


## CHAPTER 33 NavigationSplitView 튜토리얼 338


## CHAPTER 34 List, OutlineGroup, DisclosureGroup 개요 346


## CHAPTER 35 SwiftUI List, OutlineGroup, DisclosureGroup 튜토리얼 354


## CHAPTER 36 LazyVGrid 및 LazyHGrid로 SwiftUI 그리드 구축하기 365


## CHAPTER 37 Grid와 GridRow를 사용하여 SwiftUI 그리드 구축하기 377


## CHAPTER 38 SwiftUI에서 탭 그리고 페이지 뷰 구축하기 389


## CHAPTER 39 SwiftUI에서 콘텍스트 메뉴 바인딩하기 394


## CHAPTER 40 SwiftUI 그래픽 드로잉 기초 398


## CHAPTER 41 SwiftUI 애니메이션과 전환 408


## CHAPTER 42 SwiftUI에서 제스처 작업하기 421


## CHAPTER 43 사용자 정의 SwiftUI ProgressView 생성하기 430


## CHAPTER 44 SwiftUI 차트로 데이터 표시하기 437


## CHAPTER 45 SwiftUI 차트 튜토리얼 445


## CHAPTER 46 SwiftUI DocumentGroup 개요 450


## CHAPTER 47 SwiftUI DocumentGroup 튜토리얼 461


## CHAPTER 48 코어 데이터와 SwiftUI 소개 469


## CHAPTER 49 SwiftUI 코어 데이터 튜토리얼 477


## CHAPTER 50 SwiftUI 코어 데이터와 클라우드킷 저장소 개요 493


## CHAPTER 51 SwiftUI 코어 데이터와 클라우드킷 튜토리얼 499


## CHAPTER 52 시리킷 소개 511


## CHAPTER 53 SwiftUI 시리킷 메시징 익스텐션 튜토리얼 519


## CHAPTER 54 시리 단축어 앱 통합 개요 527


## CHAPTER 55 SwiftUI 시리 단축어 튜토리얼 534


## CHAPTER 56 SwiftUI와 위젯킷으로 위젯 빌드하기 556


## CHAPTER 57 SwiftUI 위젯킷 튜토리얼 565


## CHAPTER 58 위젯킷 크기 지원 580


## CHAPTER 59 SwiftUI 위젯킷 딥링크 튜토리얼 586


## CHAPTER 60 위젯킷 위젯에 구성 옵션 추가하기 593


## CHAPTER 61 UIView를 SwiftUI에 통합하기 601


## CHAPTER 62 UIViewController를 SwiftUI와 통합하기 611


## CHAPTER 63 SwiftUI를 UIKit에 통합하기 619


## CHAPTER 64 앱 스토어에 iOS 16 애플리케이션 등록을 위한 준비와 제출하기 632

# DesignPattern_Study_Singleton

# Notion Link
https://five-cosmos-fb9.notion.site/Singleton-51509596ce8f4db8b78815cd5bf5bc67

# 단일체(Singleton)

### Singleton 패턴

오직 한 개의 클래스 인스턴스만을 갖도록 보장하고

이에 대한 전역적인 접근점을 제공하는 방법

<aside>
💡 프로세스가 실행 중에 오직 하나의 오브젝트만 생성이 되도록 강제하도록 하는 디자인 패턴

</aside>

- 커넥션 풀, 스레드 풀, 디바이스 설정 객체등과 같은 성격의 인스턴스를 여러 개 만들게 되면 자원을 낭비하게 되거나 버그를 발생시킬 수 있으므로 오직 하나의 인스턴스만 생성하도록 하고 사용하도록 하는 것이 이 패턴의 목적이라 볼 수 있다.

**Singleton 패턴의 문제점**

- Multi-Thread 환경에서 안전하지 않다. 즉, Thread Safe하지 못하다.
- 여러 쓰레드가 옹유되고 있는 상황에서는 원하는대로 하나의 인스턴스가 아니라 여러 개의 인스턴스가 발생될 위험이 있다.
- 뿐만 아니라 인스턴스가 상태를 유지해야하는 상황에서 싱글톤은 더 많은 고려사항이 발생한다.
    - 싱글톤 객체 안의 어떤 변수가 있을 때 이 변수가 각기 다른 쓰레드에서 공유하게 되는 상황에 일관성을 유지하지 못할 수 있다.

**Multi-Thread 환경에서의 Singleton**

1. **정젹 변수에 인스턴스를 만들어 바로 초기화**
    1. 정적 변수는 객체가 생성되기 전 **`클래스가 메모리에 로딩될 때`** 만들어져 초기화가 한 번만 실행되게 된다.
    2. 또한, 프로그램이 종료될 때까지 없어지지 않고 메모리에 계속 상주하며 클래스에서 생성된 모든 객체에서 참조할 수 있다. 
2. **인스턴스를 만드는 메서드에 동기화 하는 방법**
    1. 객체 생성 자체로는 로드 시점에 결정되어 하나의 객체만을 사용하지만
    2. 특정 변수에 접근하는 것은 여러 쓰레드가 동시적으로 접근하기 때문에 중요하다.
    3. 이를 해결하기 위해 synchronized 라는 키워드를 통해 여러 쓰레드에서 동시에 접근하는 것을 막는 방법으로 이를 해결한다.

**일반적인 오브젝트를 만들고자 할 때**

- 정의 클래스가 있을 것이고
- 개별적인 오브젝트를 만들어 내게 될 것이다.
- 프로세스 이기 때문에 다른 메모리 공간을 가지고 있게 될 것이다.

![image](https://user-images.githubusercontent.com/18654358/156861527-f153db83-3aee-4a98-b19a-22be44d60bf7.png)

**싱글톤 패턴을 적용한다면 위의 구조가 아래와 같이 변경될 수 있다.**

![image](https://user-images.githubusercontent.com/18654358/156861531-adf6037f-16a8-43d5-9365-2b33ba35adf2.png)

**메모리 쪽을 조금 더 자세히 표현해보자면 이렇게 표현될 것이다.**

![image](https://user-images.githubusercontent.com/18654358/156861544-502df892-3b39-424c-a2ca-6194450a0911.png)

**언어에 따라 싱글톤을 구현하는 방법과 방식은 여러가지일 수 있다.**

**`싱글톤 패턴이라는 것에 포커싱을 맞추어 가장 중요한 점은`**

- 하나의 프로세스 안에서 오브젝트를 만들 때
- 단 하나의 오브젝트만 만들어지게 강제하는 것이다!
- 싱글톤 패턴을 사용하게 되는 예
    - 하나의 오브젝트가 리소스를 많이 차지할 때
    - 외부와 연결되는데 외부와의 연결이 단 한개만 있어야 할 때

### 활용성

- 클래스의 인스턴스가 오직 하나여야 함을 보장하고, 잘 정의된 접근점(Access Point)으로 모든 사용자가 접근할 수 있또록 해야 할 때
- **`유일한 인스턴스가 서브클래싱으로 확장되어야 하며, 사용자는 코드의 수정 없이 확장된 서브 클래스의 인스턴스를 사용할 수 있어야 할 떄`**

![image](https://user-images.githubusercontent.com/18654358/156861562-4048321a-22ea-4fbe-8bfd-0e50a2bbe0a2.png)

### 참여자

SIngleton

- Instance() 연산을 정의하며 유일한 인스턴스로 접근할 수 있또록 한다.
- Instance() 연산은 클래스 연산이다.
- 유일한 인스턴스를 생성하는 책임을 맡는다.

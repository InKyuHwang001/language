# 상속

---

- [상속의 의미](##상속의의미)
- [상속의 예](##상속의예)
- [생성과정과 형변환](##생성과정과형변환)
- [메서드 재정의(overridng)](##메서드재정의(overridng))
- [메서드 재정의와 가상 메서드 원리](##메서드재정의와가상메서드원리)
- [다형성과 다형성을 사용하는 이유](##다형성과다형성을사용하는이유)
- [상속의 사용처](##상속의사용처)
- [다운 캐스팅과 instanceof](##다운캐스팅과instanceof)

---

## 상속의의미

- 구현된 클래스보다 더 구체적인 기능을 가진 클래스를 구현해야 할때

- 상속의 문법

  ```java
  class B extends A{
    
  }
  ```

  자바의 클래스의 경우 **단일 상속**만을 지원

---

## 상속의예

### 일반 고객 구현

```java
public class Customer {

	private int customerID;
	private String customerName;
	private String customerGrade;
	int bonusPoint;
	double bonusRatio;
	
	public Customer() {
		customerGrade = "SILVER";
		bonusRatio = 0.01;
	}
	
	public int calcPrice(int price) {
		bonusPoint += price * bonusRatio;
		return price;
	}
	
	public String showCustomerInfo() {
		return customerName + "님의 등급은 " + customerGrade + 
				"이며, 보너스 포인트는" + bonusPoint + "입니다";
		
	}
}
```

### 우수 고객 구현

```java
public class VIPCustomer extends Customer{

	private int agentID;
	double salesRatio;
	
	public VIPCustomer() {
		customerGrade = "VIP";    //오류 발생
		bonusRatio = 0.05;
		salesRatio = 0.1;
	}
	
	public int getAgentID() {
		return agentID;
	}
}
```

### protected 접근 제어자

- 상위 클래스에 선언된 **private** 멤버 변수는 **하위 클래스**에서 **접근 할 수 없음**
- 외부 클래스는 접근 할 수 없지만, 하위 클래스는 접근 할 수 있도록 **protected** 접근 제어자를 사용

```java
	protected int customerID;
	protected String customerName;
	protected String customerGrade;

	//getter, setter 구현
	...
	public int getCustomerID() {
		return customerID;
	}

	public void setCustomerID(int customerID) {
		this.customerID = customerID;
	}

	public String getCustomerName() {
		return customerName;
	}

	public void setCustomerName(String customerName) {
		this.customerName = customerName;
	}

	public String getCustomerGrade() {
		return customerGrade;
	}

	public void setCustomerGrade(String customerGrade) {
		this.customerGrade = customerGrade;
	}
```

---

## 생성과정과형변환

### 하위 클래스가 생성 되는 과정

- 하위 클래스를 생성하면 **상위 클래스가 먼저 생성** 됨
  - new VIPCustomer()를 호출하면 Customer()가 먼저 호출됨
- 하위 클래스의 생성자에서는 반드시 **상위 클래스의 생성자를 호출함

### super 키워드

- 하위 클래스에서 가지는 **상위 클래스에 대한 참조** 값

- super()는 상위 클래스의 **기본 생성자를 호출** 함

- 하위 클래스에서 **명시적**으로 상위 클래스의 생성자를 호출하지 **않으면** **super()**가 호출 됨
   ( 이때 반드시 상 위 클래스의 기본 생성자가 존재 해야 함)

- 상위 클래스의 **기본 생성자가 없는 경우** ( 다른 생성자가 있는 경우 ) 하위 클래스에서는 생성자에서는 super를 이용하여 **명시적으로** 상위 클래스의 생성자를 호출 함

- super는 생성된 상위 클래스 인스턴스의 참조 값을 가지므로 super를 이용하여 **상위 클래스의 메서드나 멤버 변수에 접근**할 수 있음

### 상속에서 인스턴스 메모리의 상태

- 상위 클래스의 인스턴스가 먼저 생성되고, 하위 클래스의 인스턴스가 생성 됨
- 힙 메모리 상에 상위 클래스의 멤버 변수가 먼저 생성되고 하위 클래스의 멤버 변수가 생성됨

### 형 변환(업캐스팅)
- 상위 클래스로 변수를 선언하고 하위 클래스의 생성자로 인스턴스를 생성
Customer customerLee = new VIPCustomer();

- 상위 클래스 타입의 변수에 하위 클래스 변수가 대입;

  - VIPCustomer vCustomer = new VIPCustomer();

    addCustomer(vCustomer);

    int addCustomer(Customer customer){
    }

### 형 변환과 메모리

**Customer vc = new VIPCustomer();** 에서 vc가 가리키는 것은?

- VIPCustomer() 생성자에 의해 VIPCustomer 클래스의 모든 멤버 변수에 대한 메모리는 생성되었지만, 
   변수의 타입이 Customer 이므로 실제 **접근 가능한 변수나 메서드**는 **Customer의 변수와 메서드**임

---

## 메서드재정의(overridng)

### 하위 클래스에서 메서드 재정의 하기

- **오버라이딩(overriding)** : 상위 클래스에 정의된 메서드의 구현 내용이 하위 클래스에서 구현할 내용과 맞지 않는 경우 **하위 클래스에서 동일한 이름**의 메서드를 재정의 할 수 있음
- VIPCustomer 클래스의 calcPrice()는 할인율이 적용되지 않음
- 재정의 하여 구현해야 함(**반환값, 메서드 이름, 메게변수의 수와 타입이 동일**)

### @overriding (annotation)

- 애노테이션은 원래 주석이라는 의미
- 컴파일러에게 특별한 정보를 제공해주는 역할
  - @Overriding: 재정의돈 메서드
  - @FunctionalInterface: 함수형 인터페이스
  - @Deprecated: 이후 버젼에서 사용되지 않을 수 있는 변수, 메서드
  - @SuppressWarnings: 경고무시

### 형 변환과 오버라이딩 메서드 호출

Customer vc = new VIPCustomer();
vc 변수의 타입은 Customer지만 **인스턴스의 타입은 VIPCustomer** 임 (즉, **vip의 메서드**가 호출됨)
자바에서는 항상 인스턴스의 메서드가 호출 됨 (가상메서드의 원리)
자바의 모든 메서드는 가상 메서드(virtual method) 임

---

## 메서드재정의와가상메서드원리

### 메서드는 어떻게 호출되고 실행 되는가?

**Java의 메서드는 모두 가상메서드**이다.

- 메서드(함수)의 이름은 **주소값**을 나타냄
- 메서드는 **명령어의 set** 이고 프로그램이 로드되면 메서드 영역**(코드 영역)**에 명령어 **set이 위치**
- 해당 메서드가 **호출** 되면 명령어 set 이 있는 **주소를 찾아** 명령어가 실행됨
- 이때 메서드에서 사용하는 **변수들**은 **스택 메모리**에 위치 하게됨
- 따라서 **다른 인스턴스라**도 같은 메서드의 코드는 같으므로 **같은 메서드가 호출**됨
- **인스턴스가 생성**되면 변수는 **힙 메모리**에 따로 생성되지만, 메서드 **명령어 set**은 처음 **한번만 로드** 됨

### 가상 메서드의 원리

- 가상 메서드 테이블(vitual method table)에서 해당 메서드에 대한 address를 가지고 있음
- 재정의된 경우는 재정의 된 메서드의 주소를 가리킴

## 다형성과다형성을사용하는이유

### 정의

- 하나의 코드가 **여러 자료형으로 구현**되어 실행되는 것

- **같은 코드**에서 여러 **다른 실행 결과**가 나옴

- 정보은닉, 상속과 더불어 객체지향 프로그래밍의 가장 큰 특징 중 하나임

- 다형성을 잘 활용하면 유연하고 확장성있고, 유지보수가 편리한 프로그램을 만들수 있음

```java
class Animal{
	
	public void move() {
		System.out.println("동물이 움직입니다.");
	}
	
	public void eating() {
		
	}
}

class Human extends Animal{
	public void move() {
		System.out.println("사람이 두발로 걷습니다.");
	}
	
	public void readBooks() {
		System.out.println("사람이 책을 읽습니다.");
	}
}

class Tiger extends Animal{
	
	public void move() {
		System.out.println("호랑이가 네 발로 뜁니다.");
	}
	
	public void hunting() {
		System.out.println("호랑이가 사냥을 합니다.");
	}
}


class Eagle extends Animal{
	public void move() {
		System.out.println("독수리가 하늘을 날아갑니다.");
	}
	
	public void flying() {
		System.out.println("독수리가 날개를 쭉 펴고 멀리 날아갑니다");
	}
}



public class AnimalTest {

	public static void main(String[] args) {

		Animal hAnimal = new Human();
		Animal tAnimal = new Tiger();
		Animal eAnimal = new Eagle();
		
		AnimalTest test = new AnimalTest();
		test.moveAnimal(hAnimal);
		test.moveAnimal(tAnimal);
		test.moveAnimal(eAnimal);
		
		ArrayList<Animal> animalList = new ArrayList<Animal>();
		animalList.add(hAnimal);
		animalList.add(tAnimal);
		animalList.add(eAnimal);
		
		for(Animal animal : animalList) {
			animal.move();
		}
	}	
	
	public void moveAnimal(Animal animal) {
		animal.move();
		
	}
}

```

### 사용 이유

- **다른 하위 클래스를 만들 경우**

- 상속과 메서드 **재정의를 활용**하여 **확장성** 있는 프로그램을 만들 수 있음
- 그렇지 **않는 경우** 많은 **if-else if문**이 구현되고 코드의 유지보수가 어려워짐
- 여러 클래스를 하나의 타입(상위 클래스)으로 핸들링 할 수 있음

---
## 상속의사용처
### IS-A 관계(is a relationship : inheritance)
- 일반적인(general) 개념과 구체적인(specific) 개념과의 관계
- 상위 클래스 : 하위 클래스보다 일반적인 개념 ( 예: Employee )
- 하위 클래스 : 상위 클래스보다 구체적인 개념들이 더해짐 ( 예: Engineer, Manager...)
- 상속은 클래스**간**의 **결합도가 높은** 설계
- 상위 클래스의 수정이 많은 하위 클래스에 영향을 미칠 수 있음
- 계층구조가 복잡하거나 **hierarchy가 높으면 좋지 않음**
### HAS-A 관계(composition)
- 클래스가 다른 클래스를 포함하는 관계 ( 변수로 선언 )
- 코드 재사용의 가장 일반적인 방법
- Student가 Subject를 포함하는 Library를 구현할 때 ArrayList 생성하여 사용
	상속하지 않음

---

## 다운캐스팅과instanceof

### 정의

- 업캐스팅된 클래스를 다시 **원래의 타입으로** 형 변환
- 하위 클래스로의 형 변환은 **명시적**으로 해야 함

```java
Customer vc = new VIPCustomer();              //묵시적
VIPCustomer vCustomer = (VIPCustomer)vc;      //명시적
```

### instanceof를 이용하여 인스턴스의 형 체크

- 원래 인스턴스의 형이 맞는지 여부를 체크하는 키워드 맞으면 true 아니면 false를 반환 

```java
public void testDownCasting(ArrayList<Animal> list) {
		
		for(int i =0; i<list.size(); i++) {
			Animal animal = list.get(i);
		
			if ( animal instanceof Human) {
				Human human = (Human)animal;
				human.readBooks();
			}
			else if( animal instanceof Tiger) {
				Tiger tiger = (Tiger)animal;
				tiger.hunting();
			}
			else if( animal instanceof Eagle) {
				Eagle eagle = (Eagle)animal;
				eagle.flying();
			}
			else {
				System.out.println("error");
			}
		
		}
}
```


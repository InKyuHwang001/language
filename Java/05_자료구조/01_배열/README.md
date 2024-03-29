# 배열
---

- [배열](##배열)
- [2차원배열](##2차원배열)
- [ArrayList](##ArrayList)

---

## 배열

### 정의

- 동일한 자료형의 순차적 자료 구조
- 인뎃스 연산자[]를 이용 -> 빠른 참조
- 물리적 논리적 위치가 동일
- 정해진 크기가 있음
- **요소의 추가와 제거시 다른 요소들의 이동이 필요**
- ArrayList, Vector

### 선언과 초기화

- 선언

```java
int[] arr1 = new int[10];
int arr2[] = new int[10];
```

- 초기화
  - 선언과 동시에 자료형에 따른 초기화
  - 필요시 초기값 지정 가능

```java
int[] numbers = new int[] {10, 20, 30};  //개수 생략해야 함

int[] numbers = {10, 20, 30};            // new int[]  생략 가능 

int[] ids; 
ids = new int[] {10, 20, 30};            // 선언후 배열을 생성하는 경우는 new int[] 생략할 수 없음
```

### 배열의 길이와 원소의 개수는 동일하지 않음

- 100개를 선언하고 50개만 사용

```java
double[] dArr = new double[5];
		
dArr[0] = 1.1;  
dArr[1] = 2.1; 
dArr[2] = 3.1; 
		
double mtotal = 1;
for(int i = 0; i< dArr.length; i++) {
	mtotal *= dArr[i];
}
		
System.out.println(mtotal); //오류

//해결책
double[] dArr = new double[5];
int count = 0;
dArr[0] = 1.1; count++; 
dArr[1] = 2.1; count++;
dArr[2] = 3.1; count++;
		
double mtotal = 1;
for(int i = 0; i< count; i++) {
	mtotal *= dArr[i];
}
		
System.out.println(mtotal);
```

### for 문 변형

```java
for( 변수 : 배열) {

}

// 예시
public class CharArrayTest {

	public static void main(String[] args) {

		char[] alpahbets = new char[26];
		char ch = 'A';
		
		for(int i = 0; i<alpahbets.length; i++) {
			
			alpahbets[i] = ch++;
		}
		
		for(char alpha : alpahbets) {
			System.out.println(alpha +","+ (int)alpha);
		}

	}

}
```

---

## 2차원배열

```java
int[][] arr = new int[2][4];


public class TwoDimensionTest {

	public static void main(String[] args) {
		int[][] arr = { {1,2,3}, {4,5,6,7}};
		int i, j;
		
		for(i =0; i<arr.length; i++) {
			for(j=0; j<arr[i].length; j++) {
				System.out.print(arr[i][j] + " ");
			}
			System.out.println(", \t" + arr[i].length);
			System.out.println();
		}
	}
}

```

---

## ArrayList

### 주요 메서드

- .add()
- .size()
- .get(int index)
- .remove(int index)
- .isEmpty()

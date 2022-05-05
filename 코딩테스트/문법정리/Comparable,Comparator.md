### 날짜  2022-04-23 00:48
### 주제: #정렬 #객체정렬 #코딩테스트 
---
### 메모
> 객체를 비교하기 위해 Comparable, Comparator 개념을 참고문헌을 보고 정리 해보았다. 
### 출처(참고문헌)
- https://st-lab.tistory.com/243
### 연결문서
- [[익명클래스]]
- [[(문제)문자열 내 마음대로 정렬하기]]
# Comparable, Comparator를 이용하여  java 객체 정렬

## 비교하기
- primitive type(기본 자료형)은 자바 자체에서 제공되기에 별다른 처리없이 부등호로 비교가 가능하다. 
- 객체를 비교하기 위해서 Comparable, Comparator가 필요하다.

## Comparable 

- 인터페이스, compareTo(T o)를 재정의 
- 자기 자신(this)과 매개변수 객체를 비교
- lang 패키지에 있어서 import 안해도 된다.
  

## Comparator
- 참고
  -  Java8 부터는 Interface에서도 일반 메소드를 구현할 수 있도록 변경되어서 추상 메서드인 compare(T o1, T o2) 만 필수적으로 재정의 하면 된다. 나머지는 default, static 로 구현된 메서드들이다.
  -  default로 선언된 메소드는 재정의(Override)를 할 수 있고, static은 재정의를 할 수 없다는 차이다.
  
- 인터페이스, compare(T o1, T o2)를 재정의 
- 두 매개변수 객체를 비교
- util패키지에 있어 import 필요하다.

## 사용방법
### Comparable
```java

class Student implements Comparable<Student> {
 
	int age;			// 나이
	int classNumber;	// 학급
	
	Student(int age, int classNumber) {
		this.age = age;
		this.classNumber = classNumber;
	}
	
	1. 자기자신.age - 매개변수객체.age 비교 
	@Override
	public int compareTo(Student o) {
		return this.age - o.age;
	}
	
	2. >, <, == 비교
	@Override
	public int compareTo(Student o) {
    
		// 자기자신의 age가 o의 age보다 크다면 양수
		if(this.age > o.age) {
			return 1;
		}
		// 자기 자신의 age와 o의 age가 같다면 0
		else if(this.age == o.age) {
			return 0;
		}
		// 자기 자신의 age가 o의 age보다 작다면 음수
		else {
			return -1;
		}
	}
}
```

- 1, 2번 둘 중 하나의 방법을 사용하면 된다.
- 1번을 사용하면 3가지 조건문을 사용하지 않아도 된다.
 
**1번 방법 사용 시 주의할 점 : 만약 int 타입을 비교 한다면** 
> -2,147,483,648 - 1 = ~~-2,147,483,649~~ 이런 경우
> -2,147,483,649가 될 것이라고 예상하지만 2,147,483,647인 int형의 최대반환값이 나오게 되는데 이것을 **Underflow** 라고 한다. 
> 
>  2,147,483,647 + 1 = ~~2,147,483,648~~  이런 경우
>  2,147,483,647가 될 것이라고 예상하지만 -2,147,483,649인 int형의 최소값이 나오게 되는데 이것을**Overflow** 라고 한다.
	
	
### Comparator
```java
import java.util.Comparator;	// import 필요
class Student implements Comparator<Student> {
 
	int age;			// 나이
	int classNumber;	// 학급
	
	Student(int age, int classNumber) {
		this.age = age;
		this.classNumber = classNumber;
	}
	1. 두 개의 매개변수 차를 비교
	@Override
	public int compare(Student o1, Student o2) {
 
		/*
		 * 만약 o1의 classNumber가 o2의 classNumber보다 크다면 양수가 반환 될 것이고,
		 * 같다면 0을, 작다면 음수를 반환할 것이다.
		 */
		return o1.classNumber - o2.classNumber;
	}
	
	2. >, <, == 비교
	@Override
	public int compare(Student o1, Student o2) {
    
		// o1의 학급이 o2의 학급보다 크다면 양수
		if(o1.classNumber > o2.classNumber) {
			return 1;
		}
		// o1의 학급이 o2의 학급과 같다면 0
		else if(o1.classNumber == o2.classNumber) {
			return 0;
		}
		// o1의 학급이 o2의 학급보다 작다면 음수
		else {
			return -1;
		}
	}
}
```
- 자기자신과 상관없는 독립적으로 매개변수로 넘겨진 객체 두개를 비교할 수 있다.


## 익명클래스 활용하기
```java
import java.util.Comparator;
 
public class Test {
	public static void main(String[] args)  {
 
		Student a = new Student(17, 2);	// 17살 2반
		Student b = new Student(18, 1);	// 18살 1반
		Student c = new Student(15, 3);	// 15살 3반
			
		// comp 익명객체를 통해 b와 c객체를 비교한다.
		int isBig = comp.compare(b, c);
		
		if(isBig > 0) {
			System.out.println("b객체가 c객체보다 큽니다.");
		}
		else if(isBig == 0) {
			System.out.println("두 객체의 크기가 같습니다.");
		}
		else {
			System.out.println("b객체가 c객체보다 작습니다.");
		}
		
	}
	
	public static Comparator<Student> comp = new Comparator<Student>() {
		@Override
		public int compare(Student o1, Student o2) {
			return o1.classNumber - o2.classNumber;
		}
	};
}
 
class Student {
 
	int age;			// 나이
	int classNumber;	// 학급
	
	Student(int age, int classNumber) {
		this.age = age;
		this.classNumber = classNumber;
	}
	
}
```

- 익명 객체를 사용해서 classNumber를 비교했다. 
- 다른 이름의 익명 객체를 만들어 age를 비교할 수도 있다.

#### Comparable 익명객체 사용하지 않는 이유
Comparable은 자기자신과 매개변수객체가 비교하는 것이기 때문이다. **동일한 타입과의 비교가 불가능하다.**


## Comparable, Comparator 정렬관계
>Java에서의 정렬은 특별한 정의가 있지 않는 한 오름 차순이다.
**[두 수의 비교 결과에 따른 작동 방식]**
**음수**일 경우 : 두 원소의 위치를 **교환 안함**
**양수**일 경우 : 두 원소의 위치를 **교환 함**

### Comparable 에서 정렬
```java
java.util.Arrays;
 
public class Test {
	
	public static void main(String[] args) {
		
		MyInteger[] arr = new MyInteger[10];
		
		// 객체 배열 초기화 (랜덤 값으로) 
		for(int i = 0; i < 10; i++) {
			arr[i] = new MyInteger((int)(Math.random() * 100));
		}
 
		// 정렬 이전
		System.out.print("정렬 전 : ");
		for(int i = 0; i < 10; i++) {
			System.out.print(arr[i].value + " ");
		}
		System.out.println();
		
		Arrays.sort(arr);
        
		// 정렬 이후
		System.out.print("정렬 후 : ");
		for(int i = 0; i < 10; i++) {
			System.out.print(arr[i].value + " ");
		}
		System.out.println();
	}
	
}
 
class MyInteger implements Comparable<MyInteger> {
	int value;
	
	public MyInteger(int value) {
		this.value = value;
	}
	
	@Override
	public int compareTo(MyInteger o) {
		return this.value - o.value;
	}
	
}
```

만약 Comparable을 구현하지 않고 Arrays.sort를 사용한경우 아래와 같은 오류가 발생한다. 
![[Pasted image 20220423023657.png]]
Arrays.sort 안에서 정렬을 하면서 원소를 비교하려 하는데, 해당 클래스가 비교할 수 있는 기준이 정의되어있지 않아서 정렬 자체가 불가능한 것이다.

### Comparator 에서 정렬
```java
import java.util.Arrays;
import java.util.Comparator;
 
public class Test {
	public static void main(String[] args) {
		
		MyInteger[] arr = new MyInteger[10];
		
		// 객체 배열 초기화 (랜덤 값으로) 
		for(int i = 0; i < 10; i++) {
			arr[i] = new MyInteger((int)(Math.random() * 100));
		}
 
		// 정렬 이전
		System.out.print("정렬 전 : ");
		for(int i = 0; i < 10; i++) {
			System.out.print(arr[i].value + " ");
		}
		System.out.println();
		
		Arrays.sort(arr, comp);		// MyInteger에 대한 Comparator을 구현한 익명객체를 넘겨줌
        
		// 정렬 이후
		System.out.print("정렬 후 : ");
		for(int i = 0; i < 10; i++) {
			System.out.print(arr[i].value + " ");
		}
		System.out.println();
	}
 
	static Comparator<MyInteger> comp = new Comparator<MyInteger>() {
		
		@Override
		public int compare(MyInteger o1, MyInteger o2) {
			return o1.value - o2.value;
		}
	};
}
 
class MyInteger {
	int value;
	
	public MyInteger(int value) {
		this.value = value;
	}
}
```
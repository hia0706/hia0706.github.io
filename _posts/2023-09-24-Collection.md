---
layout: post
title: "[자료구조] Collection에 대해?"
date: 2023-09-24
categories: [Development, 자료구조]
tags: [자료구조, java]
---

<p>
  <img src='/assets/img/documents/collection.png'>
  <em>컬렉션 프레임워크 상속계층도</em>
</p>

### 컬렉션의 대표적인 인터페이스

- **리스트 (List)**
  - `인덱스 순서로 요소를 저장`한다. 중복된 데이터를 저장할 수 있다.
- **큐 (Queue)**
  - 데이터가 저장된 순서대로 출력되는 `선입선출 (FIFO: First In First Out)` 의 구조를 갖는 선형 자료구조이다.
  - 인터페이스는 존재하나, 직접 구현된 클래스는 존재하지 않는다.
- **집합 (Set)**
  - `순서가 없으며, 데이터를 중복하여 저장할 수 없다.` 집합 연산 (**합집합, 교집합, 차집합** 등) 을 지원한다.
- **맵 (Map)**
  - `Key-value 쌍으로 데이터를 저장`한다. 순서가 존재하지 않으며, **Key(= 컬럼명,변수명) 가 중복될 수 없다.**

---

## ▶️ List

> 컬렉션 프레임워크의 주요 인터페이스 중 하나이다.

- List 인터페이스는 순서가 있는 데이터 집합이며, 데이터의 중복을 허용한다.

- 저장 공간의 크기가 고정되지 않고 **가변적**이며 중간에 **빈 공간을 허용하지 않는다.**

### List 대표 기능

**List 추가**

```java
list.add("값");
```

**List 삭제**

```java
list.remove("값");
list.remove(index);
```

**List 값 변경**

```java
list.set(index, "값");
```

**List 크기 확인**

```java
list.size();
```

**List 값 확인**

```java
// 특정 값 들어있는지 확인
list.contains("값");

// 비어있는지 확인
list.isEmpty();
```

|           | **저장 방식**                                                             | **크기 할당**                                        | **속도**                 |
|:---------:|:---------------------------------------------------------------------:|:------------------------------------------------:|:----------------------:|
| **Array** | **정해진 공간**이 있고,<br>그 모든 곳의**식별자(인덱스)가 존재**<br>ex) str[i]              | 객체생성시 **크기 할당 필수**<br>ex) char[] c = new char[3] | 삽입/삭제: 느림<br>데이터조회: 빠름 |
| **List**  | **식별자(인덱스)가 없음**,<br>앞의 요소가 삭제되면<br>새로 추가되는 요소가<br>**그 공간에 저장**될 수 있음 | **크기 할당 필요X**<br>(자바에선 자동으로<br>1.5배씩 늘어남)        | 삽입/삭제: 빠름<br>데이터조회: 느림 |

### 1️⃣ ArrayList

> **ArrayList**는 List 인터페이스를 구현한 클래스로, 컬렉션 프레임워크에서 가장 많이 사용되는 컬렉션 클래스이다.

- 메모리가 재할당되어 **Array에 비해 속도가 느리다**는 단점이 있다.

- 데이터의 순차적으로 저장하며, **데이터의 중복을 허용**한다.

- 설정한 저장 용량 크기가 넘어서 더 많은 객체가 들어오게 되면 배열 크기를 **1.5**배로 증가 시킨다.
  
  ```java
  public class ArrayList {
      public static void main(String[] args) {
          List<String> animals = new ArrayList<String>();
  
          animals.add("dog");
          animals.add("cat");
          animals.add("pig");
          animals.add("cow");
  
          int size = animals.size();
  
          for (int i = 0; i < size; i++) {
              String str = animals.get(i);
              System.out.println(i + " : " + str);
          }
      }
  }
  ```

---

### 2️⃣ LinkedList

> 불연속적으로 저장된 데이터를 서로 연결한 형태로 구성된 자료구조이자 컬렉션이다.

- 배열의 단점인 크기를 변경할 수 없고 비순차적인 데이터를 삽입/제거 하는데 시간이 많이 걸리는 점을 보완하기 위해 고안되었다.

- 데이터를 **추가, 삭제, 변경**하기 위해 사용한다.

---

### 3️⃣ Vector

> ArrayList와 동일한 내부구조를 가지고 있다. 값이 추가되면 자동으로 크기가 조절되며 그 다음 객체들은 한 자리씩 뒤로 이동한다.

ArrayList와 다른점은 동기화된 메소드로 구성되어 있기 때문에 멀티스레드가 동시에 이 메소드들을 실행할 수 없고, 하나의 스레드가 실행을 완료해야만 다른 스레드들이 실행할 수 있다.

💡 그래서 멀티 스레드 환경에서 `안전하게 객체를 추가하고 삭제`할 수 있다.

💡 하지만 스레드가 1개일 때도 동기화를 하기 때문에 ArrayList보다 성능이 떨어진다는 단점이 있다.

---

### 4️⃣ Stack

> 데이터를 순서대로 쌓는 자료구조이다.

- `LIFO(Last In First Out)` 즉, 후입선출 방식

- 단방향 입출력 구조 : 데이터의 들어오는 방향과 나가는 방향이 같다.

- 데이터를 하나씩만 넣고 뺄 수 있다.

- 깊이 우선 탐색(DFS)에 이용된다.

- 재귀 함수의 동작 흐름과 같은 구조를 가진다.

---

### 5️⃣ Iterator

> 인터페이스이며 컬렉션에 저장된 요소를 읽어오는 방법

- 각 요소에 접근하는 기능을 가졌다.

- Iterator를 반환하는 Iterator() 메소드가 정의되어 있다.

```java
Iterator<String> iterator = animals.iterator();

    while(iterator.hasNext()) {
        String str = iterator.next();
        if (str.equals("cat")) {
            iterator.remove();
        }
    }
    System.out.println(animals.subList(0, 2)); // 0부터 2인덱스 까지 값 출력
    // 출력: [dog, pig, cow]
```

---

## Queue

> 자료구조의 일종으로 리스트의 자료나 나열되는 자료, 순환되는 자료, 대기열 등에 사용된다.

- `FIFO(First In First Out)` 선입선출 방식

- 큐의 `앞 부분은 삭제 연산`만 수행하고, `뒷 부분은 삽입 연산`만 수행한다.

- `Index의 개념이 없어서` 어떠한 값이 몇 번째에 있는지는 알 수 없다.

- 컴퓨터 버퍼에서 주로 사용되고, 여러 데이터가 한번에 입력이 들어올 때 대기열을 만들어 순차적으로 처리할 때 사용된다. 

---

## Set

> Set 인터페이스를 구현하는 대표적인 클래스에는 HashSet, TreeSet이 있다.

- 저장 순서를 유지하지 않고, 중복을 허용하지 않는다.

### 1️⃣ HashSet

> Set 인터페이스를 구현한 가장 대표적인 컬렉션이다.

- 추가할 때 add 메소드나 addAll 메소드를 사용한다.

```java
public class HashSetDemo {
    public static void main(String[] args) {
        HashSet<String> drink = new HashSet<String>();

        drink.add("cola");
        drink.add("cola");
        drink.add("cider");
        drink.add("smoothie");
        drink.add("tea");

        Iterator it = drink.iterator();

        while(it.hasNext()){
            System.out.println(it.next());
       }
    }
    // 출력
    // smoothie
    // tea
    // cola
    // cider
}
```

💡 중복 입력한 cola는 한 번만 출력되고, 출력 순서가 입력 순서와 다르다는 것을 확인할 수 있다. 저장 순서대로 출력하고 싶다면 LinkedList를 사용해야 한다.

### 2️⃣ TreeSet

<p>
  <img src='/assets/img/documents/treeset.png'>
  <em>이진 검색 트리</em>
</p>

> 이진 검색 트리(binary search tree) 형태로 데이터를 저장하는 컬렉션 클래스

        💡 이진 검색 트리 - 여러 노드가 서로 연결된 구조

- Set의 특징인 중복 저장이 되지 않고, 순서 유지가 안되는 것을 가지고 있다.

- `정렬과 검색(범위검색)`에 특화되어 있다.

- 비순차적으로 저장하기 때문에 `추가 및 삭제에 시간이 걸린다.`

한 노드에는 노드를 연결할 수 있다. 트리는 root 라는 하나의 노드로부터 시작해 계속 확장할 수 있다. 한 노드와 노드로부터 확장된 두 노드는 서로 부모-자식 관계에 있는데, 부모로부터 오른쪽으로 확장된 자식 노드는 반드시 부모 노드의 값보다 커야 한다. 
`단, 왼쪽으로 확장된 자식 노드는 반드시 부모 노드의 값보다 작아야 한다.`

---

## Map

> Map 인터페이스는 키(Key)와 값(Value)로 구성된 Entry 객체를 저장하는 구조를 가지고 있다.

키와 값이라는 두 데이터를 연결하는 것이 매핑이다. 또한, 해싱을 사용하기 때문에 방대한 양의 데이터를 검색하는데 있어서 뛰어난 성능을 보인다. 

### ▶️ HashMap

> Map 인터페이스를 구현하는 대표적인 인터페이스

- 같은 키의 값을 삽입하려고 하면 해당 키의 값이 변경된다.

- 키는 중복이 되지 않지만 값은 중복 될 수 있다.

- Null 값도 저장이 가능하다.

---

### 선언

- Key, Value 2개의 값을 가지고 있으므로 타입을 선언하려면 두 개의 타입을 선언해야한다.

- `HashMap<타입, 타입> 변수명 = new HashMap<타입, 타입>();` 로 선언한다.

- 나머지 사용법은 예제 참고 🔽

```java
public class HashmapDemo {
    public static void main(String[] args) {
        HashMap map = new HashMap();
        HashMap<Integer, Integer> m1 = new HashMap<>(); // Integer 타입 설정
        HashMap<Integer, Integer> m2 = new HashMap<>(m1); // m1 값 복사
        HashMap<Integer, Integer> m3 = new HashMap<>(10); // 초기 용량 지정
        HashMap<Integer, Integer> m4 = new HashMap<>() { // 변수 선언 및 초기값 지정
            {
                put(1, 100);
                put(2, 200);
            }
        };

        HashMap<String, String> str = new HashMap<String, String>(); // String 타입 설정
        HashMap<Character, Character> ch = new HashMap<Character, Character>(); // Char 타입 설정
    }
}
```

 💡 `java7`부터 다이아몬드 연산자를 사용하여 타입 추론을 할 수 있게되서 첫 번째 코드를 선호한다.

```java
HashMap<String, String> map = new HashMap<>(); 
HashMap<String, String> map = new HashMap<String, String>();
```

---

### 추가

- `put(Key, Value)` 으로 값을 추가한다.

- 들어가는 타입은 변수를 선언할 당시의 타입으로 맞춰서 입력해줘야한다.

- 같은 **Key**의 데이터를 추가하면 나중에 넣은 **Value**로 변경된다.

```java
public class HashmapPutDemo {
    public static void main(String[] args) {
        HashMap<String, String> map = new HashMap<>();

        // 값 추가
        map.put("1", "Hello");
        map.put("2", "World");
        map.put("3", "Hello2");
        map.put("4", "World2");
        map.put("2", "WorldWorld2");

        System.out.println(map);
    }
}
```

🔽 결과

```textile
{1=Hello, 2=WorldWorld2, 3=Hello2, 4=World2}
```

---

### 삭제

- `remove(Key)` 메소드를 사용하여 값을 삭제한다.

- `clear()` 메소드를 사용하면 **HashMap의 모든 Key 값**을 삭제한다.

```java
public class HashMapDemo {
    public static void main(String[] args) {
        HashMap<String, String> map = new HashMap<>();

        // 값 추가
        map.put("1", "Hello1");
        map.put("2", "Goodbye2");
        map.put("3", "Hello3");
        map.put("4", "Goodbye4");

        System.out.println(map);

        map.remove("3");
        System.out.println(map);

        map.clear();
        System.out.println(map);
    }
}
```

🔽 결과

```textile
{1=Hello1, 2=Goodbye2, 3=Hello3, 4=Goodbye4}
{1=Hello1, 2=Goodbye2, 4=Goodbye4}
{}
```

---

### 크기 구하기

- `size()` 메소드를 사용한다.

```java
public class HashMapDemo {
    public static void main(String[] args) {
        HashMap<String, String> map = new HashMap<>();

        // 값 추가
        map.put("1", "Hello1");
        map.put("2", "Goodbye2");
        map.put("3", "Hello3");
        map.put("4", "Goodbye4");

        System.out.println(map);
        System.out.println("크기 -> " + map.size());

    }
}
```

🔽 결과

```textile
{1=Hello1, 2=Goodbye2, 3=Hello3, 4=Goodbye4}
크기 -> 4
```

---

### 출력하기

```java
System.out.println(map);
```

결과 🔽

```textile
{1=Hello1, 2=Goodbye2, 3=Hello3, 4=Goodbye4}
```

위 방법으로 출력하면 아래의 값을 얻을 수 있지만 HashMap은 순서를 보장하기 않기 때문에 출력된 순서가 아래와 같을 것이라는 보장은 없기 때문에 향상된 for문을 사용해야 한다.

🔽 향상된 for 문

```java
public class HashMapDemo {
    public static void main(String[] args) {
        HashMap<String, String> map = new HashMap<>();

        // 값 추가
        map.put("1", "Hello1");
        map.put("2", "Goodbye2");
        map.put("3", "Hello3");
        map.put("4", "Goodbye4");

        for (Map.Entry<String, String> m : map.entrySet()) {
            System.out.println("Key : " + m.getKey() + "Value : " + m.getValue());
        }
    }
}
```

🔽 출력

```textile
Key: 1, Value: Hello1
Key: 2, Value: Goodbye2
Key: 3, Value: Hello3
Key: 4, Value: Goodbye4
```
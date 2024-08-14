## 문자열
### Scanner
```java
Scanner scanner = new Scanner(System.in);
String str1 = scanner.next();
String str2 = scanner.nextLine();
double v = scanner.nextDouble();
int i = scanner.nextInt();
```
콘솔 입력값으로 들어온 값을 사용하는 클래스입니다.  
next는 공백이 나올 때까지 읽고, nextLine은 Enter가 나올때까지 읽습니다.

### charAt
```java
String str = "Hello World";
char c = str.charAt(0);
System.out.print(c); // H

String str = "0";
int num = str.charAt(0); // 48
int num = str.charAt(0) - '0'; // 0 
```
String 타입의 데이터(문자열)에서 특정 문자를 char 타입으로 변환할 때 사용하는 함수입니다.  
해당 Char을 int로 형변환하면 아스키코드값이 나오는데 숫자로 변환하고 싶다면 문자 0을 빼주면 됩니다.  

### char 형변환
```java
int num = '1'-'0' // 1
int num = Character.getNumericValue('1') // 1
```

### 대소문자
```java
String str = "hello world"
str = str.toUpperCase(); // 문자열을 대문자로 변환
str = str.toLowerCase(); // 문자열을 소문자로 변환

Char c = "c"
c = Character.toUpperCase(c); // 문자를 대문자로 변환
c = Character.toLowerCase(c); // 문자를 소문자로 변환

Char c = "c"
c = Character.toUpperCase(c); // 문자를 대문자로 변환
c = Character.toLowerCase(c); // 문자를 소문자로 변환

// 대소문자 여부 확인
char c = 'c';
Character.isLowerCase(c); // true
Character.isUpperCase(c); // false

// 문자열을 비교할 때 대소문자를 무시하고 비교할 수도 있다.
left.equalsIgnoreCase(right)
```

### toCharArray
문자열을 쪼개서 Char 배열로 만들어주는 함수입니다.
```java
String str = "hello world";
char[] chars = str.toCharArray(); // char 배열
String s = new String(chars); // "hello world"
String s1 = String.valueOf(chars) // "hello world"
```
<br>

### 알파벳인지 확인 - Character.isAlphabetic
```java
String str = "hello world";
char[] chars = str.toCharArray(); // char 배열
for (char c : chars) {
    System.out.println(Character.isAlphabetic(c));
}
```


### Split
문자열을 잘라서 배열로 만들어주는 함수입니다.
```java
// 공백 분리
String answer="Hello World";
String[] s = answer.split(" "); // ["Hello","World"]

// 쉼표 분리
answer="Hello,World";
String[] split = answer.split(","); // ["Hello","World"]

// 공백과 쉼표 분리 | 사용
answer="Hello,W orld";
String[] split1 = answer.split(" |,"); // ["Hello","W","orld"]

// limit 0 = 그냥 split과 일치
// 빈문자열은 제거됨
answer="h:e:l:l:o:";
String[] split2 = answer.split(":", 0);// ["h","e","l","l","o"]

// limit 2 => 2개의 배열로 쪼갬
String[] split3 = answer.split(":", 2); // ["h","e:l:l:o:"]

// limit을 더 크게 잡을 경우, 빈문자열을 제거되지 않음
String[] split4 = answer.split(":", 10); // ["h","e","l","l","o",""]

// limit을 크게 잡을 때랑 같음
String[] split5 = answer.split(":", -1); // ["h","e","l","l","o",""]

// 메타 문자를 사용할 경우
// ? * + ( ) [ ] { } 이스케이프 \\ 처리
answer = "hello{world";
String[] split6 = answer.split("\\{"); // ["hello","world"]
```

### indexOf
특정 문자나 문자열이 앞에서부터 처음 발견되는 인덱스를 반환하며 찾지 못했을 경우 -1을 반환하는 함수입니다.
```java
String answer="Hello World";
answer.indexOf("e"); // 1
answer.indexOf("Hello"); // 0
answer.indexOf("back"); // -1

// 2번 인덱스부터 뒤로가면서 찾기
answer.indexOf("e", 2);// -1 

// 배열의 경우 indexOf를 지원하지 않고 ArrayList 자료구조에서만 지원하므로
// list로 변환시키고 찾는다.
String[] arr = {"a","b","c"};
System.out.println(Arrays.asList(arr).indexOf("b")); //1이 출력된다.
```

### lastIndexOf
특정 문자나 문자열이 뒤에서부터 처음 발견되는 인덱스를 반환하며 만약 찾지 못했을 경우 "-1"을 반환합니다.
```java
String answer="Hello World";
answer.lastIndexOf("l");// 9
answer.lastIndexOf("Hello");// 0  
answer.lastIndexOf("back");// -1

// 두번째 인자는 시작 인덱스
String answer="Hello World";
answer.lastIndexOf("l", 9);// 9 -> 9번 인덱스부터 0번 인덱스로 가면서 찾기
answer.lastIndexOf("l", 8);// 9 -> 8번 인덱스부터 0번 인덱스로 가면서 찾기
```

### SubString
문자열을 자르는 함수입니다.
```java
public String substring(int beginIndex)
public String substring(int beginIndex, int endIndex)

String str = "hello world";
str.substring(5); // (공백)world
str.substring(6, 11); // world
str.substring(6, 100); // out of index

// is beautiful 만 뽑아내기
String str = "This island is beautiful";
int beginIndex = str.lastIndexOf("is");
int endIndex = str.length();
String result = str.substring(beginIndex, endIndex);
```

### StringBuilder
문자열을 이어붙이거나 거꾸로 출력하기 위해서 사용하는 함수입니다.
```java
StringBuilder sb = new StringBuilder();
sb.append("hello");
sb.append(" world");
String s = sb.toString(); // hello world

// 역순 출력 reverse
String str = "hello world";
StringBuilder sb = new StringBuilder(str);
String s = sb.reverse().toString(); // dlrow olleh

// StringBuilder의 인자로 숫자를 주면 크기로 인지하므로 String값을 줘야한다.
String s = new StringBuilder(String.valueOf(32)).reverse().toString();
System.out.println("s = " + s); // 23

// StringBuilder의 인자로 String과 Char이 오지만 이후 append에는 다른 타입도 넣을 수 있다.
// chars는 String을 char로 쪼개서 해당 char의 정수값 IntStream을 반환한다.  
// Character의 getNumbericValue 메서드는 숫자형 문자 char 또는 숫자형 문자의 정수값을 주면 숫자로 바꿔준다. (ex '1' -> 1)  
class Solution {
    public int[] solution(long n) {
        return new StringBuilder().append(n).reverse().chars().map(Character::getNumericValue).toArray();
    }
}
```



### replcae, replaceAll
문자열에서 특정 문자를 변환시켜주는 함수입니다.  
replace와 replaceAll을 같은 역할을 하는데 replaceAll은 정규식을 사용할 수 있습니다.  
```java
String str = "hello world";
// 타겟 대상, 변환 문자
String replace = str.replace("l", " ");
System.out.println("replace = " + replace); // replace = he  o wor d

String str = "h,e,ll, world";
String s = str.replaceAll("[^a-zA-Z]", "");
System.out.println("s = " + s); // s = hellworld

// \\ 두번 사용해야 한다.
str.replaceAll("[^\\d]", ""); // 숫자가 아닌것 교체
```
java에서 정규식으로 \를 사용하기 위해서는 \\\\ 로 사용해야 한다.

### 진수 변환
```java
String str = "010101010101";
int decimal = Integer.parseInt(str, 2); // 문자, 진수 -> 10진수 변환
System.out.println("decimal = " + decimal); // 1365

int i = 127;
 
String binaryString = Integer.toBinaryString(i); //2진수로 변환
String octalString = Integer.toOctalString(i);   //8진수로 변환
String hexString = Integer.toHexString(i);       //16진수로 변환
 
System.out.println(binaryString); //1111111
System.out.println(octalString);  //177
System.out.println(hexString);    //7f
 
 
int binaryToDecimal = Integer.parseInt(binaryString, 2); // 2진수 10진수로 복원
int binaryToOctal = Integer.parseInt(octalString, 8); // 8진수 10진수로 복원
int binaryToHex = Integer.parseInt(hexString, 16); // 16진수 10진수로 복원
 
System.out.println(binaryToDecimal); //127
System.out.println(binaryToOctal);   //127
System.out.println(binaryToHex);     //127
```

### 아스키코드 변환
```java
int a = 65;
char a1 = (char) a;
System.out.println(a1); // A
int a11 = a1;
System.out.println(a11); // 65
```

<Br>

## 배열
---

### 채우기
```java
int[] arr = new int[10];
Arrays.fill(arr,Integer.MAX_VALUE);
```
int로 해두면 전부 0으로 세팅되는데 이를 원하는 값으로 세팅해줄 수 있습니다.  

### 정렬
```java
int[] ints = new int[3];
ints[0]=6;
ints[1]=3;
Arrays.sort(ints);
for (int anInt : ints) {
    System.out.println(anInt);
}

//  출력
0
3
6
```
Arrays.sort 를 사용해서 일반 배열을 정렬시킬 수 있습니다.  

### clone
```java
int[] ints = new int[3];
ints[0]=1;
ints[1]=2;
ints[2]=3;
int[] clone = ints.clone();
for (int i : clone) {
    System.out.println("i = " + i);
}
```
깊은 복사로 값은 같지만 서로 다른 참조값을 가리키도록 복사합니다.

### contains
```java
// Arrays 사용
// equals를 사용해야하기 때문에 박싱 객체를 사용해야 합니다.
Integer[] leftSide = {1,4,7};
Arrays.asList(leftSide).contains(1);       

// Stream 사용
String[] arr = new String[]{"1", "2", "3"};
String stringToSearch = "2";
System.out.println(Arrays.stream(arr).anyMatch(s -> s.equals(stringToSearch)));

// equals를 사용하지 않는다면 박싱타입을 사용하지 않아도 됩니다.
int[] a = {1,2,3,4};
boolean contains = IntStream.of(a).anyMatch(x -> x == 4);
```

### sum
```java
int[] a = {1,2,3,4};
int sum = Arrays.stream(a).sum();

List<Integer> arr = new ArrayList<>();
arr.add(1);
arr.add(2);
arr.add(3);
int sum2 = arr.stream().mapToInt(Integer::intValue).sum();
```

### 자르기
```java
int[] arr = {1,2,3,4,5,6,7,8};
// 인자 순서(배열, 시작, 끝점(포함X))
int[] copyArr = Arrays.copyOfRange(arr, 1, 3);
for (int unit : copyArr) {
    System.out.println(unit); // 2, 3
}
```

### count
```java
public class Test {
    public static void main(String[] args) {
        int[] arr = {1,1,1,1,1,1,2,3,4,5,6};
        long count = Arrays.stream(arr).filter(a -> a == 1).count();
        System.out.println(count);
    }
}
```

### min, max
```java
public int solution(int[][] sizes) {

    // 2차원 배열에서 max 구하기
    int x = Arrays.stream(sizes).flatMapToInt(size -> Arrays.stream(size)).max().getAsInt();
    
    for (int[] size : sizes) {
        // 1차원 배열에서 min 구하기
        Arrays.stream(size).min().getAsInt();
    }
}

// 리스트에서 최대 최소 찾기
ArrayList<Integer> list = new ArrayList<>(Arrays.asList(0, 3, 2, 1, 5));

// Max
int max = Collections.max(list);
int min = Collections.min(list);
```

### 특정 값 인덱스 찾기
```java
String[] arr = {"a","b","c"};
System.out.println(Arrays.asList(arr).indexOf("b")); //1이 출력된다.
```
자바 배열에서는 indexOf를 지원하지 않고 List 자료구조에서 지원하므로 asList로 변환하고 사용해야 합니다.

### 리스트 배열로 바꾸기
```java
List<String> list = new ArrayList<>();
list.add("a");
list.add("b");
list.add("c");

String[] result = list.stream().toArray(String[]::new);
String[] result = list.toArray(new String[0]); // 파라미터를 0으로 주면 List에 길이에 맞게 알아서 조정된다.
```


<br>

## 해쉬
### Map
#### getOrDefault
map에서 key값으로 value를 꺼내올 때, 만약 map안에 key값으로 저장된 것이 없다면 default값으로 정해줄 수 있는 함수입니다.  
```java
HashMap<Character, Integer> map = new HashMap<>();
String str = "helloworld";
for(char c : str.toCharArray()){
    map.put(c,map.getOrDefault(c,0)); // 없으면 default값으로 0을 반환하라
}
```

#### containsKey
map 안에 해당 key값이 존재하는지 확인하는 함수입니다.  
```java
HashMap<Character, Integer> map = new HashMap<>();
map.put('A',23);
map.containsKey('A'); // true
```

#### size
map에서 key의 개수를 알려줍니다.
```java
HashMap<Character, Integer> map = new HashMap<>();
map.put('A',23);
map.size();  // 1
```

#### remove
map에서 key값을 갖는 key-value 쌍을 제거합니다.
```java
HashMap<Character, Integer> map = new HashMap<>();
map.put('A',23);
System.out.println(map.size()); // 1
Integer a = map.remove('A'); // value값 23을 반환
System.out.println(a); // 23
System.out.println(map.size()); // 제거되었으므로 0
```

#### equals
map에서 equals를 하면 key와 value값이 모두 같은지 비교합니다.
```java
HashMap<Character, Integer> map1 = new HashMap<>();
map1.put('A',23);
HashMap<Character, Integer> map2 = new HashMap<>();
map2.put('A',23);
System.out.println(map1.equals(map2)); // true
```

#### Max 구하기
```java
Collections.max(counterMap.entrySet(),Map.Entry.comparingByValue()).getKey()
```
컬렉션 관련해서 기능이 필요하면 Collections 클래스를 찾아보도록 합니다.  
map에서 entryset을 뽑아서 value를 기준으로 max인 entryset를 뽑고 거기서 key를 가져오는 코드입니다.

### ConcurrentHashMap
ConcurrentHashMap은 쓰기 작업에 동기화가 되어 있는 HashMap인데 거의 모든 면에서 HashMap보다 성능이 좋습니다.  
ConcurrentHashMap은 HashMap과 다르게 key, value에 null을 허용하지 않습니다.  




### TreeSet
Set은 집합 자료구조이고, TreeSet은 정렬된 집합 자료구조입니다.  
#### add
추가하는 API입니다.
```java
TreeSet<Integer> tSet = new TreeSet<>();
tSet.add(1);
tSet.add(1);
tSet.add(2);
tSet.add(3);
for (Integer integer : tSet) {
    System.out.println(integer);
}
// 출력
1
2
3
```

#### 역순
기본적으로 오름차순으로 정렬되는데 Collections.reverseOrder()를 사용하면 내림차순으로 변경할 수 있습니다. 
```java
TreeSet<Integer> tSet = new TreeSet<>(Collections.reverseOrder());
tSet.add(1);
tSet.add(1);
tSet.add(2);
tSet.add(3);
for (Integer integer : tSet) {
    System.out.println(integer);
}
// 출력
3
2
1
```

#### remove
요소를 제거합니다.
```java
 TreeSet<Integer> tSet = new TreeSet<>(Collections.reverseOrder());
tSet.add(1);
tSet.add(2);
tSet.remove(1);
for (Integer integer : tSet) {
    System.out.println(integer);
}

// 출력 
2
```

#### size
사이즈 크기를 알려줍니다.
```java
TreeSet<Integer> tSet = new TreeSet<>(Collections.reverseOrder());
tSet.add(1);
tSet.add(2);
System.out.println(tSet.size()); // 2
```

#### first, last
+ first
    - 오름차순 : 가장 작은 값
    - 내림차순 : 가장 큰 값
+ last
    - 오름차순 : 가장 큰 값
    - 내림차순 : 가장 작은 값

정렬 기준으로 가장 작은 혹은 가장 큰 것 꺼내는 API입니다.
```java
// 오름차순
TreeSet<Integer> tSet = new TreeSet<>();
tSet.add(1);
tSet.add(2);
tSet.add(3);
System.out.println(tSet.first()); // 1
System.out.println(tSet.last()); // 3

// 내림차순
TreeSet<Integer> tSet = new TreeSet<>(Collections.reverseOrder());
tSet.add(1);
tSet.add(2);
tSet.add(3);
System.out.println(tSet.first()); // 3
System.out.println(tSet.last()); // 1
```
<Br>

## Stack
---
Stack 클래스는 List 컬렉션 클래스의 Vector 클래스를 상속받아, 전형적인 스택 메모리 구조의 클래스를 제공합니다.  
스택 메모리 구조는 선형 메모리 공간에 데이터를 저장하면서 후입선출(LIFO)의 시멘틱을 따르는 자료 구조입니다.  

### push
stack에 값을 넣습니다.
```java
Stack<Integer> stack = new Stack<>();
stack.push(1);
```

### pop
가장 마지막에 push된 값을 꺼내고 스택에서 해당 값을 지웁니다.
```java
Stack<Integer> stack = new Stack<>();
stack.push(1);
stack.push(2);
stack.push(3);
System.out.println(stack.pop()); // 3
System.out.println(stack.pop()); // 2
```

### peek
가장 마지막에 push된 값을 꺼내고 스택에서는 지우지 않습니다.
```java
Stack<Integer> stack = new Stack<>();
stack.push(1);
stack.push(2);
stack.push(3);
System.out.println(stack.peek()); // 3
System.out.println(stack.peek()); // 3
```

### size
스택에 들어있는 값의 개수를 확인합니다.
```java
Stack<Integer> stack = new Stack<>();
stack.push(1);
stack.push(2);
stack.push(3);
System.out.println(stack.size()); // 3
```

### empty
스택이 비어있는지 확인합니다.
```java
Stack<Integer> stack = new Stack<>();
stack.push(1);
stack.push(2);
stack.push(3);
System.out.println(stack.isEmpty()); // false
```

### search
가장 앞에서부터 존재하는 인덱스 반환하지만 인덱스가 0이 아니라 1부터 취급함을 주의해야 합니다.
```java
Stack<Integer> stack = new Stack<>();
stack.push(4);
stack.push(5);
stack.push(6);
System.out.println(stack.search(5)); // 2
```

<br>

## Queue
---
클래스로 구현된 스택과는 달리 자바에서 큐 메모리 구조는 별도의 인터페이스 형태로 제공됩니다.  
큐 메모리 구조는 선형 메모리 공간에 데이터를 저장하면서 선입선출(FIFO)의 시멘틱을 따르는 자료 구조입니다.  
Queue 인터페이스를 상속받는 하위 인터페이스는 다음과 같습니다.  
+ Deque\<E>
+ BlockingDeque\<E>
+ BlockingQueue\<E>
+ TransferQueue\<E>

이 중에서도 Deque 인터페이스를 구현한 LinkedList 클래스가 큐 메모리 구조를 구현하는데 가장 많이 사용됩니다.  
Deque는 앞, 뒤에서 모두 접근이 가능합니다.

### Dequeue
#### add
```java
Deque<Integer> q = new LinkedList<>();
q.add(1); // 뒤에 삽입
q.add(2);
q.add(3);
q.addLast(5); // 뒤에 삽입 add랑 같음
q.addFirst(4); // 맨 앞에 삽입
for (Integer integer : q) {
    System.out.println("integer = " + integer);
}
// 출력
integer = 4
integer = 1
integer = 2
integer = 3
integer = 5
```

#### poll, remove
pop과 비슷합니다.  
remove는 poolFirst와 같은 기능을 합니다.  
비어있다면 null을 반환합니다.
```java
Deque<Integer> q = new LinkedList<>();
q.add(1); 
q.add(2);
q.add(3);

// 맨앞에 요소 가져오고 큐에서 제거
q.pollFirst(); // 1
// 맨 뒤 요소 가져오고 큐에서 제거
q.pollLast(); // 3
```

#### peek
요소를 꺼내기만 하는 함수입니다.
비어있다면 null을 반환합니다.
```java
Deque<Integer> q = new LinkedList<>();
q.add(1); // 뒤에 삽입
q.add(2);
q.add(3);

// 맨 앞 요소 가져오기
q.peekFirst(); // 1
// 맨 뒤 요소 가져오기
q.peekLast(); // 3
```

#### Contains
포함하고 있는지를 부울 값으로 반환합니다.
```java
Deque<Integer> q = new LinkedList<>();
q.add(1);
q.add(2);
System.out.println(q.contains(1)); // true
```

### 우선순위 큐
```java
PriorityQueue<Student> pq = new PriorityQueue<>();
PriorityQueue<Student> pqReverse = new PriorityQueue<>(Collections.reverseOrder());
```
제공하는 api는 큐와 유사합니다.  
우선순위를 정할 때는 객체 안의 CompareTo를 사용하게 됩니다.  
기본적으로 오름차순으로 꺼내게 되고 reverseOrder를 이용해서 내림차순으로도 가능합니다.


<Br>

## 정렬
---
### 배열 정렬
```java
// 오름차순
int arr[] = {4,23,33,15,17,19};
Arrays.sort(arr);

// 내림차순
// int가 아닌 Integer를 사용해야 합니다.
Integer arr[] = {4,23,33,15,17,19};
Arrays.sort(arr,Collections.reverseOrder());
```
String 정렬도 위와 동일합니다.  

### 배열 부분 정렬
```java
int[] arr = {1, 26, 17, 25, 99, 44, 303};

Arrays.sort(arr, 0, 4);
```
0부터 4개 즉, 3번 인덱스까지 포함해서 정렬합니다.

### 문자열 길이 정렬
문자열 길이로 정렬하고 싶다면 직접 Comparator를 구현해야 합니다.
```java
String[] arr = {"Apple", "Kiwi", "Orange", "Banana", "Watermelon", "Cherry"};

Arrays.sort(arr, new Comparator<String>() {
    @Override
    public int compare(String s1, String s2) {
        return Integer.compare(s1.length(),s2.length());
    }
});

// 람다로 더 간단하게
Arrays.sort(arr, (s1, s2) -> Integer.compare(s1.length(), s2.length()));
```
__자바에서 구현하는 정렬 방식은 대부분 앞에 오는 것(자신) - 타겟을 뺀 값을 리턴해주면 오름차순 정렬이 됩니다.__  
오름차순으로 구현해두고 Collections.reverseOrder()를 사용하면 내림차순 정렬이 가능합니다.  
reverseOrder를 사용하기 싫다면 compare를 구현할 때 (타겟 - 자신)을 리턴해주면 됩니다.  
연산자를 쓰는 방식은 과거의 방식이고 최근에는 박싱타입의 compare 정적 메서드를 사용합니다.

### 객체 정렬
```java
public static class Fruit implements Comparable<Fruit> {
    private String name;
    private int price;
    public Fruit(String name, int price) {
        this.name = name;
        this.price = price;
    }

    @Override
    public int compareTo(@NotNull Fruit fruit) {
        return this.price - fruit.price;
    }
}

Fruit[] arr = {
        new Fruit("Apple", 100),
        new Fruit("Kiwi", 500),
        new Fruit("Orange", 200),
        new Fruit("Banana", 50),
        new Fruit("Watermelon", 880),
        new Fruit("Cherry", 10)
};

Arrays.sort(arr); // 내림차순
Arrays.sort(arr,Collections.reverseOrder()); // 오름차순
```

### 컬렉션 정렬
```java
ArrayList<Integer> arr = new ArrayList<>();
arr.add(3);
arr.add(2);
arr.add(1);
// 오름차순 정렬
Collections.sort(arr);
for (Integer integer : arr) {
    System.out.println(integer); 
}

// 출력
// 1
// 2
// 3

// 내림차순 정렬
Collections.sort(arr,Collections.reverseOrder());
```
컬렉션 정렬에서는 Collection.sort를 사용합니다.

### Comparator 정적 메서드 정렬
```java
String[] arr = {"Apple", "Kiwi", "Orange", "Banana", "Watermelon", "Cherry"};

Arrays.sort(arr,Comparator.comparing((String str) -> str));

ArrayList<Student> students = new ArrayList<>();
students.add(new Student(1,"name",1));
students.add(new Student(2,"name2",2));
students.add(new Student(3,"name3",3));

Collections.sort(students,Comparator.comparing((Student st) -> st.getName())
        .thenComparingInt(st -> st.getGrade())
        .thenComparingInt(st -> st.getAge()).reversed())                
        ;
```
Comparator 정적 메서드로 제공되는 정렬 방식을 사용할 수 있습니다.  
comparing은 문자열을 비교할 때 사용되고 comparingInt는 정수 비교 시 사용됩니다.  
reversed를 이용하면 내림차순이 가능합니다.  
첫 번째 비교 대상은 객체 타입을 반드시 명시해줘야 하고 이후에는 컴파일러가 알아서 인식하기 때문에 타입을 명시하지 않아도 됩니다.  

### 이진 탐색
```java
int[] arr = new int[5];
arr[0]=1;
arr[1]=2;
arr[2]=3;
arr[3]=3;
arr[4]=5;
int i = Arrays.binarySearch(arr, 3);
System.out.println(i); // 2
i = Arrays.binarySearch(arr, 0);
System.out.println(i); // -1
i = Arrays.binarySearch(arr, 4);
System.out.println(i); // -5
```
이진 탐색을 하기 위해서는 해당 배열이 정렬되어 있어야 합니다.  
Arrays.binarySearch는 두 번째 인자를 첫 번째 인자(배열)에서 찾아서 인덱스를 반환합니다.  
만약 존재하지 않을 경우 음수로 어디에 들어가야 하는지 인덱스를 반환합니다.  
0을 인자로 주었을 때 출력값이 -1인데 그 의미는 배열의 첫 번째에 들어가야 한다는 의미입니다.  
즉, 1번째 -> 인덱스 0을 의미합니다.  
4를 인자로 주었을 때 출력값이 -5인데 배열의 5번째 -> 4번 인덱스에 들어가야 한다는 의미입니다.  

<br>


> 중복, 조합 코드는 코틀린입니다. 

## 순열
---
```kotlin
fun <T> permutation(arr: List<T>, r: Int): List<List<T>> {
  if (arr.size < r) {
    return emptyList()
  }

  val result = mutableListOf<List<T>>()
  fun permute(currentPermutation: List<T>, remainingElements: List<T>) {
    if (currentPermutation.size == r) {
      result.add(currentPermutation)
      return
    }
    for (i in remainingElements.indices) {
      permute(currentPermutation + remainingElements[i], remainingElements - remainingElements[i])
    }
  }
  permute(listOf(), arr)
  return result
}

```
<br>

## 중복 순열
---
```kotlin
fun <T> permutationWithRepetition(arr: List<T>, r: Int): List<List<T>> {
  val result = mutableListOf<List<T>>()
  fun permute(currentPermutation: List<T>) {
    if (currentPermutation.size == r) {
      result.add(currentPermutation)
      return
    }
    for (i in arr.indices) {
      permute(currentPermutation + arr[i])
    }
  }
  permute(listOf())
  return result
}
```

## 조합
---
```kotlin
fun <T> combination(arr: List<T>, r: Int): List<List<T>> {
  if (arr.size < r) {
    return emptyList()
  }

  val result = mutableListOf<List<T>>()

  fun combine(start: Int, current: List<T>) {
    if (current.size == r) {
      result.add(current)
      return
    }

    for (i in start..current.lastIndex) {
      combine(i + 1, current + arr[i])
    }
  }
  combine(0, listOf())
  return result
}
```

<br>

## 중복 조합
---
```kotlin
fun <T> combinationWithRepetition(arr: List<T>, r: Int): List<List<T>> {
  val result = mutableListOf<List<T>>()
  fun combine(start: Int, currentCombination: List<T>) {
    if (currentCombination.size == r) {
      result.add(currentCombination)
      return
    }
    for (i in start until arr.size) {
      combine(i, currentCombination + arr[i])
    }
  }
  combine(0, listOf())
  return result
}
```

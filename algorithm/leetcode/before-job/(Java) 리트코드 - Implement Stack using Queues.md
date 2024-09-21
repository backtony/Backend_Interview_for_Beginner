[문제 링크](https://leetcode.com/problems/implement-stack-using-queues/)


## Java 풀이 1
```java
import java.util.LinkedList;
import java.util.Queue;

class MyStack {

    Queue<Integer> q;

    public MyStack() {
        q = new LinkedList<>();
    }

    public void push(int x) {
        q.add(x);
        int length = q.size();
        for (int i = 0; i <length-1;i++){
            q.add(q.remove());
        }
    }

    public int pop() {
        return q.poll();
    }

    public int top() {
        return q.peek();
    }

    public boolean empty() {
        return q.isEmpty();
    }
}
```
큐 1개를 이용한 삽입 O(n), 삭제 O(1) 복잡도

## Java 풀이 2
```java
import java.util.LinkedList;
import java.util.Queue;

class MyStack {

    Queue<Integer> q1;
    Queue<Integer> q2;
    int top;

    public MyStack() {
        q1 = new LinkedList<>();
        q2 = new LinkedList<>();
    }

    public void push(int x) {
        q1.add(x);
        top = x;
    }

    public int pop() {
        while (q1.size()>1){
            top = q1.poll();
            q2.add(top);
        }
        Integer pop = q1.poll();
        Queue<Integer> temp = q1;
        q1 = q2;
        q2 = temp;        
        return pop;
    }

    public int top() {
        return top;
    }

    public boolean empty() {
        return q1.isEmpty();
    }
}
```
큐 2개를 이용한 삽입 O(1), 삭제 O(n) 복잡도

## kotlin 풀이
```kotlin
import java.util.LinkedList
import java.util.Queue

class MyStack() {

    val q : Queue<Int> = LinkedList()

    fun push(x: Int) {
        val size = q.size
        q.add(x)
        repeat(size) {
            q.add(q.poll())
        }
    }

    fun pop(): Int {
        return q.poll()
    }

    fun top(): Int {
        return q.peek()
    }

    fun empty(): Boolean {
        return q.isEmpty()
    }
}
```

[문제 링크](https://leetcode.com/problems/implement-queue-using-stacks/)


## Java 풀이
```java
import java.util.Stack;

class MyQueue {

    Stack<Integer> stack1;
    Stack<Integer> stack2;

    public MyQueue() {
        stack1 = new Stack<>();
        stack2 = new Stack<>();
    }

    public void push(int x) {
        stack1.push(x);
    }

    public int pop() {

        if (!stack2.isEmpty()){
            return stack2.pop();
        }

        while (!stack1.isEmpty()){
            stack2.push(stack1.pop());
        }
        return stack2.pop();
    }

    public int peek() {

        if (!stack2.isEmpty()){
            return stack2.peek();
        }

        while (!stack1.isEmpty()){
            stack2.push(stack1.pop());
        }
        return stack2.peek();
    }

    public boolean empty() {
        return stack1.isEmpty() && stack2.isEmpty();
    }
}
```

## kotlin 풀이
```kotlin
import java.util.*

class MyQueue() {
    val stack1 = Stack<Int>()
    val stack2 = Stack<Int>()

    fun push(x: Int) {
        stack1.push(x)
    }

    fun pop(): Int {

        if (stack2.isNotEmpty()) {
            return stack2.pop()
        }

        while (stack1.isNotEmpty()) {
            stack2.push(stack1.pop())
        }

        return stack2.pop()
    }

    fun peek(): Int {
        if (stack2.isNotEmpty()) {
            return stack2.peek()
        }

        while (stack1.isNotEmpty()) {
            stack2.push(stack1.pop())
        }

        return stack2.peek()
    }

    fun empty(): Boolean {
        return stack1.isEmpty() && stack2.isEmpty()
    }
}
```

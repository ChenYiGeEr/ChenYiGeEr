###### 设计一个有getMin功能的栈

###### 栈和队列的区别

最大的区别就是栈是**先入后出** （first in last out）FILO，而队列是**先入先出**（first in first out）FIFO

---

```java
import java.util.Stack;
/**
 * 题目：实现一个特殊的栈，在实现栈的基础功能的基础上，再去实现返回栈中最小元素的操作
 * 要求：pop、push、getMin的时间复杂度都要是O(1)
 * 难度：🌟
 * 解题思路：使用两个栈
 */ 
public class MyStack{
  // 保存正常数据
	private Stack<Integer> stackData;
	// 从栈底到栈顶由大到小保存数据
	private Stack<Integer> stackMin;
	public MyStack(){
    // 无参构造初始化两个栈
    this.stackData = new Stack<Integer>();
    this.stackMin = new Stack<Integer>();
  }
  // 入栈
  public void　push(Integer num){
    // 判断如果stackMin也是空的，就将num也push到stackMin中
		if(this.stackMin.isEmpty()){
      this.stackMin.push(num);
    } else if(num<=this.getMin()){
      // 如果stackMin不是空的，就需要判断num和stackMin顶部的value大小，若num小于等于value，则push到stackMin顶部
    	this.stackMin.push(num);
    }
    // stackData入栈
    this.stackData.push(num);
  }
  // 出栈
  public Integer pop(){
    // 判断如果stackData为空的话则返回null
    if(this.stackData.isEmpty()){
      throw new RuntimeException("your stack is empty!");
    }
    // 不为空的话 肯定stackMin也不为空
    Integer num = this.stackData.pop();
    if(num == this.getMin()){
      // 当弹出元素是栈内最小值的话，将stackMin中栈顶元素弹出
      this.stackMin.pop();
    }
    // 返回num
    return num;
  }
  // 获取栈中最小的数字
  public Integer getMin(){
    // 判断如果stackData为空的话则返回null
    if(this.stackData.isEmpty()){
      throw new RuntimeException("your stack is empty!");
    }
    // 返回stackMin的顶部值
    return this.stackMin.peek();
  }
}
```

---

##### 由两个栈组成的队列


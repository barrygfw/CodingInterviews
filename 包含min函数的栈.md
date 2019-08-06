### 题目描述

定义栈的数据结构，请在该类型中实现一个能够得到栈中所含最小元素的min函数（时间复杂度应为O（1））

### 解析

我们很简单能想到,用一个变量来存储最小的元素,但是问题来了,如果最小的元素出栈了,那么怎么得到次小元素,由此可见,我们不仅仅要保存最小元素,还要保证最小元素出栈后,还能得到次小元素

我们可以用一个辅助栈,来存放当前最小元素和次小元素,我们每次都把最小元素压入辅助栈,就能够博癌症辅助栈的栈顶一直都是最小元素,当最小元素从数据栈内弹出之后,同时弹出辅助栈的最小元素,此时辅助栈的新栈顶元素就是下一个最小值,代码示例如下

### 代码示例

```java
import java.util.Stack;

public class Solution {

    private Stack<Integer> data = null;
    private Stack<Integer> mdata = null;
    public Solution() {
        data = new Stack<Integer>();
        mdata = new Stack<Integer>();
    }
    
    public void push(int node) {
        data.push(node);
        if (mdata.empty() || mdata.peek() > node) {
            mdata.push(node);
        }else {
            mdata.push(mdata.peek());
        }
    }
    
    public void pop() {
        data.pop();
        mdata.pop();
    }
    
    public int top() {
        return data.peek();
    }
    
    public int min() {
        return mdata.peek();
    }
}
```
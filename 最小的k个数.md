### 题目描述

输入n个整数，找出其中最小的K个数。例如输入4,5,1,6,2,7,3,8这8个数字，则最小的4个数字是1,2,3,4,。

### 解析

我们可以从快速排序中收到启发,如果选择的基准点正好是数组的第k个数字,那么数组调整之后,比第k个数字小的所有数字都在数组的左边,比第k个数字大的所有数字都位于数组的右边,数组左边的k个数字就是最小的k个数(这k个数不一定是排序的)

这种方法修改了原始数据,时间复杂度为O(n),如果不允许修改原始数据,那么还有另外一种时间复杂度为nlogk的方法

我们可以使用一个大小为k的大根堆,遍历数组,与堆顶元素比较,如果比堆顶元素小,则堆顶元素移除,当前遍历数字加入大根堆,并重新维护这个大根堆,遍历完成后,大根堆中存储的k个数就是数组中最小的k个数

这种方法特别适合处理海量数据,不会修改原始数据,代码示例如下(代码演示了第一种方法)

### 代码示例

```java
import java.util.ArrayList;
public class Solution {
    public ArrayList<Integer> GetLeastNumbers_Solution(int [] input, int k) {
        ArrayList<Integer> ans = new ArrayList<Integer>();
        int len = input.length;
        if (k > len || k < 1) return ans;
        int start = 0;
        int end = len - 1;
        int index = Partition(input, len, start, end);
        while (index != k - 1) {
            if (index < k - 1) {
                start = index + 1;
                index = Partition(input, len, start, end);
            }else {
                end = index - 1;
                index = Partition(input, len, start, end);
            }
        }
        for (int i = 0; i < k; i++) {
            ans.add(input[i]);
        }
        return ans;
    }
    public int Partition(int[] data, int length, int start, int end) {
        if (data == null || length <= 0 || start < 0 || end >= length) 
            return -1;
        int small = start - 1;
        for (int index = start; index < end; index++) {
            if (data[index] < data[end]) {
                small++;
                if (small != index) 
                    swap(data, small, index);
            }
        }
        small++;
        swap(data, small, end);
        return small;
    }
    public void swap(int[] data, int i, int j) {
        int temp = data[i];
        data[i] = data[j];
        data[j] = temp;
    }
}
```
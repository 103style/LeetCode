# [剑指 Offer 09. 用两个栈实现队列](https://leetcode-cn.com/problems/yong-liang-ge-zhan-shi-xian-dui-lie-lcof/)

---

**leetcode-cn Daily Challenge on June 30, 2020.**

---

> 用两个栈实现一个队列。队列的声明如下，请实现它的两个函数 `appendTail` 和 `deleteHead` ，分别完成在队列尾部插入整数和在队列头部删除整数的功能。(若队列中没有元素，`deleteHead` 操作返回 **-1** )
>
>  
>
> ### 示例 1：
> ```
> 输入：
> ["CQueue","appendTail","deleteHead","deleteHead"]
> [[],[3],[],[]]
> 输出：[null,null,3,-1]
> ```
>
> ### 示例 2：
> ```
> 输入：
> ["CQueue","deleteHead","appendTail","appendTail","deleteHead","deleteHead"]
> [[],[],[5],[2],[],[]]
> 输出：[null,-1,null,null,5,2]
> ```
>
> ### 提示：
> * `1 <= values <= 10000`
> * `最多会对 appendTail、deleteHead 进行 10000 次调用`


---


### Solution
* **mine**
  * **Java**
    * `执行用时：214 ms, 击败了 35.16%, 内存消耗：48.7 MB, 击败了 100%.`
      ```
      //add: O(1)time O(1)space
      //delete: O(N)time O(N)space
      LinkedList<Integer> list1,list2;

      public CQueue() {
          list1 = new LinkedList<>();
          list2 = new LinkedList<>();
      }

      public void appendTail(int value) {
          list1.push(value);
      }

      public int deleteHead() {
          if(list1.isEmpty()){
              return -1;
          }
          while(!list1.isEmpty()){
              list2.push(list1.pop());
          }
          int res = list2.pop();
          while(!list2.isEmpty()){
              list1.push(list2.pop());
          }
          return res;
      }
      ```
      
    * `执行用时：51 ms, 击败了 96.24%, 内存消耗：48.7 MB, 击败了 100%.`
      ```
      LinkedList<Integer> list1,list2;

      public CQueue() {
          list1 = new LinkedList<>();
          list2 = new LinkedList<>();
      }

      public void appendTail(int value) {
          list1.push(value);
      }

      public int deleteHead() {
          if(!list2.isEmpty()){
              return list2.pop();
          }
          if(list1.isEmpty()){
              return -1;
          }
          while(!list1.isEmpty()){
              list2.push(list1.pop());
          }
          return list2.pop();
      }
      ```
---

* **the most votes**
  * `执行用时：51 ms, 击败了 96.24%, 内存消耗：48.7 MB, 击败了 100%.`
    ```
    //add: O(1)time  O(1)space
    //delete: O(1)time in average, O(1)space
    LinkedList<Integer> stack1;
    LinkedList<Integer> stack2;

    public CQueue() {
        stack1 = new LinkedList<>();
        stack2 = new LinkedList<>();
    }

    public void appendTail(int value) {
        stack1.add(value);
    }

    public int deleteHead() {
        if (stack2.isEmpty()) {
            if (stack1.isEmpty()) return -1;
            while (!stack1.isEmpty()) {
                stack2.add(stack1.pop());
            }
            return stack2.pop();
        } else return stack2.pop();
    }
    ```

---

# 最多能完成排序的块
```题目描述
    这个问题和“最多能完成排序的块”相似，但给定数组中的元素可以重复，输入数组最大长度为2000，其中的元素最大为10**8。
    arr是一个可能包含重复元素的整数数组，我们将这个数组分割成几个“块”，并将这些块分别进行排序。之后再连接起来，使得连接的结果和按升序排序后的原数组相同。
    我们最多能将数组分成多少块？


示例 1:
    输入: arr = [5,4,3,2,1]
    输出: 1
    解释:
    将数组分成2块或者更多块，都无法得到所需的结果。
    例如，分成 [5, 4], [3, 2, 1] 的结果是 [4, 5, 1, 2, 3]，这不是有序的数组。


示例 2:
    输入: arr = [2,1,3,4,4]
    输出: 4
    解释:
    我们可以把它分成两块，例如 [2, 1], [3, 4, 4]。
    然而，分成 [2, 1], [3], [4], [4] 可以得到最多的块数。


注意:
    arr的长度在[1, 2000]之间。
    arr[i]的大小在[0, 10**8]之间。

var maxChunksToSorted = function (arr) {//TODO}
```

# 数组去重 
const array = [1, 2, 3, 1, 9, 1, 2, 8]

1、可以使用集合Set实现
```javascript
const array = [1, 2, 3, 1, 9, 1, 2, 8]

const uniq = arr => […new Set(arr)]

const result = uniq(array); // [1, 2, 3, 9, 8]
```

2、使用reduce
```javascript
const array = [1, 2, 3, 1, 9, 1, 2, 8]

const uniq = arr => arr.reduce((acc, curr) => acc.includes(curr) ? acc : […acc, curr], [])

const result = uniq(array); // [1, 2, 3, 9, 8]
```

# 查找重复元素：找出数组arr中重复出现过的元素 [1,2,3,4,1,2,2,2] => [1,2]

# 字符串陷阱
```
//字符串陷阱   请输出结果并进行解释
function showCase(value) {
  switch(value) {
    case 'A':
      console.log('Case A');
      break;
    case 'B':
      console.log('Case B');
      break;
    case undefined:
      console.log('undefined');
      break;
    default:
      console.log('Do not know!');
  }
}
showCase(new String('A'));
```

答案：Do not know!

在 switch 内部使用严格相等 === 进行判断，并且 new String("A") 返回的是一个对象，而 String("A") 则是直接返回字符串 "A"。

# 提升变量
```
//提升变量  请输出结果并进行解释
var name = 'spring';
(function () {
    if (typeof name === 'undefined') {
      var name = 'summer';
      console.log(name);
    } else {
      console.log(name);
    }
})();
```
答案:summer

在 JavaScript中， functions 和 variables 会被提升。变量提升是JavaScript将声明移至作用域 scope (全局域或者当前函数作用域) 顶部的行为。
这意味着你可以在声明一个函数或变量之前引用它，或者可以说：一个变量或函数可以在它被引用之后声明。

# 添加元素(指定位置添加)

描述：在数组arr的index处添加元素item，不要直接修改数组arr，结果返回新的数组 [1,2,3] 2,6 结果为[1,2,6,3]

# filter过滤器
```
var ary = [0,1,2];
ary[10] = 10;
ary.filter(function(x) {
  return x === undefined;
});
```

# 求两个数组的交集
```
const firstArray = [2, 2, 4, 1];
const secondArray = [1, 2, 0, 2]; 
intersection(firstArray, secondArray); // 实现intersection函数
```

# 给定一个整数数组，找到从三个整数中产生的最大乘积
```
const unsortedArray = [-10, 7, 2, 3, 5, -1, -7];
computeProduct(unsortedArray) // 实现computeProduct函数
```

# 移除数组中的元素(返回新的数组) 

描述：移除数组arr中的所有值和item相等的元素。不要直接修改数组，结果返回新的数组
```
 function remove(arr, item) { //TODO}
 let newArray = remove([1,2,3,4,2],2);//[1,3,4]
```

```
答案：
function remove(arr, item) { 
  return arr.filter(a => item !== a)
}
```

# 在末尾添加元素

描述：在数组arr末尾添加元素item，不要直接修改数组arr，结果返回新数组 [1,2,3] 添加元素4 返回新数组[1,2,3,4]

```
答案：
const arr = [1, 2, 3];
const newArr = [...arr, 4]; // [1, 2, 3, 4]
或者
const arr = [1, 2, 3];
const newArr = arr.concat(4); // [1, 2, 3, 4]
```

# 给定一个整数数组，请找出两个元素之间的最大差，较小值的元素必须位于较大元素之前
```
const array = [7, 8, 15, 9, 20, 3, 1, 10];
findLargestDifference(array)
function findLargestDifference(array) {
//TODO
}//符合条件的两个数字:7和20
```

# 查找数组元素位置

找出元素item在给定数组arr中的位置 描述：如果数组中存在item就返回元素在数组中的位置，否则就会返回-1 [1,2,3,4,5,6] --> 存在3就输出2，存在7输出-1
```
function indexOf(arr, item) {
//TODO
}
```

# 数组形式的整数加法
```
题目描述：
        对于非负整数 X 而言，X 的数组形式是每位数字按从左到右的顺序形成的数组。例如，如果 X = 1231，那么其数组形式为 [1,2,3,1]。给定非负整数 X 的数组形式 A，返回整数 X+K 的数组形式。

    示例 1：

        输入：A = [1,2,0,0], K = 34
        输出：[1,2,3,4]
        解释：1200 + 34 = 1234
    示例 2：

        输入：A = [2,7,4], K = 181
        输出：[4,5,5]
        解释：274 + 181 = 455


    示例 3：
        输入：A = [9,9,9,9,9,9,9,9,9,9], K = 1
        输出：[1,0,0,0,0,0,0,0,0,0,0]
        解释：9999999999 + 1 = 10000000000


    提示：

        1 <= A.length <= 10000
        0 <= A[i] <= 9
        0 <= K <= 10000
        如果 A.length > 1，那么 A[0] != 0


var addToArrayForm = function (A, K) {//TODO}
```

# 字符的最短距离

```
题目描述
    给定一个字符串 S 和一个字符 C。返回一个代表字符串 S 中每个字符到字符串 S 中的字符 C 的最短距离的数组。


    示例 :
        输入: S = "loveleetcode", C = 'e'
        输出: [3, 2, 1, 0, 1, 0, 0, 1, 2, 2, 1, 0]

    说明:
        - 字符串 S 的长度范围为 [1, 10000]。
        - C 是一个单字符，且保证是字符串 S 里的字符。
        - S 和 C 中的所有字母均为小写字母。

var shortestToChar = function (S, C) {//TODO}
```

# 用栈实现队列
```
题目描述
  使用栈实现队列的下列操作：

  push(x) -- 将一个元素放入队列的尾部。
  pop() -- 从队列首部移除元素。
  peek() -- 返回队列首部的元素。
  empty() -- 返回队列是否为空。
  示例:

  MyQueue queue = new MyQueue();

  queue.push(1);
  queue.push(2);
  queue.peek(); // 返回 1
  queue.pop(); // 返回 1
  queue.empty(); // 返回 false
  说明:

  你只能使用标准的栈操作 -- 也就是只有 push to top, peek/pop from top, size, 和 is empty 操作是合法的。
  你所使用的语言也许不支持栈。你可以使用 list 或者 deque（双端队列）来模拟一个栈，只要是标准的栈操作即可。
  假设所有操作都是有效的、 （例如，一个空的队列不会调用 pop 或者 peek 操作）。


var MyQueue = function () {
    //TODO
};

/**
 * Push element x to the back of queue. 
 * @param {number} x
 * @return {void}
 */
MyQueue.prototype.push = function (x) {
    //TODO
};

/**
 * Removes the element from in front of queue and returns that element.
 * @return {number}
 */
MyQueue.prototype.pop = function () {
    //TODO
};

/**
 * Get the front element.
 * @return {number}
 */
MyQueue.prototype.peek = function () {
    //TODO
};

/**
 * Returns whether the queue is empty.
 * @return {boolean}
 */
MyQueue.prototype.empty = function () {
    //TODO
};
```

# 手动实现数组 Reduce 方法
```
if (!Array.prototype.reduce) {
  Object.defineProperty(Array.prototype, "reduce", {
    value: function (callback) {
      if (this === null) {
        throw new TypeError("Array.prototype.reduce called on null or undefiend");
      }
      if (typeof callback !== "function") {
        throw new TypeError(callback + "is not a function");
      }
      var o = Object(this);
      // 位运算符  
      // >>>是无符号右移运算符，保证结果为非负整数,是length值所要的数字。(如果运算为NaN，length结果为0，在后续代码中遍历对象也不会抛出异常)
      var len = o.length >>> 0;
      var k = 0;
      var value;
      if (arguments.length >= 2) {
        value = arguments[1];
      } else {
        while (k < len && !(k in o)) {
          k++;
        }
        if (k >= len) {
          throw new TypeError("Reduce of empty array with no initial value");
        }
        value = o[k++];
      }
      while (k < len) {
        if (k in o) {
          value = callback(value, o[k], k, o);
        }
        k++;
      }
      return value;
    },
  });
}
```

# 字符串解码
```
题目描述:
    给定一个经过编码的字符串，返回它解码后的字符串。
    编码规则为: k[encoded_string]，表示其中方括号内部的 encoded_string 正好重复 k 次。注意 k 保证为正整数。
    你可以认为输入字符串总是有效的；输入字符串中没有额外的空格，且输入的方括号总是符合格式要求的。
    此外，你可以认为原始数据不包含数字，所有的数字只表示重复的次数 k ，例如不会出现像 3a 或 2[4] 的输入。

示例 1：
    输入：s = "3[a]2[bc]"
    输出："aaabcbc"


示例 2：
    输入：s = "3[a2[c]]"
    输出："accaccacc"


示例 3：
    输入：s = "2[abc]3[cd]ef"
    输出："abcabccdcdcdef"


示例 4：
    输入：s = "abc3[cd]xyz"
    输出："abccdcdcdxyz"

var decodeString = function (s) {//TODO}
```

# 设计一个支持增量操作的栈
```
题目描述：
        请你设计一个支持下述操作的栈。
        实现自定义栈类 CustomStack ：
        CustomStack(int maxSize)：用 maxSize 初始化对象，maxSize 是栈中最多能容纳的元素数量，栈在增长到 maxSize 之后则不支持 push 操作。
        void push(int x)：如果栈还未增长到 maxSize ，就将 x 添加到栈顶。
        int pop()：弹出栈顶元素，并返回栈顶的值，或栈为空时返回 -1 。
        void inc(int k, int val)：栈底的 k 个元素的值都增加 val 。如果栈中元素总数小于 k ，则栈中的所有元素都增加 val 。


    示例：
        输入：
        ["CustomStack","push","push","pop","push","push","push","increment","increment","pop","pop","pop","pop"]
        [[3],[1],[2],[],[2],[3],[4],[5,100],[2,100],[],[],[],[]]
        输出：
        [null,null,null,2,null,null,null,null,null,103,202,201,-1]
        解释：
        CustomStack customStack = new CustomStack(3); // 栈是空的 []
        customStack.push(1); // 栈变为 [1]
        customStack.push(2); // 栈变为 [1, 2]
        customStack.pop(); // 返回 2 --> 返回栈顶值 2，栈变为 [1]
        customStack.push(2); // 栈变为 [1, 2]
        customStack.push(3); // 栈变为 [1, 2, 3]
        customStack.push(4); // 栈仍然是 [1, 2, 3]，不能添加其他元素使栈大小变为 4
        customStack.increment(5, 100); // 栈变为 [101, 102, 103]
        customStack.increment(2, 100); // 栈变为 [201, 202, 103]
        customStack.pop(); // 返回 103 --> 返回栈顶值 103，栈变为 [201, 202]
        customStack.pop(); // 返回 202 --> 返回栈顶值 202，栈变为 [201]
        customStack.pop(); // 返回 201 --> 返回栈顶值 201，栈变为 []
        customStack.pop(); // 返回 -1 --> 栈为空，返回 -1


    提示：
        1 <= maxSize <= 1000
        1 <= x <= 1000
        1 <= k <= 1000
        0 <= val <= 100
        每种方法 increment，push 以及 pop 分别最多调用 1000 次   

/**
 * @param {number} maxSize
 */
var CustomStack = function (maxSize) {
    //TODO
};

/** 
 * @param {number} x
 * @return {void}
 */
CustomStack.prototype.push = function (x) {
    //TODO
};

/**
 * @return {number}
 */
CustomStack.prototype.pop = function () {
    //TODO
};

/** 
 * @param {number} k 
 * @param {number} val
 * @return {void}
 */
CustomStack.prototype.increment = function (k, val) {
    //TODO
};
```

# 手写实现Objeect.freeze
Object.freeze方法可以冻结一个对象，冻结是指不能向这个对象添加新的属性，不能修改现有属性的值，不能删除属性，甚至不能修改这个对象现有属性的可枚举性、可配置性、可写性。换句话说，这个对象永远是不可变的，此方法返回被冻结的对象。Object.freeze是浅冻结。

```
function myFreeze(obj) {
  for(item in obj){
    if(obj[item] instanceof Object){
      myFreeze(obj[item]);
    } else {
      Object.defineProperty(obj, item, {
        writable: false;
      })
    }
  }
  Object.seal(obj);
}
```

# 二叉树的最大深度
```
题目描述：
    给定一个二叉树，找出其最大深度。
    二叉树的深度为根节点到最远叶子节点的最长路径上的节点数。
    说明: 叶子节点是指没有子节点的节点。

示例：
    给定二叉树 [3,9,20,null,null,15,7]，

        3
       / \
      9  20
     /    \
    15     7

    返回它的最大深度 3 。
var maxDepth = function(root) {
    //TODO
}
```

# LRU缓存机制
```
题目描述：
    运用你所掌握的数据结构，设计和实现一个 LRU (最近最少使用) 缓存机制 。
    实现 LRUCache 类：
        LRUCache(int capacity) 以正整数作为容量 capacity 初始化 LRU 缓存
        int get(int key) 如果关键字 key 存在于缓存中，则返回关键字的值，否则返回 -1 。
        void put(int key, int value) 如果关键字已经存在，则变更其数据值；如果关键字不存在，则插入该组「关键字-值」。当缓存容量达到上限时，它应该在写入新数据之前删除最久未使用的数据值，从而为新的数据值留出空间。


示例：

    输入：["LRUCache", "put", "put", "get", "put", "get", "put", "get", "get", "get"]
            [[2], [1, 1], [2, 2], [1], [3, 3], [2], [4, 4], [1], [3], [4]]
    输出：[null, null, null, 1, null, -1, null, -1, 3, 4]
    解释：
        LRUCache lRUCache = new LRUCache(2);
        lRUCache.put(1, 1); // 缓存是 {1=1}
        lRUCache.put(2, 2); // 缓存是 {1=1, 2=2}
        lRUCache.get(1); // 返回 1
        lRUCache.put(3, 3); // 该操作会使得关键字 2 作废，缓存是 {1=1, 3=3}
        lRUCache.get(2); // 返回 -1 (未找到)
        lRUCache.put(4, 4); // 该操作会使得关键字 1 作废，缓存是 {4=4, 3=3}
        lRUCache.get(1); // 返回 -1 (未找到)
        lRUCache.get(3); // 返回 3
        lRUCache.get(4); // 返回 4

var Node = function (key = null, val = null, next = null, pre = null) {
    //TODO
}
var LRUCache = function (capacity = 0) {
    //TODO
};

/** 
 * @param {number} key
 * @return {number}
 */
LRUCache.prototype.get = function (key) {
    //TODO
};

/** 
 * @param {number} key 
 * @param {number} value
 * @return {void}
 */
LRUCache.prototype.put = function (key, value) {
    //TODO
};
```

# 相交链表
```
题目描述
    编写一个程序，找到两个单链表相交的起始节点。

示例1：
    输入：intersectVal = 8, listA = [4,1,8,4,5], listB = [5,0,1,8,4,5], skipA = 2, skipB = 3
    输出：Reference of the node with value = 8
    输入解释：相交节点的值为 8 （注意，如果两个链表相交则不能为 0）。从各自的表头开始算起，链表 A 为 [4,1,8,4,5]，链表 B 为 [5,0,1,8,4,5]。在 A 中，相交节点前有 2 个节点；在 B 中，相交节点前有 3 个节点。


示例2：
    输入：intersectVal&nbsp;= 2, listA = [0,9,1,2,4], listB = [3,2,4], skipA = 3, skipB = 1
    输出：Reference of the node with value = 2
    输入解释：相交节点的值为 2 （注意，如果两个链表相交则不能为 0）。从各自的表头开始算起，链表 A 为 [0,9,1,2,4]，链表 B 为 [3,2,4]。在 A 中，相交节点前有 3 个节点；在 B 中，相交节点前有 1 个节点。


示例3：
    输入：intersectVal = 0, listA = [2,6,4], listB = [1,5], skipA = 3, skipB = 2
    输出：null
    输入解释：从各自的表头开始算起，链表 A 为 [2,6,4]，链表 B 为 [1,5]。由于这两个链表不相交，所以 intersectVal 必须为 0，而 skipA 和 skipB 可以是任意值。
    解释：这两个链表不相交，因此返回 null。



注意：
    如果两个链表没有交点，返回 null.
    在返回结果后，两个链表仍须保持原有的结构。
    可假定整个链表结构中没有循环。


    var getIntersectionNode = function(headA, headB) {
        //TODO
    }
```

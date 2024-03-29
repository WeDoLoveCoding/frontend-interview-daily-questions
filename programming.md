# 字典序排数

```
给你一个整数 n ，按字典序返回范围 [1, n] 内所有整数。

你必须设计一个时间复杂度为 O(n) 且使用 O(1) 额外空间的算法。


示例 1：
输入：n = 13
输出：[1,10,11,12,13,2,3,4,5,6,7,8,9]

示例 2：
输入：n = 2
输出：[1,2]

var lexicalOrder = function(n) {
   let nums = [];
   for (let i = 1; i <= n; i++) {
    nums.push(i);
   }
   return nums.sort();
};

或

var lexicalOrder = function (n) {
    const ret = [];
    let number = 1;
    for (let i = 0; i < n; i++) {
        ret.push(number);
        if (number * 10 <= n) {
            number *= 10;
        } else {
            while (number % 10 === 9 || number + 1 > n) {
                number = Math.floor(number / 10);
            }
            number++;
        }
    }
    return ret;
};
```

# 反转字符串中的元音字母

```
给你一个字符串 s ，仅反转字符串中的所有元音字母，并返回结果字符串。

元音字母包括 'a'、'e'、'i'、'o'、'u'，且可能以大小写两种形式出现。


示例 1：
输入：s = "hello"
输出："holle"

示例 2：
输入：s = "leetcode"
输出："leotcede"

// 双指针：我们可以使用两个指针 i 和 j 对字符串相向地进行遍历。

// 具体地，指针 i 初始时指向字符串 s 的首位，指针 j 初始时指向字符串 s 的末位。在遍历的过程中，我们不停地将 i 向右移动，直到 i 指向一个元音字母（或者超出字符串的边界范围）；同时，我们不停地将 j 向左移动，直到 j 指向一个元音字母。此时，如果 i<j，那么我们交换 i 和 j 指向的元音字母，否则说明所有的元音字母均已遍历过，就可以退出遍历的过程。

var reverseVowels = function (s) {
    const n = s.length;
    const arr = Array.from(s);
    let i = 0, j = n - 1;
    while (i < j) {
        while (i < n && !isVowel(arr[i])) {
            ++i;
        }
        while (j > 0 && !isVowel(s[j])) {
            --j;
        }
        if (i < j) {
            swap(arr, i, j);
            ++i;
            --j;
        }
    }
    return arr.join('');
}

const isVowel = (ch) => {
    return "aeiouAEIOU".indexOf(ch) >= 0;
}

const swap = (arr, i, j) => {
    const temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
}
```

# 找不同
```
给定两个字符串 s 和 t，它们只包含小写字母。
字符串 t 由字符串 s 随机重排，然后在随机位置添加一个字母。
请找出在 t 中被添加的字母。

示例 1：

输入：s = "abcd", t = "abcde"
输出："e"
解释：'e' 是那个被添加的字母。


示例 2：

输入：s = "", t = "y"
输出："y"


示例 3：

输入：s = "a", t = "aa"
输出："a"


示例 4：

输入：s = "ae", t = "aea"
输出："a"

var findTheDifference = function (s, t) {
    // TODO
};
```

# 消失的数字
```
数组nums包含从0到n的所有整数，但其中缺了一个。请编写代码找出那个缺失的整数。你有办法在O(n)时间内完成吗？


示例 1：
输入：[3,0,1]
输出：2


示例 2：
输入：[9,6,4,2,3,5,7,0,1]
输出：8


var missingNumber = function(nums) {
    // TODO
};
```

# 两个数组的交集 II
```
给你两个整数数组&nbsp;nums1 和 nums2 ，请你以数组形式返回两数组的交集。返回结果中每个元素出现的次数，应与元素在两个数组中都出现的次数一致（如果出现次数不一致，则考虑取较小值）。可以不考虑输出结果的顺序。


示例 1：
输入：nums1 = [1,2,2,1], nums2 = [2,2]
输出：[2,2]


示例 2:
输入：nums1 = [4,9,5], nums2 = [9,4,9,8,4]
输出：[4,9]
&nbsp;

提示：
1 <= nums1.length, nums2.length <= 1000
0 <= nums1[i], nums2[i] <= 1000


var intersect = function(nums1, nums2) {
    // TODO
};
```

# 反转字符串
```
编写一个函数，其作用是将输入的字符串反转过来。输入字符串以字符数组 s 的形式给出。

不要给另外的数组分配额外的空间，你必须原地修改输入数组、使用 O(1) 的额外空间解决这一问题。


示例 1：
输入：s = ["h","e","l","l","o"]
输出：["o","l","l","e","h"]


示例 2：
输入：s = ["H","a","n","n","a","h"]
输出：["h","a","n","n","a","H"]


提示：
1 <= s.length <= 105
s[i] 都是 ASCII 码表中的可打印字符



var reverseString = function(s) {
    //TODO
};
```

# 合并两个有序数组
```
给你两个按 非递减顺序 排列的整数数组&nbsp;nums1 和 nums2，另有两个整数 m 和 n ，分别表示 nums1 和 nums2 中的元素数目。

请你 合并 nums2 到 nums1 中，使合并后的数组同样按 非递减顺序 排列。

注意：最终，合并后数组不应由函数返回，而是存储在数组 nums1 中。为了应对这种情况，nums1 的初始长度为 m + n，其中前 m 个元素表示应合并的元素，后 n 个元素为 0 ，应忽略。nums2 的长度为 n 。

&nbsp;
示例 1：
输入：nums1 = [1,2,3,0,0,0], m = 3, nums2 = [2,5,6], n = 3
输出：[1,2,2,3,5,6]
解释：需要合并 [1,2,3] 和 [2,5,6] 。
合并结果是 [1,2,2,3,5,6] ，其中斜体加粗标注的为 nums1 中的元素。


示例 2：
输入：nums1 = [1], m = 1, nums2 = [], n = 0
输出：[1]
解释：需要合并 [1] 和 [] 。
合并结果是 [1] 。


示例 3：
输入：nums1 = [0], m = 0, nums2 = [1], n = 1
输出：[1]
解释：需要合并的数组是 [] 和 [1] 。
合并结果是 [1] 。
注意，因为 m = 0 ，所以 nums1 中没有元素。nums1 中仅存的 0 仅仅是为了确保合并结果可以顺利存放到 nums1 中。
&nbsp;

提示：
nums1.length == m + n
nums2.length == n
0 <= m, n <= 200
1 <= m + n <= 200
-109 <= nums1[i], nums2[j] <= 109

var merge = function (nums1, m, nums2, n) {
    // TODO
};
```

# 数组相对排序
```
给定两个数组，arr1 和 arr2:

arr2 中的元素各不相同
arr2 中的每个元素都出现在 arr1 中
对 arr1 中的元素进行排序，使 arr1 中项的相对顺序和 arr2 中的相对顺序相同。未在 arr2 中出现过的元素需要按照升序放在 arr1 的末尾。

var relativeSortArray = function (arr1, arr2) {
    // TODO
};
```

# 找到所有数组中消失的数字
```
给你一个含 n 个整数的数组 nums ，其中 nums[i] 在区间 [1, n] 内。请你找出所有在 [1, n] 范围内但没有出现在 nums 中的数字，并以数组的形式返回结果。


示例 1：
输入：nums = [4,3,2,7,8,2,3,1]
输出：[5,6]


示例 2：
输入：nums = [1,1]
输出：[2]
&nbsp;

提示：
n == nums.length
1 <= n <= 105
1 <= nums[i] <= n
进阶：你能在不使用额外空间且时间复杂度为 O(n) 的情况下解决这个问题吗? 你可以假定返回的数组不算在额外空间内

var findDisappearedNumbers = function (nums) {
    //TODO
};
```

# 设计哈希集合
```
不使用任何内建的哈希表库设计一个哈希集合（HashSet）。
实现 MyHashSet 类：
void add(key) 向哈希集合中插入值 key 。
bool contains(key) 返回哈希集合中是否存在这个值 key 。
void remove(key) 将给定值 key 从哈希集合中删除。如果哈希集合中没有这个值，什么也不做。

示例：

输入：
["MyHashSet", "add", "add", "contains", "contains", "add", "contains", "remove", "contains"]
[[], [1], [2], [1], [3], [2], [2], [2], [2]]
输出：
[null, null, null, true, false, null, true, null, false]

解释：
MyHashSet myHashSet = new MyHashSet();
myHashSet.add(1);      // set = [1]
myHashSet.add(2);      // set = [1, 2]
myHashSet.contains(1); // 返回 True
myHashSet.contains(3); // 返回 False ，（未找到）
myHashSet.add(2);      // set = [1, 2]
myHashSet.contains(2); // 返回 True
myHashSet.remove(2);   // set = [1]
myHashSet.contains(2); // 返回 False ，（已移除）

var MyHashSet = function () {

};

/** 
 * @param {number} key
 * @return {void}
 */
MyHashSet.prototype.add = function (key) {

};

/** 
 * @param {number} key
 * @return {void}
 */
MyHashSet.prototype.remove = function (key) {

};

/** 
 * @param {number} key
 * @return {boolean}
 */
MyHashSet.prototype.contains = function (key) {

};

/**
 * Your MyHashSet object will be instantiated and called as such:
 * var obj = new MyHashSet()
 * obj.add(key)
 * obj.remove(key)
 * var param_3 = obj.contains(key)
 */
```

# 搜索插入位置
```
给定一个排序数组和一个目标值，在数组中找到目标值，并返回其索引。如果目标值不存在于数组中，返回它将会被按顺序插入的位置。
请必须使用时间复杂度为 O(log n) 的算法。


示例 1:
输入: nums = [1,3,5,6], target = 5
输出: 2


示例 2:
输入: nums = [1,3,5,6], target = 2
输出: 1


示例 3:
输入: nums = [1,3,5,6], target = 7
输出: 4


示例 4:
输入: nums = [1,3,5,6], target = 0
输出: 0


示例 5:
输入: nums = [1], target = 0
输出: 0

var searchInsert = function (nums, target) {
    //TODO
};
```

# 用栈实现队列
```
请你仅使用两个栈实现先入先出队列。队列应当支持一般队列支持的所有操作（push、pop、peek、empty）：
实现 MyQueue 类：

void push(int x) 将元素 x 推到队列的末尾
int pop() 从队列的开头移除并返回元素
int peek() 返回队列开头的元素
boolean empty() 如果队列为空，返回 true ；否则，返回 false
说明：

你 只能 使用标准的栈操作 —— 也就是只有 push to top, peek/pop from top, size, 和 is empty 操作是合法的。
你所使用的语言也许不支持栈。你可以使用 list 或者 deque（双端队列）来模拟一个栈，只要是标准的栈操作即可。


示例 1：
输入：
["MyQueue", "push", "push", "peek", "pop", "empty"]
[[], [1], [2], [], [], []]
输出：
[null, null, null, 1, 1, false]

解释：
MyQueue myQueue = new MyQueue();
myQueue.push(1); // queue is: [1]
myQueue.push(2); // queue is: [1, 2] (leftmost is front of the queue)
myQueue.peek(); // return 1
myQueue.pop(); // return 1, queue is [2]
myQueue.empty(); // return false


var MyQueue = function () {

};

/** 
 * @param {number} x
 * @return {void}
 */
MyQueue.prototype.push = function (x) {

};

/**
 * @return {number}
 */
MyQueue.prototype.pop = function () {

};

/**
 * @return {number}
 */
MyQueue.prototype.peek = function () {

};

/**
 * @return {boolean}
 */
MyQueue.prototype.empty = function () {

};

/**
 * Your MyQueue object will be instantiated and called as such:
 * var obj = new MyQueue()
 * obj.push(x)
 * var param_2 = obj.pop()
 * var param_3 = obj.peek()
 * var param_4 = obj.empty()
 */
```

# 移除链表元素
```
给你一个链表的头节点 head 和一个整数 val ，请你删除链表中所有满足 Node.val == val 的节点，并返回 新的头节点 。


示例 1：
输入：head = [1,2,6,3,4,5,6], val = 6
输出：[1,2,3,4,5]


示例 2：
输入：head = [], val = 1
输出：[]


示例 3：
输入：head = [7,7,7,7], val = 7
输出：[]

var removeElements = function (head, val) {
    // TODO
};
```

# 手写一个发布订阅模式

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

# 环形链表
```
题目描述：
    给定一个链表，判断链表中是否有环。
    如果链表中有某个节点，可以通过连续跟踪 next 指针再次到达，则链表中存在环。 为了表示给定链表中的环，我们使用整数 pos 来表示链表尾连接到链表中的位置（索引从 0 开始）。 如果 pos 是 -1，则在该链表中没有环。注意：pos 不作为参数进行传递，仅仅是为了标识链表的实际情况。

    如果链表中存在环，则返回 true 。 否则，返回 false 。

var hasCycle = function (head) {
    //TODO
};
```

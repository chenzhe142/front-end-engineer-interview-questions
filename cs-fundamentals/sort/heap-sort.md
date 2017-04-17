# heap & priority queue

[Leetcode - kth largest element in an array](https://leetcode.com/problems/kth-largest-element-in-an-array/)

## heap

利用最大堆进行排序的算法HEAPSORT的基本思想是：

首先利用`maxHeapify(array, startIndex, endIndex)`算法将一个n元素数组转换为最大堆，此时该数组的最大元素就是A[0]，所以，交换A[0]和A[n-1]。 然后，将数组A[0…n-2]看成新的数组，该数组中，除了根节点之外，其他左右子树依然满足最大堆的性质，只是根节点因为发生了交换所以有可能不满足最大堆性质，所以，对根节点调用MAX-HEAPIFY即可。

重复以上这个过程直到堆的大小变为1。
该算法的时间复杂度为O(n lg n)。

（节选自[算法导论笔记：06 - 堆排序](http://blog.csdn.net/gqtcgq/article/details/45200959))

```javascript

function swap(nums, i, j) {
  const temp = nums[i];
  nums[i] = nums[j];
  nums[j] = temp;
}

function maxHeapify(nums, i, length) {
  let left = 2 * i + 1;
  let right = 2 * i + 2;

  let largest = i;

  if (left < length && nums[largest] < nums[left]) {
    largest = left;
  }

  if (right < length && nums[largest] < nums[right]) {
    largest = right;
  }

  if (largest !== i) {
    swap(nums, i, largest);

    maxHeapify(nums, largest, length);
  }
}

function heapify(nums) {
  for (let i = Math.floor(nums.length/2) - 1; i >= 0; i -= 1) {
    maxHeapify(nums, i, nums.length);
  }
}

function heapsort(nums) {
  let length = nums.length;

  for (let i = nums.length - 1; i >= 0; i -= 1) {
    swap(0, i);
    length -= 1;
    maxHeapify(nums, 0, length);
  }
}

```

## priority queue

### `heap.insert()`

### `heap.extractMax()`
基于最大堆，移除`nums[0]`（最大值），将`nums[nums.length-1]`移至第一个，进行`maxHeapify()`

```javascript
function extractMax(nums) {
  const max = nums[0];
  if (nums.length > 0) {
    nums[0] = nums[nums.length-1];
    nums.pop();

    maxHeapify(nums, 0, nums.length);
  }
}
```

### `heap.increaseKey(nums, i, newKey, length)`
从下至上的heapify过程。
将某个元素的关键字增加为key，重新构造优先队列。

该算法将`A[i]`的关键字置为key，然后从索引i开始向上比较，如果`A[i] > A[PARENT(i)]`，则交换`A[i]` 和`A[PARENT(i)]`，然后`i= PARENT(i)`。重复这个过程直到I = 0。

该算法与`maxHeapify()`类似，只不过该算法是从下往上维护最大堆的性质。该算法的时间复杂度为O(lg n)。

代码如下：

```javascript
//from down to up to keep the property of max heap
function increaseKey(nums, i, newKey, length) {
  if (nums[i] > key) {
    throw new Error('The value of newKey is not valid');
  }

  let largest = i;
  nums[i] = newKey;

  while (i > 0) {
    let parent = Math.floor((i-1)/2);

    if (nums[parent] < nums[i]) {
      swap(nums, i, parent);  
      i = parent;
    } else {
      break;
    }
  }
}
```

### `heap.insert(nums, newVal)`
向优先队列中插入元素。
该算法首先将heapsiize增加，然后置A[heapsize]为负无穷大。然后调用increaseKey(nums, i, newKey, length) 时间复杂度为(lg n)。

代码如下：

```javascript
function insert(nums, newVal) {
  nums.push(Number.NEGATIVE_INFINITY);
  increaseKey(nums, nums.length-1, newVal, nums.length-1);
}
```

### `heap.delete(nums, index)`
从优先队列中删除元素。

该算法将最后的元素A[heapsize]存储到A[index]中，然后减少heapsize。

然后比较当前index元素的值与父母的值大小，如果A[index] < A[PARENT(index)]，则从上往下维护堆的性质（MAXHEAPIFY），否则，从下往上维护堆的性质(INCREASE-KEY)。

代码如下：

```javascript
function delete(nums, index) {
  nums[index] = nums[nums.length-1];
  let key = nums[index];

  let parent = Math.floor((index-1)/2);
  nums.pop();

  if (parent >= 0 && key > nums[parent]) {
    increaseKey(nums, index, key, nums.length);
  } else {
    maxHeapify(nums, index, nums.length);
  }

}
```

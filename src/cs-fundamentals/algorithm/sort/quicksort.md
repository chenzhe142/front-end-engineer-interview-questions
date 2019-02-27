# quicksort & quick selection

[Leetcode - kth largest element in an array](https://leetcode.com/problems/kth-largest-element-in-an-array/)

## Partition

```javascript
// partIndex represents the start of last part
function partition(nums, startIndex, endIndex, pivotIndex) {
  let pivotVal = nums[pivotIndex];
  swap(nums, endIndex, pivotIndex);

  let partIndex = startIndex;

  for (let i = startIndex; i < endIndex; i += 1) {
    const val = nums[i];

    if (val < pivotVal) {
      swap(nums, i, partIndex);
      partIndex += 1;
    }
  }

  //move pivotVal to the correct place
  swap(partIndex, endIndex);
  return partIndex;
}
```

## Quicksort

```javascript
function quicksort(nums, startIndex, endIndex) {
  if (startIndex < endIndex) {
    q = partition(nums, startIndex, endIndex);
    quicksort(nums, startIndex, q-1);
  }
}
```

## Quick selection

```javascript
function select(nums, startIndex, endIndex, k) {
  if (left === right) {
    return nums[left];
  }

  let pivotIndex = endIndex;
  pivotIndex = partition(nums, startIndex, endIndex, pivotIndex);

  if (pivotIndex === k) {
    return nums[pivotIndex];
  } else if (pivotIndex < k) {
    return select(nums, startIndex, pivotIndex-1, k);
  } else {
    return select(nums, pivotIndex+1, endIndex, k);
  }
}
```

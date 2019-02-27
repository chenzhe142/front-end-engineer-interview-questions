# Interview

不管使用什么样的介质来进行面试，在最开始一定要**完全理解题意**，把不确定的点跟面试官交流清楚，并让面试官提供几个sample input和output。

## Using laptop:
1. 写出伪代码，简单介绍思路。上机写代码最重要的一点是代码可以跑，所以要尽快动笔。
2. 对待corner case，可以提前写好一些test case，边写边验证，有助于在coding的过程中发现bug。

以下是一个test-driven coding的例子：

```javascript
// leetcode: remove K digits https://leetcode.com/problems/remove-k-digits/#/description
var removeKdigits = function(num, k) {

    const getNumString = function(num, k) {
        if (k === 0) {
            return num;
        }

        if (num.length === k) {
            return "";
        }

        let minVal = parseInt(num[0], 10);
        let minIndex = 0;

        for (let i = 0; i <= k; i += 1) {
            const n = parseInt(num[i], 10);
            if (n < minVal) {
                minVal = n;
                minIndex = i;
            }
        }

        const subRes = getNumString(num.substring(minIndex+1), k-minIndex);

        return num[minIndex] + subRes;
    };

    // trim front zeros
    let newNum = getNumString(num, k);

    let startIndex = 0;
    while (startIndex < newNum.length && newNum[startIndex] === '0') {
        startIndex += 1;
    }

    return startIndex >= newNum.length ? "0" : newNum.substring(startIndex);
};
```

```javascript

var num1 = '112';
var k1 = 1;
var res1 = '11';

console.log(removeKdigits(num1, k1));
console.log(removeKdigits(num1, k1) === res1);

var num2 = '1107';
var k2 = 1;
var res2 = '107';

console.log(removeKdigits(num2, k2));
console.log(removeKdigits(num2, k2) === res2);
```

## Using whiteboard:
1. 想清楚再下笔，通常要在想清楚时间复杂度之后再开始写，确保思路完全正确

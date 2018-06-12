# LeetCode
加油！算法学习之路
#### 167. 两数之和 II - 输入有序数组（简单）
```
var twoSum = function(numbers, target) {
     let array=[];
    for(let i=0;i<numbers.length;i++)
        {
            for(let j=i+1;j<numbers.length;j++)
                {
                    if(numbers[i]+numbers[j]==target)
                        {
                            array[0]=i+1;
                            array[1]=j+1;
                            return array;
                        }
                }
        }
};
```

# LeetCode
加油！算法学习之路
## 目录
* [1.两数之和](#167)
* [167. 两数之和 II - 输入有序数组](#167)
* [215.数组中的第K个最大元素](#414)
* [414. 第三大的数](#414)
* [766. 托普利茨矩阵](#766)
#### <a id="167">167. 两数之和 II - 输入有序数组（简单）</a>
给定一个已按照升序排列 的有序数组，找到两个数使得它们相加之和等于目标数。

函数应该返回这两个下标值 index1 和 index2，其中 index1 必须小于 index2。
```javascript
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
类同1.两数之和

#### <a id="766">766. 托普利茨矩阵(简单）</a>
如果一个矩阵的每一方向由左上到右下的对角线上具有相同元素，那么这个矩阵是托普利茨矩阵。

给定一个 M x N 的矩阵，当且仅当它是托普利茨矩阵时返回 True。
```javascript
var isToeplitzMatrix = function(matrix) {
    if(matrix.length==1||matrix[0].length==1)
        {
            return true;
        }
    else{
    for(let i=0;i<matrix.length-1;i++)
        {
            for(let j=0;j<matrix[i].length-1;j++)
                {
                    if(matrix[i][j]==matrix[i+1][j+1])
                        {
                            if(i==matrix.length-2&&j==matrix[0].length-2)
                                {
                                    return true;
                                }
                        }
                    else
                        return false;
                }   
        }
    }
};
```

#### <a id="414">414. 第三大的数(简单）</a>
给定一个非空数组，返回此数组中第三大的数。如果不存在，则返回数组中最大的数。要求算法时间复杂度必须是O(n)。

```javascript
var thirdMax = function(nums) {
    let hash={};
    let array=[];
    let item;
    for(let i=0;i<nums.length;i++)
        {
           if(!hash[nums[i]])
               {
               hash[nums[i]]=true;
               array.push(nums[i]);
               }
        }//剔除相同的数
    for(let j=0;j<array.length;j++)
        {
            for(let h=j+1;h<array.length;h++)
                {
                    if(array[j]<array[h])
                        {
                            item=array[j];
                            array[j]=array[h];
                            array[h]=item;                            
                        }
                }
        }//利用冒泡法进行排序
     if(array.length>2)
        return array[2];
    else
        return array[0];
    
};
```
类同215.数组中的第K个最大元素


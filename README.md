# LeetCode
加油！算法学习之路
## 目录
* [1.两数之和](#167)
* [35. 搜索插入位置](#35)
* [167. 两数之和 II - 输入有序数组](#167)
* [215.数组中的第K个最大元素](#414)
* [414. 第三大的数](#414)
* [581. 最短无序连续子数组](#581)
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

#### <a id="581">581. 最短无序连续子数组(简单）</a>
给定一个整数数组，你需要寻找一个连续的子数组，如果对这个子数组进行升序排序，那么整个数组都会变为升序排序。

你找到的子数组应是最短的，请输出它的长度。
```javascript
var findUnsortedSubarray = function(nums) {
    let item;
    let [...array]=nums;//ES6，深拷贝，浅拷贝的话，array一变化，nums也变化了
    let my_arr=[];
    let arr=[];
    for(let i=0;i<array.length;i++)
        {
            for(let j=i+1;j<array.length;j++)
                {
                    if(array[i]>array[j])
                        {
                            item=array[i];
                            array[i]=array[j];
                            array[j]=item;
                        }
                }
        }
    for(let h=0;h<array.length;h++)
        {
            if(array[h]==nums[h])
                {
                    my_arr.push(h);
                }
            else{
                break;
            }
        }
    for(let g=array.length-1;g>=0;g--)
        {
            if(array[g]==nums[g])
                {
                   arr.push(g);
                }
            else{
              break;
            }
        }
    if(nums.length-arr.length-my_arr.length<0)
        {
            return 0;
        }
    else{
    return (nums.length-arr.length-my_arr.length);
    }
        
};
```
先将其排序，再比较这两个数组两端哪些一样。过程较为复杂，等待改进。

#### <a id="35">35. 搜索插入位置(简单)</a>
给定一个排序数组和一个目标值，在数组中找到目标值，并返回其索引。如果目标值不存在于数组中，返回它将会被按顺序插入的位置。

你可以假设数组中无重复元素。
```javascript
var searchInsert = function(nums, target) {
    for(let i=0;i<nums.length;i++)
        {
            if(nums[i]==target)
                return i;
            else if(i==nums.length-1){
                for(let j=0;j<nums.length;j++)
                    {
                        if(nums[0]>target)
                            {
                                return 0;
                            }
                        else if(nums[nums.length-1]<target)
                            {
                                return nums.length;
                            }
                        else if(target<nums[j+1]&&target>nums[j])
                            {
                                return j+1;
                            }
                    }
            }
        }
};
```


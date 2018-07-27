# LeetCode
加油！算法学习之路
## 目录
* [1.两数之和](#167)
* [26. 删除排序数组中的重复项](#26)
* [27. 移除元素](#27)
* [35. 搜索插入位置](#35)
* [53. 最大子序和](#53)
* [66. 加一](#66)
* [88. 合并两个有序数组](#88)
* [118. 杨辉三角](#119)
* [119. 杨辉三角 II](#119)
* [167. 两数之和 II - 输入有序数组](#167)
* [189. 旋转数组](#189)
* [215.数组中的第K个最大元素](#414)
* [268. 缺失数字](#268)
* [283.移动零](#283)
* [414. 第三大的数](#414)
* [485. 最大连续1的个数](#485)
* [566. 重塑矩阵](#566)
* [581. 最短无序连续子数组](#581)
* [628. 三个数的最大乘积](#628)
* [643. 子数组最大平均数 I](#643)
* [665. 非递减数列](#665)
* [746. 使用最小花费爬楼梯](#746)
* [766. 托普利茨矩阵](#766)
* [830. 较大分组的位置](#830)
* [849. 到最近的人的最大距离](#849)
* [867. 转置矩阵](#867)
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
改进方法：
```javascript
var twoSum = function(nums, target) {
   let hash={};
   let pair,num;
   for(let i=0;i<nums.length;i++)
       {
          num=nums[i];
           pair=target-num;
           if(hash.hasOwnProperty(pair))//判断hash对象中是否有pair属性
               {
                   return [hash[pair],i]
               }
           hash[num]=i;
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
改进方法：
```javascript
var findKthLargest = function(nums, k) {
    function sortNums(a,b)
    {
        return b-a;//利用sort方法，sort内部参数必须是函数，b-a表示从大到小排序，当b-a大于0时交换顺序，以此实现排序
    }
    nums.sort(sortNums)
    return nums[k-1];
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
<br>改进方法：
```javascript
var findUnsortedSubarray = function(nums) {
     let n=nums.length;
    let min=nums[n-1];
    let max=nums[0];
    let start=-1;
    let end=-2;
    for(let i=0;i<n;i++)
        {
           max=Math.max(nums[i],max)
           min=Math.min(nums[n-i-1],min)
           if(nums[i]<max)
               end=i
            if(nums[n-i-1]>min)
                start=n-i-1
           
        }
    return end-start+1
};
```
[拷贝](https://www.cnblogs.com/Chen-XiaoJun/p/6217373.html)
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

#### <a id="189">189. 旋转数组（简单）</a>
给定一个数组，将数组中的元素向右移动 k 个位置，其中 k 是非负数。
```javascript
var rotate = function(nums, k) {
    let items;
    for(let j=0;j<k;j++)
        {
       for(let i=0;i<nums.length-1;i++)
          {
            items=nums[i+1];
            nums[i+1]=nums[0];
            nums[0]=items;
          }
        }
};
```
比较简单，主要是通过nums数组的第一个元素和其他的依次进行交换，总共进行k次。
<br>改进方法：
```javascript
var rotate = function(nums, k) {
    let len=nums.length;
    let arr=nums.splice(len-k,k);
    nums.unshift(...ary)//...将数组转化成用逗号隔开的参数，如[1,2,3,4,5,6,7] 和 k = 3，结果为[5,6,7,1,2,3,4]，不加...，结果是[[5,6,7],1,2,3,4]
    };
```

#### <a id="566">566. 重塑矩阵（简单）</a>
在MATLAB中，有一个非常有用的函数 reshape，它可以将一个矩阵重塑为另一个大小不同的新矩阵，但保留其原始数据。

给出一个由二维数组表示的矩阵，以及两个正整数r和c，分别表示想要的重构的矩阵的行数和列数。

重构后的矩阵需要将原始矩阵的所有元素以相同的行遍历顺序填充。

如果具有给定参数的reshape操作是可行且合理的，则输出新的重塑矩阵；否则，输出原始矩阵。

（1）先将二维数组映射为一维数组
<br>我一开始的想法是利用数组循环得出：
```javascript
 for(let i=0;i<nums.length;i++)
        {
            for(let j=0;j<nums[i].length;j++)
                {
                    array.push(nums[i][j]);
                }
        }
```
后来百度得到更简单的方法：
```javacript
  array.concat.apply(array,nums);
```
这个里面运用了concat和apply的方法，apply将nums数组解析为一个个参数，array调用了concat方法，concat将array和nums合并为一个参数。
<br>[apply相关知识参考链接](https://blog.csdn.net/business122/article/details/8000676)

<br>(2)找到相关的关系。arr[i][j]=array[i+c*j]
```javascript
var matrixReshape = function(nums, r, c) {
    let array=[];
    let arr=new Array();
    array=[].concat.apply([],nums); 
    if(r*c==array.length)
        {
            for(let i=0;i<r;i++)
                {
                    arr[i]=new Array();
                    for(let j=0;j<c;j++)
                        {
                           arr[i][j]=array[j+i*c];
                        }
                }
            return arr;
        }   
    else{
        return nums;
    }
};
```
<br>[二维数组定义相关参考链接](http://blog.sina.com.cn/s/blog_e084ba2b0102wk57.html)

#### <a id="27">27. 移除元素（简单）</a>
给定一个数组 nums 和一个值 val，你需要原地移除所有数值等于 val 的元素，返回移除后数组的新长度。

不要使用额外的数组空间，你必须在原地修改输入数组并在使用 O(1) 额外空间的条件下完成。

元素的顺序可以改变。你不需要考虑数组中超出新长度后面的元素。
```javascript
var removeElement = function(nums, val) {
     for(let i=0;i<nums.length;i++)
         {
             if(nums[i]==val)
                 {
                      nums.splice(i,1);
                      i--;//因为nums被移除了一位，所以i要减一
                 }
         }
};
```
学会用原型写程序，这样可以在项目中可以减少很多代码量
```javascript
var removeElement = function(nums, val) {
     nums.remove(val);
};

Array.prototype.remove=function(val){
    let arr=[];
    for(let i=0;i<this.length;i++)
        {
          if(this[i]==val)
              arr.push(i);
        }
    for(let i=0;i<arr.length;i++)
    {
        this.splice(arr[i]-i,1);//注意每删掉一个之后的变化
    }
}
```

#### <a id="26">26. 删除排序数组中的重复项</a>
给定一个排序数组，你需要在原地删除重复出现的元素，使得每个元素只出现一次，返回移除后数组的新长度。

不要使用额外的数组空间，你必须在原地修改输入数组并在使用 O(1) 额外空间的条件下完成。
```javascript
var removeDuplicates = function(nums) {
    nums.remove();
};
Array.prototype.remove=function()
{
    let hash={};
    for(let i=0;i<this.length;i++)
        {
            if(!hash[this[i]])
                {
                    hash[this[i]]=true;
                }
            else{
                this.splice(i,1);
                i--;
            }
        }
}
```

#### <a id="830">830. 较大分组的位置</a>
在一个由小写字母构成的字符串 S 中，包含由一些连续的相同字符所构成的分组。

例如，在字符串 S = "abbxxxxzyy" 中，就含有 "a", "bb", "xxxx", "z" 和 "yy" 这样的一些分组。

我们称所有包含大于或等于三个连续字符的分组为较大分组。找到每一个较大分组的起始和终止位置。

最终结果按照字典顺序输出。
```javascript
var largeGroupPositions = function(S) {
    let arr=[];
    for(let i=0;i<S.length;i++)
        {
            for(let j=0;j<S.length;j++)
                {
                    if(S[i]==S[i+j]&&S[i]==S[i+1]&&S[i]==S[i+2])
                        {
                            if(S[i]!=S[i+j+1])
                                {
                                    if(j>1)
                                        {
                                              arr.push([i,i+j]);
                                              i=i+j;
                                        }
                                }
                        }
                }
        }
    return arr;
};
```
这种方法的用时达到300多ms，较为繁琐，改进方法
```javascript
    var largeGroupPositions = function(S) {
    let outPut=[]
    let reg=/([a-z])\1\1+/g//\1代表与第一个小括号内匹配的字符相同
    let out=reg.exec(S)//exec返回的是一个数组，所以下方要用out[0]，通过反复调用exec来历遍字符串中所有的匹配文本
    while(out)
        {
            outPut.push([out.index,out.index+out[0].length-1])
            out=reg.exec(S)
        }
    return outPut
};
```
#### <a id="66">66. 加一</a>
给定一个非负整数组成的非空数组，在该数的基础上加一，返回一个新的数组。

最高位数字存放在数组的首位， 数组中每个元素只存储一个数字。

你可以假设除了整数 0 之外，这个整数不会以零开头。
<br>我开始是这样做的
```javascript
var plusOne = function(digits) {
    let num=digits.join("");
    let arr=[];
    num=Number(num);
    num=num+1;
    let string=num.toString();
    for(let i=0;i<string.length;i++)
        {
                    arr.unshift(num%10);
                    num=Math.floor(num/10);
        }
    return arr;
};
```
将其转换成数字，加一后再利用除法转换成数组，后发现使用这种方法计算超过其范围的数字就会出错，后改变方法
```javascript
var plusOne = function(digits) {
    for(let i=digits.length-1;i>=0;i--)
        {
             if(digits[i]!=9)//判断是不是9，不是就直接加一后返回该数组
                 {
                     digits[i]++;
                     return digits;
                 }
            else{
                digits[i]=0;
            }
        }
    digits.unshift(1);//如果全部为0，则循环完成，继续执行接下来的打码，利用unshift将1放在数组最前面，返回该数组
    return digits;
};
```
#### <a id="119">119. 杨辉三角 II</a>
给定一个非负索引 k，其中 k ≤ 33，返回杨辉三角的第 k 行。在杨辉三角中，每个数是它左上方和右上方的数的和。
```javascript
var getRow = function(rowIndex) {
    let array=[1,1]
    let arr=[1,1]
    if(rowIndex==0)
        return [1]
    else{
    for(let i=1;i<rowIndex;i++)
        {
            for(let j=array.length-1;j>0;j--)
                {
                       arr.splice(1,0,array[j]+array[j-1])//历遍，使上一行的数字相加等于这一行
                }
            array=arr;
            arr=[1,1];
        }
    return array;
    }
};
```
类同118.杨辉三角

#### <a id="665">665. 非递减数列</a>
给定一个长度为 n 的整数数组，你的任务是判断在最多改变 1 个元素的情况下，该数组能否变成一个非递减数列。

我们是这样定义一个非递减数列的： 对于数组中所有的 i (1 <= i < n)，满足 array[i] <= array[i + 1]。
```javascript
var checkPossibility = function(nums) {
    let len=nums.length;
    if(nums[0]>nums[1])
        {
            nums[0]=nums[1];
        }
    else if(nums[len-1]<nums[len-2])
        {
            nums[len-1]= nums[len-2];
        }
    else{
       let i=1;
       while(nums[i]<=nums[i+1])
           i++;
        if(nums[i]>nums[i+2])
            nums[i]=nums[i+1];
        else
          nums[i+1]=nums[i];
    }
    console.log(nums);
    let [...array]=nums;
    array.sort(function(a,b)
              {
        return a-b;
    })
    for(let j=0;j<len;j++)
        {
            if(array[j]!=nums[j])
                return false;
        }
    return true;
}//分为两头和中间的无序进行计算，同时又将中间的无序分为两种进行计算
```
改进方法：
```javascript
var checkPossibility = function(nums) {
    let count=0;
    if(nums[0]>nums[1])
        {
            nums[0]=nums[1];
            count++;
        }
  for(let i=2;i<nums.length&&count<2;i++)
      {
          if(nums[i-1]>nums[i])
              {
                  if(nums[i]>nums[i-2])
                      {
                          nums[i-1]=nums[i-2];
                      }
                  else{
                      nums[i]=nums[i-1];
                  }
                  count++;
              }
         
      }
     return count<2;        //利用count来判断为真还是为假，更简洁。
}
```
#### <a id="283">283. 移动零</a>
给定一个数组 nums，编写一个函数将所有 0 移动到数组的末尾，同时保持非零元素的相对顺序。
```javascript
var moveZeroes = function(nums) {
    let count=0;
    for(let i=0;i<nums.length;i++)
        {
            if(nums[i]==0)
                {
                    nums.splice(i,1);
                    i--;
                    count++;
                }
        }
    for(let j=0;j<count;j++)
        {
            nums.push(0);
        }
};
```
如果是倒序进行计算，那么就会减少时间复杂度。

#### <a id="268">268. 缺失数字</a>
给定一个包含 0, 1, 2, ..., n 中 n 个数的序列，找出 0 .. n 中没有出现在序列中的那个数。
```javascript
var missingNumber = function(nums) {
    if(nums.length==1)
        {
            if(nums[0]==0)
                return 1;
        }
   nums.sort(function(a,b)
            {
       return a-b;
   })
     if(nums[0]!=0)
        return 0;
   for(let i=0;i<nums.length-1;i++)
       {
           if(nums[i+1]!=(nums[i]+1))
               {
                   return nums[i]+1;
               }
       }
    return nums[nums.length-1]+1;
};//通过比较排序后的数组是否依次加一来判断
```
改进方法
```javascript
var missingNumber = function(nums) {
    let len=nums.length;
    let sum=(len+0)*(len+1)/2;
    for(let i=0;i<nums.length;i++)
        {
            sum=sum-nums[i];
        }
    return sum;
}//求出0-n的和，再与nums中的数相减就可以得出相应的结果
```
#### <a id="746">746. 使用最小花费爬楼梯</a>
数组的每个索引做为一个阶梯，第 i个阶梯对应着一个非负数的体力花费值 cost[i](索引从0开始)。

每当你爬上一个阶梯你都要花费对应的体力花费值，然后你可以选择继续爬一个阶梯或者爬两个阶梯。

您需要找到达到楼层顶部的最低花费。在开始时，你可以选择从索引为 0 或 1 的元素作为初始阶梯。
```javascript
var minCostClimbingStairs = function(cost) {
    let arr=[];
    arr[0]=0;
    arr[1]=0;
    for(let i=2;i<cost.length+1;i++)
        {
            arr[i]=Math.min(arr[i-1]+cost[i-1],arr[i-2]+cost[i-2])
        }
    return arr[cost.length];//动态规划，找到关键的状态方程：arr[i]=Math.min(arr[i-1]+cost[i-1],arr[i-2]+cost[i-2])，使arr里面存放的都是最小的答案
};
```
[动态规划](https://blog.csdn.net/baidu_28312631/article/details/47418773)

#### <a id="88">88. 合并两个有序数组</a>
给定两个有序整数数组 nums1 和 nums2，将 nums2 合并到 nums1 中，使得 num1 成为一个有序数组。
```javascript
var merge = function(nums1, m, nums2, n) {
    nums1.splice(m,nums1.length-m);
    nums2.splice(n,nums2.length-n);
    nums1.push.apply(nums1,nums2);//利用apply将nums2分解为一个一个的参数，在调用push函数，添加到nums1后面
    nums1.sort(function(a,b){
return a-b;
    })
};
```
#### <a id="53">53. 最大子序和</a>
给定一个整数数组 nums ，找到一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和。
```javascript
var maxSubArray = function(nums) {
    let sum=nums[0];
    let maxNum=nums[0];
    for(let i=1;i<nums.length;i++)
        {
            if(sum>0)
                {
                    sum=sum+nums[i];
                }
            else
                {
                    sum=nums[i];
                }
            if(maxNum<sum){
                maxNum=sum;
            }
        }
    return maxNum;
};
```
#### <a id="628">628. 三个数的最大乘积</a>
给定一个整型数组，在数组中找出由三个数组成的最大乘积，并输出这个乘积。

```javascript
var maximumProduct = function(nums) {
   nums.sort(function(a,b){
       return b-a;
   });
   let len=nums.length;
   let max_value1=nums[0]*nums[1]*nums[2];
   let max_value2=nums[0]*nums[len-1]*nums[len-2];
   return Math.max(max_value1,max_value2);
};
```
将sort用程序写出来会减少执行用时。

#### <a id="867">867. 转置矩阵</a>
给定一个矩阵 A， 返回 A 的转置矩阵。

矩阵的转置是指将矩阵的主对角线翻转，交换矩阵的行索引与列索引。
```javascript
/**
 * @param {number[][]} A
 * @return {number[][]}
 */
var transpose = function(A) {
    let B=[];
    let C=[];
    for(let j=0;j<A[0].length;j++)
    {
        for(let i=0;i<A.length;i++)
            {
             B.push(A[i][j]);
            }
            C.push(B);
            B=[];
    }
    return C;      
};

```
#### <a id="643">643. 子数组最大平均数 I</a>
给定 n 个整数，找出平均数最大且长度为 k 的连续子数组，并输出该最大平均数。
```javascript
var findMaxAverage = function(nums, k) {
    let maxValue=0;
    let average=-Infinity;
    for(let i=0;i<nums.length;i++)
    {
        for(let j=i;j<k+i;j++)
            {
                maxValue+=nums[j];
               
            }
        average=Math.max(maxValue/k,average);
        maxValue=0;
        if(i==(nums.length-k)){
            return average;
        }
    }
};
```
时间太长，改进
```javascript
var findMaxAverage = function(nums, k) {
    if(nums.length==1)
        return nums[0];
    let curValue=0;
    for(let i=0;i<k-1;i++)
        {
            curValue+=nums[i];
        }
    if(k==nums.length)
        return (curValue+nums[k-1])/k;
    let mathValue=-Infinity;
    for(let i=k-1;i<nums.length;i++)
        {
            curValue+=nums[i];
            if((i-k)>-1)
                curValue-=nums[i-k]
            
            mathValue=Math.max(mathValue,curValue)
        }
    return mathValue/k;
};
```
利用循环，先加后面的再减去前面的，使其在一个循环内完成，减少时间复杂度

#### <a id="849">849. 到最近的人的最大距离</a>
在一排座位（ seats）中，1 代表有人坐在座位上，0 代表座位上是空的。

至少有一个空座位，且至少有一人坐在座位上。

亚历克斯希望坐在一个能够使他与离他最近的人之间的距离达到最大化的座位上。

返回他到离他最近的人的最大距离。
```javascript
var maxDistToClosest = function(seats) {
    let max=0;
    let d=0;
    let n=0;
    let left_value;
    for(let i=0;i<seats.length;i++)
        {
             if(seats[i]==1)
                 {
                      d=Math.max(d,i-max)
                      max=i;
                      n++;
                     console.log(i,n)
                 }
            if(n==1)
                {
                     left_value=max;
                }
        }
    let right_value=seats.length-1-max;
    let res=Math.max(left_value,d/2,right_value);
    if(res==right_value)
        return right_value;

    if(res==left_value)
        return left_value;
    return Math.floor(d/2);
};//通过比较前后以及中间的间隔计算
```
改进方法：利用平均数简化算法
```javascript
var maxDistToClosest = function(seats) {
    let index=[];
    let len=seats.length;
    let max=0;
    let avg;
    let min;
    if(len==2)
        return 1;
    for(let i=0;i<len;i++)
        {
             if(seats[i]==1)
                 index.push(i);
        }
    len=index.length;
    for(let i=0;i<len-1;i++)
        {
            avg=parseInt((index[i]+index[i+1])/2);
            min=Math.min(avg-index[i],index[i+1]-avg);
            if(max<min)
                max=min;
        }
    if(seats[0]==0&&max<index[0])
        max=index[0];
    if(seats[seats.length-1]==0&&max<seats.length-index[len-1]-1)
        max=seats.length-index[len-1]-1
    return max;
};
```
#### <a id="485">485. 最大连续1的个数</a>
给定一个二进制数组， 计算其中最大连续1的个数。
```javascript
var findMaxConsecutiveOnes = function(nums) {
    let n=0;
    let array=[];
    let min=0;
    let res=0;
    for(let i=0;i<nums.length;i++)
     {
         if(nums[i]==1)
             {
                 n++;
                 res=Math.max(res,n);
             }
         else
             {
                 n=0;
             }
     }
    return res;
};
```

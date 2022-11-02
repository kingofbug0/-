# LeetCode

## leetcode第一题两数之和：

```c++
#include <stdio.h>
#include <stdlib.h>
int* twoSum(int* nums, int numsSize, int target, int* returnSize)
{
	int i, j;
	{
		int* answer = NULL;//声明指针answer先指向一个NULL；
		int i,j;
		for (i = 0; i < numsSize; i++)//numsSize是代表这个数组的大小，因为在数组中函数是连续存放所以用i和j来寻找储存的数
			for (j = i + 1; j < numsSize; j++)
			{
				if ((nums[i] + nums[j]) == target)//判断是否相同
				{
					answer = (int*)malloc(2 * sizeof(int));//获取地址 解指针；
					answer[0] = i;//用首地址存放找到的第一个位置
					answer[1] = j;//存放第二个找到的数字
					*returnSize = 2;//因为numsSize只有两个数i和j所以这个位置的*returnSize赋值2
					return answer;//得到的结果地址给到answer
				}
			}
		return answer;
	}
}

int main()
{
	int target, nums[100], * answer, i, returnSize;
	printf("请输入答案:");
	scanf_s("%d", &target);
	printf("请输入数组数字:");
	for (i = 0; i < 5; i++)
	{
		scanf_s("%d", &nums[i]);
	}
	answer = twoSum(nums,5, target, &returnSize);//调用自定义函数，5代表数组的大小；
	for (i = 0; i < returnSize; i++)//输出两次
	{
		printf("%d", *answer);//输出*answer地址所存放的值
		answer++;//得到存放下一个地址的值，因为是连续存储的
	}
	return 0;
}
```



## leetcode  数组 

- 删除排序数组中的重复项
- 输入：nums = [1,1,2]
- 输出：2, nums = [1,2,_]
- 解释：函数应该返回新的长度 2 ，并且原数组 nums 的前两个元素被修改为 1, 2 。不需要考虑数组中超出新长度后面的元素。

```java
class Solution {
   public int removeDuplicates(int[] nums)   
   {
        if (nums == null || nums.length == 0)  //处理边界条件 如果数组为空直接返回
         {
            return 0;
        }
      int count=1;//计数器
     for(int left=0,right=1;right<nums.length;right++)//利用双指针遍历
     {
         if(nums[left]!=nums[right])//如果左边的数不等于右边的数
         {
             nums[++left]=nums[right];//左边的数组和右边的数组指向同一块地址 然后用右边的数组去覆盖住左边的数组的值 删掉重复项
             ++count;//计数器加1
         }
     }
        

        return count;//返回计数器的长度

   }
}
```

## 买卖股票的最佳时机 II

- 输入：prices = [7,1,5,3,6,4]
- 输出：7
- 解释：在第 2 天（股票价格 = 1）的时候买入，在第 3 天（股票价格 = 5）的时候卖出, 这笔交易所能获得利润 = 5 - 1 = 4 。
- ​     随后，在第 4 天（股票价格 = 3）的时候买入，在第 5 天（股票价格 = 6）的时候卖出, 这笔交易所能获得利润 = 6 - 3 = 3 。
- ​     总利润为 4 + 3 = 7 。

```java
class Solution {
    public int maxProfit(int[] prices) {
        int sum=0;
      for(int left=0,right=1;right<prices.length;left++,right++)//利用双指针遍历数组
      {
          

          if(prices[left]<prices[right])//如果左边数组的价格小于右边数组的价格
          {
            sum=sum+ prices[right]-prices[left];//用右边数组的价格减去左边数组的价格得到盈利，用sum算这个数组中有几个这样有差值的数字之和
          }
         
      }
      return sum;//返回到总和 及得到最大的盈利利润
    }

}
```

## 旋转数组

- 输入: nums = [1,2,3,4,5,6,7], k = 3
- 输出: [5,6,7,1,2,3,4]
- 解释:
- 向右轮转 1 步: [7,1,2,3,4,5,6]
- 向右轮转 2 步: [6,7,1,2,3,4,5]  
- 向右轮转 3 步: [5,6,7,1,2,3,4]
- //该题目意思大概就是 数组中每个数往右移动的距离，若是最后一个数组 则是往第一个数组方向移动

```java
class Solution {
    public void rotate(int[] nums, int k) 
    {
      int []Newnums=new int[nums.length];//添加一个新数组去接受这个需要转动的数组
      for(int i=0;i<nums.length;i++)//遍历一遍
      {
          Newnums[i]=nums[i];//将新数组赋值
      }
      for(int i=0;i<nums.length;i++)//遍历 开始进行移动
      {
          nums[(i+k)%nums.length]=Newnums[i];//K代表的是需要移动的距离 及0号位->k号位 1号位->1+k号位，若数组在后面 比如最后一个为 nums[6+3] 它应该移动至nums[2]号位  用nums[6+3==9%7==2]就是变到了nums[2]的位置
      }
    }
}
```

## 存在重复元素

- 输入：nums = [1,2,3,1]
- 输出：true   //意思就是查询是否有重复的数组

```java
class Solution {
    public boolean containsDuplicate(int[] nums) 
    {
      Arrays.sort(nums);//用JAVA自带的Arrays.sort(nums)排序 从小到大
      for(int left=0;left<nums.length-1;left++)//遍历数组
      {
          if(nums[left]==nums[left+1])//如果两个相邻的数组有一样的数字
          {
              return true;//就返回true
          }
      }
      return false;//若遍历完后没有这样的数字 就返回false
    }
}
```

## 只出现一次的数字

- 输入: [4,1,2,1,2]
- 输出: 4 

```java
class Solution {
    public int singleNumber(int[] nums) 
    {
    Arrays.sort(nums);//先对数组进行排序
    if(nums.length==1)//处理边界 如果这个数组仅有一个数字 直接返回该数字
    {
        return nums[0];
    }
       if(nums[0]!=nums[1])//处理第一个数字就是单独出现的数字的时候，直接返回第一个数字
    {
        return nums[0];
    }
    if(nums[nums.length-1]!=nums[nums.length-2])//这个是处理最后一个数字就是单独出现的时候后，直接返回最后一个数字
    {
        return nums[nums.length-1];
    }
    for(int i=1;i<nums.length-1;i++)//开始处理3个及以上的数组 遍历
    {
        if(nums[i]!=nums[i+1]&&nums[i]!=nums[i-1])//比如[1,1,2] 中间这个1与他的前后比较 如果与他的前后均不一样就返回这个数
        {
           return nums[i];
        }
    }
    return 0;
    }
}	
```

## 两个数组的交集 II

- 输入：nums1 = [1,2,2,1], nums2 = [2,2]
- 输出：[2,2]//也不完全是交集 就是两个数组中出现相同的元素

```java
class Solution {
    public int[] intersect(int[] nums1, int[] nums2) 
    {
            Arrays.sort(nums1);
            Arrays.sort(nums2);//对这两个数组进行排序
            if(nums2.length< nums1.length)//处理这两个数组的长度  始终保持第一个数组的长度小于第二个数组的长度
            {
                int temp[]=nums2;
                nums2=nums1;
                nums1=temp;
            }
            int index=0;//添加计数器
            int up=0;//添加双指针
            int down=0;
            while(up<nums1.length&&down<nums2.length)//循环遍历
            {
              if(nums1[up]<nums2[down])//因为是两个数组 我把他看成上下两个 当上面那个数组指向的值大小 小于 下面的值时，上面的指针往后指
              {
                  up++;
              }
              else if(nums1[up]>nums2[down])//当上面那个数组指向的值大小 大于 下面的值时，下面的指针往后指
               {
                   down++;
               }
                else
                {
                    nums2[index]=nums1[up];//用大的那个数组来接受相同的数字 用nums当做一个容器来接受相同的数字 从0开始
                    index++;//记完后计数器往后走
                    up++;//上下同时向后走一格
                    down++;
                }
            }
          int []nums3=new int[index];//添加新数组 用计数器的大小来规定新数组的大小
            for(int j=0;j<index;j++)//遍历长度为index 的大小
            {
                nums3[j]=nums2[j];//用nums2记录的数组来写入到新数组nums3中去
            }
            return nums3;//最后的输出用新数组nums3来输出 此时记录的全是重复的数字
    }
}
```

## 加一

- 输入:digits = [1,2,3]
- 输出：[1,2,4]
  解释：输入数组表示数字 123。//即尾数加1

```java
class Solution {
    public int[] plusOne(int[] digits)
    {
      for(int i=digits.length-1;i>=0;i--)//遍历数组 从尾部开始  这个循环中处理的是不全为9的情况 如2499 9->0 4->在！=9时完成 9->0在==0时完成
      {
          if(digits[i]!=9)//如果最后一个数字不为9 则直接尾数加1
          {
           digits[i]=digits[i]+1;//尾数+1
           return digits;//加完后直接返回加完后的数组
          }
          else
          {
              digits[i]=0;//如果尾数为9的话，直接变成0 因为 289->290
          }
      }
      int arr[]=new int[digits.length+1];//创建一个新数组 因为当尾数为9且该数组中全为9时会面临扩大数组的问题如 9->1，0
      arr[0]=1;//数组中全为9 如999->1000第一位直接变成了1 而后面的数字全在上面的循环中变成了0
       return arr;//返回该数组
    }
}
```

## 移动零

- 输入: nums = [0,1,0,3,12]
- 输出: [1,3,12,0,0]//把0移动到最后去

```java
class Solution {
    public void moveZeroes(int[] nums)
     {
         if(nums.length==1)//处理只有一个数字的时候 直接return
         {
             return ;
         }
      int j=0;//添加双指针
         for(int i=0;i<nums.length;i++)//遍历数组
         {
             if(nums[i]!=0)//如果i指针指向的值不为0的话 与j指针的值进行交换 并且j指针开始指向j的下一个
             {
                 int temp=nums[i];
                 nums[i]=nums[j];
                 nums[j]=temp;
                 j++;
             }
         }
    }
}
```

## 两数之和

- 输入：nums = [2,7,11,15], target = 9
  输出：[0,1]
  解释：因为 nums[0] + nums[1] == 9 ，返回 [0, 1] 。

```java
class Solution {
    public int[] twoSum(int[] nums, int target)
    { 
       int i,j;
       i=0;
       j=nums.length-1;
      for(int ii=0;ii<nums.length;ii++)
        {
            if(nums[j]>target)
            {
                j--;
            }
            else if(nums[j]+nums[i]>target)
            {
                j--;
            }
            else if(nums[j]+nums[i]<target)
            {
                i++;
            }
           else if(nums[j]+nums[i]==target)
           {
                return new int []{i,j};
           }
        }
        return new int []{i,j};
    }
}
```

## 反转字符串

- 输入：s = ["h","e","l","l","o"]
- 输出：["o","l","l","e","h"]

```java
class Solution 
{
    public void reverseString(char[] s) 
    {
            int left=s.length-1;
            int right=0;
            for(int i=0;i<s.length/2;i++)
            {
                char temp;
                temp=s[left];
                s[left]=s[right];
                s[right]=temp;
                left--;
                right++;
            }
    }
}
```

## 整数反转

- 输入：x = 123
- 输出：321

```java
class Solution 
    {
       public int reverse(int x)
       {
           long res=0;//用一个大的数来接受
           while(x!=0)
           {
               int a=x%10;//取模结果
               long nR=res*10+a;//添加一个新结果来接受这个
               res=nR;
               if(res>Integer.MAX_VALUE||res<Integer.MIN_VALUE)//判断这个数是否大于了最大值与小于了最小值
               {
                   return 0;
               }
               x=x/10;
           }
           return (int)res;//把long类型的值转换为int类型输出
       }
    }
```

## 字符串中的第一个唯一字符

- 给定一个字符串 s ，找到 它的第一个不重复的字符，并返回它的索引 。如果不存在，则返回 -1 。
- 示例 1：
- 输入: s = "leetcode"
  输出: 0

#### indexof（）的用法

用来查找字符串中第一次出现这个字符的索引

```java
class Solution
       {
           public int firstUniqChar(String s)
           {
               for(int i=0;i<s.length();i++)
               {
                   if(s.indexOf(s.charAt(i))==s.lastIndexOf(s.charAt(i)))//这个方法就是 用JAVA的API 先找第一次出现这个字符的位置 indexof再用 lastIndexof找到最后出现的位置 如果这两个位置相等 就表示只出现了一次 返回找到这个值的位置即可
                   {
                       return i;
                   }
               }
               return -1;//没找到就返回-1
           }
       }
```

## 有效的字母异位词

- 给定两个字符串 s 和 t ，编写一个函数来判断 t 是否是 s 的字母异位词。
- 注意：若 s 和 t 中每个字符出现的次数都相同，则称 s 和 t 互为字母异位词。




```java
class Solution
    {
        public boolean isAnagram(String s, String t)
        {
            if(s.length()!=t.length())//长度不同就之间返回false
            {
                return false;
            }

            char []c1=s.toCharArray();//用char数组来接受他
            char []c2=s.toCharArray();
            Arrays.sort(c1);//对其进行排序
            Arrays.sort(c2);
            return Arrays.equals(c1,c2);//排序后直接用Arrays的比较函数equals进行比较
        }
    }
```

## 洛谷 YODA碰撞 

当两个整数碰撞时会发生什么？先将数位较少的数前不断添加前导 00 直到和数位较高的数的数位数量相同为止。然后，从两个数的最低位开始，每次将两个数的对应数位进行比较，并删去较小的那个数位（如果这两个数位相等则**不执行任何操作**），不断向高数位执行上述操作，直到最高位为止。此时，将这两个数中没有删去的数位按顺序依次拼接，可以得到两个新数。

例如，对于 456328 和 284315这两个数，这两个的碰撞过程如下所示：

|  4   |  5   |  6   |  3   |  2   |  8   |
| :--: | :--: | :--: | :--: | :--: | :--: |
|  2   |  8   |  4   |  3   |  1   |  5   |

不难看出，碰撞之后得到的两个新数为 46328 和 83。

现在给定两个数 n,m*n*,*m*，请求出这两个数进行碰撞之后分别得到的新数。如果某个数在进行碰撞之后，其数位都已经被删空了，则在输出中输出一行字符串 `YODA`。具体见『输出格式』部分。

```java
package Java_Stu;
import java.util.ArrayList;
class LeetCode
{
    public static void main(String[] args)
    {
        BoomNum(456328,284315);
    }
     private static void BoomNum(int n,int m)
    {
        String s1 = Integer.toString(n);
        String s2 = Integer.toString(m);
        ArrayList<Character>arr1=new ArrayList<>();
        ArrayList<Character>arr2=new ArrayList<>();
        int up=s1.length()-1;
        int down=s2.length()-1;
        //添加元素
        while(up>=0)
        {
            arr1.add(s1.charAt(up));
            up--;
        }
        while (down>=0)
        {
            arr2.add(s2.charAt(down));
            down--;
        }
        up=0;
        down=0;

        //比较元素
        while(up<arr1.size()&&down<arr2.size())
        {
            if(arr1.get(up)>arr2.get(down))
            {
                arr2.remove(down);
                up++;

            }
            else if(arr1.get(up)<arr2.get(down))
            {
                arr1.remove(up);
                down++;

            }
            else
            {
                up++;
                down++;
            }
        }
        if(arr1.size()==0)
        {
            System.out.println("YODA");
        }
        else
        {
            for(int i=arr1.size()-1;i>=0;i--)
            {
                Character c1 = arr1.get(i);
                System.out.print(c1);
            }
            System.out.println();
        }
        if(arr2.size()==0)
        {
            System.out.println("YODA");
        }
        else
        {
            for(int i=arr2.size()-1;i>=0;i--)
            {
                Character c2 = arr2.get(i);
                System.out.print(c2);
            }
        }
    }
}


```

## 验证回文串

- 输入: s = "A man, a plan, a canal: Panama"

- 输出：true
- 解释："amanaplanacanalpanama" 是回文串。

```java
class Solution
    {
        public boolean isPalindrome(String s)
        {
            int left=0;
            int right=s.length()-1;
            char c1[]=s.toCharArray();//把字符串转换为字符数组 存储在c1中
            while(left<right)//利用双指针来判断
            {
                while(!Character.isLetterOrDigit(s.charAt(left))&&left<right)//当左边的字符不为数字或字母 并且左边指针小于右边指针时 左边往后指
                {
                    left++;
                }
                while(!Character.isLetterOrDigit(s.charAt(right))&&left<right)//当右边指针所指字符不为数字或字母时 并且左边指针小于右边指针时 右边指针前指
                {
                    right--;
                }
                if(Character.toLowerCase(s.charAt(left))!=Character.toLowerCase(s.charAt(right)))//判断左边的指针不等于右边指针时 返回false 这个toLowerCase方法是将大小写统一 将大写转换为小写
                {
                    return false;
                }
                else//如果相同的话 左右指针接着指向下一位
                {
                    left++;
                    right--;
                }
            }
            return true;//当全部相同时 返回true
        }
    }
```

- isLetter是判断英文
- isDigit是判断数字
- isLetterOrDigit是判断是否为英文或者数字

## 实现 strStr()

输入：haystack = "sadbutsad", needle = "sad"

输出：0

解释："sad" 在下标 0 和 6 处匹配。

第一个匹配项的下标是 0 ，所以返回 0 。

```java
class Solution//这是最简单的方法 直接调用API indexOf作比较 返回第一次出现这个字符串的索引
    {
        public int strStr(String haystack, String needle)
        {
           return haystack.indexOf(needle);
        }
    }

```

```java
class Solution//正常来说
    {
        public int strStr(String haystack, String needle)
        {
            int up=0;
            int down=0;//还是添加上下双指针 上指针指向haystack 下指针指向needle
            int index=0;//添加一个计数器
            if(haystack.length()==needle.length())//当两个字符串长度相同时
            {
                if(haystack.equals(needle))//用equals比较即可
                {
                    return 0;
                }
                return -1;
            }
            while(up<haystack.length()&&down<needle.length())//判断条件
            {
                if(haystack.charAt(up)==needle.charAt(down))//还是将String转换为字符 如果有相同的 就让他们指向下一个
                {
                    down++;
                    up++;
                    index++;
                }
                else//否则的话 上指针回到第一个+1的位置 从第二个字母开始比较 下指针回到初始位置
                {
                    up=up-down+1;
                    down=0;
                    index=0;
                }
                if(index==needle.length())//如果找到了，就是比如 leetcode 和cod c在四号位找到六号位截至 那就返回六号位减去下指针的2 等于4   这里index==needle.length代表的是 当这几个字母长度与计数器的吻合时
                {
                    return up-down;
                }
            }
            return -1;
        }
    }
```

## 最长公共前缀

- 输入：strs = ["flower","flow","flight"]
- 输出："fl"

```java
class Solution
   {
       public String longestCommonPrefix(String[] strs)
       {
           String temp=strs[0];//第一个字符串 默认有公共字符串
            int i=1;//从第二个开始找
            while (i<strs.length)
            {
                while(strs[i].indexOf(temp)!=0)//说明第二个与第一个没找到公共串的时候
                {
                    temp=temp.substring(0,temp.length()-1);//存储临时的公共串减少一个长度 接着找  如果一直没找到temp就变成空字符串了  substring是指从（x，y）号位置的字符截取
                }
                    i++;
            }
           return temp;//返回找到的字符串  如果没找到就返回空了
       }
   }
```

## 设置Goal解析器

输入：command = "G()(al)"
输出："Goal"
解释：Goal 解析器解释命令的步骤如下所示：
G -> G
() -> o
(al) -> al
最后连接得到的结果是 "Goal"

```java
class Solution
    {
        public String interpret(String command)
        {
            int len=0;
            String res="";//设置一个空字符串
            for(len=0;len<command.length();len++)//循环遍历
            {
                if(command.charAt(len)=='G')//如果是为G 那么结果加个G
                {
                    res+='G';
                }
                   if(command.charAt(len)=='(')//如果有一个左括号判断下一个是否为右括号
                   {
                       len++;
                       if(command.charAt(len)=='a')//判断一下是否为(a)这种字符串 如果是就变成al
                       {
                           res+="al";
                       }
                       if(command.charAt(len)==')')//如果不是这种字符串 判断一下是否为右括号 如果是就变成o
                       {
                          res+='o';
                       }
                   }
            }
            return res;//返回这个新的字符串
        }
    }
```

## 检查整数及其两倍数是否存在

- 输入：arr = [10,2,5,3]
- 输出：true
- 解释：N = 10 是 M = 5 的两倍，即 10 = 2 * 5 。

```java
class Solution
    {
        public boolean checkIfExist(int[] arr)
        {
            Arrays.sort(arr);//先给数组排个序
            int behind = 1;//设置一个向后指的指针 作为比较指针
            int i = 0;//设置一个循环完毕才移动的指针
            if(arr[0]<0&&arr[behind]<0)//先判断这个数组的首地址的数是否大于0 这是负数的两倍运算
            {
                while (i < arr.length && behind < arr.length)//进入循环判断
                {
                    if(i==behind)//如果两个指针指向同一个位置时 比较指针向后移动一位
                    {
                        behind++;
                        continue;
                    }
                    if (arr[i] == arr[behind] * 2 )//如果找到了这个两倍数就返回true
                        return true;
                    else if (arr[i] < arr[behind] * 2)//判断这个数是否小于这个两倍数  如果小于了  i往后移动一位 因为小于了的话 说明后面也没有指针会比这个大 就直接往后比较了
                        i++;
                    else if (arr[i] > arr[behind] * 2)//如果这个数大于了这个两倍数 比较指针往后移动
                        behind++;
                }
            }
            else while (i < arr.length && behind < arr.length)//这是正数的比较 和上边差不多 只不过移动位置和负数相反
            {
                if(i==behind)
                {
                    behind++;
                    continue;
                }
                if (arr[behind] == arr[i] * 2 )
                    return true;
                else if (arr[behind] < arr[i] * 2)
                    behind++;
                else if (arr[behind] > arr[i] * 2)
                    i++;
            }
            return false;
        }
    }
```

## 买卖股票的最佳时机

- 输入：[7,1,5,3,6,4]

- 输出：5
- 解释：在第 2 天（股票价格 = 1）的时候买入，在第 5 天（股票价格 = 6）的时候卖出，最大利润 = 6-1 = 5 。 注意利润不能是 7-1 = 6, 因为卖出价格需要大于买入价格；同时，你不能在买入前卖出股票。

```java
class Solution
    {
        public int maxProfit(int[] prices)
        {
            int profit[]=new int[prices.length];//添加一个利润
            int left=0;
            int right=1;//双指针思想
             if(prices.length==1)//如果只有一个数 就直接返回0了 不存在买卖问题
                return 0;
            if(prices[0]>=prices[1])//如果第一天的价格就高于第二天的价格 两个往后移动就可以了
            {
                left++;
                right++;
            }
            while(right<prices.length&&left<prices.length)
            {
               if(prices[right]<=prices[left])//当右边的价格小于左边的价格时候 将小价格转变成买进的价格 然后接着和下一个比较
                {
                    left=right;
                    right++;
                }
                else
                {
                    profit[index]=prices[right]-prices[left];//如果不存在这种 就添加一个利润进来 并且继续比较
                    right++;
                }
            }
            Arrays.sort(profit);//对添加进来的利润进行排序
            return profit[profit.length-1];//取最大值利润
        }
    }
```

## 盒子中小球的最大数量 hashmap的运用

- 输入：lowLimit = 1, highLimit = 10

- 输出：2

- 解释：
- 盒子编号：1 2 3 4 5 6 7 8 9 10 11 ...
- 小球数量：2 1 1 1 1 1 1 1 1 0  0  ...
- 编号 1 的盒子放有最多小球，小球数量为 2 。

```java
import java.util.*;
class Solution
    {
        public int countBalls(int lowLimit, int highLimit)
        {
              if(lowLimit==highLimit)
            {
                return 1;
            }
            Map<Integer,Integer>map=new HashMap<>();
            while(lowLimit<highLimit)
            {
                while(lowLimit<=highLimit)
                {
                    int box=0;
                    String s=Integer.toString(lowLimit);//将数字转换成String类型 方便分开后运算
                    for(int i=0;i<s.length();i++)
                    {
                        box+=s.charAt(i)-'0';//数字放在哪个盒子
                    }
                    map.put(box,(map.get(box)==null?1:map.get(box)+1));//这个就是HashMap中的统计字符串出现的次数 这里是统计数字出现的次数
                    //主要运用的就是 判断map.get(box)是这个数存不存在 如果不存在 就设置为1 如果存在就在以前的基础上+1计数
                    lowLimit++;//进入下一个数判断
                }
            }
            Collection collect=map.values();//统计字符 通过map的值来统计
            Integer max=(Integer) Collections.max(collect);//找最大值 从Collection这个对集合的操作工具中
            return max;//返回最大值
        }
    }
```

## 第 N 个泰波那契数

- 泰波那契序列 Tn 定义如下： 

- T0 = 0, T1 = 1, T2 = 1, 且在 n >= 0 的条件下 Tn+3 = Tn + Tn+1 + Tn+2

- 给你整数 n，请返回第 n 个泰波那契数 Tn 的值。


```java
class Solution
    {
        public int tribonacci(int n)//其实就是斐波那契数列的升级版 多加了一个数
        {
            int res=0;
            int[]arr=new int[n+1];
            if(n==0)
            {
                return 0;
            }
            else if (n<=2)
            {
                return 1;
            }
            for(int i=3;i<=n;i++)
            {
                arr[0]=0;
                arr[1]=1;
                arr[2]=1;
                arr[i]=arr[i-3]+arr[i-2]+arr[i-1];//arr[4]=arr[1]+arr[2]+arr[3]
                if(i==n)//当i=n时
                {
                    return arr[i];//就返回该结果
                }
            }
            return 0;
        }
    }
```

## 两个数组间的距离值

输入：arr1 = [4,5,8], arr2 = [10,9,1,8], d = 2
输出：2
解释：
对于 arr1[0]=4 我们有：
|4-10|=6 > d=2 
|4-9|=5 > d=2 
|4-1|=3 > d=2 
|4-8|=4 > d=2 
所以 arr1[0]=4 符合距离要求

对于 arr1[1]=5 我们有：
|5-10|=5 > d=2 
|5-9|=4 > d=2 
|5-1|=4 > d=2 
|5-8|=3 > d=2
所以 arr1[1]=5 也符合距离要求

对于 arr1[2]=8 我们有：
|8-10|=2 <= d=2
|8-9|=1 <= d=2
|8-1|=7 > d=2
|8-8|=0 <= d=2
存在距离小于等于 2 的情况，不符合距离要求 

```java
class Solution
    {
        public int findTheDistanceValue(int[] arr1, int[] arr2, int d)//就是看arr1与arr2之间的每个差值都大于2没有 如果大于2了就存在这样的一个距离值 就+1
        {
                int count=0;//添加计数器
                for(int i=0;i<arr1.length;i++)//对于arr1中的数组
                {
                    int index=arr1.length-1;
                    for(int j=0;j<arr2.length;j++)//对于arr2中的数组
                    {
                        int res=arr1[i]-arr2[j];
                        if(res<0)
                        {
                            res=res*-1;//有距离小于0的话就让其变成正的
                        }
                        if(res<=d)
                        {
                            index--;//这个索引的作用是 判断arr[1]中是否所有元素都大于这个距离值
                        }

                    }
                    if(index==arr1.length-1)//当所有的元素大于这个距离值时 计数器+1
                    {
                        count++;
                    }
                }
                return count;
        }
    }
```

## 盛最多水的容器

- 给定一个长度为 n 的整数数组 height 。有 n 条垂线，第 i 条线的两个端点是 (i, 0) 和 (i, height[i]) 。

- 找出其中的两条线，使得它们与 x 轴共同构成的容器可以容纳最多的水。

- 返回容器可以储存的最大水量。

- 说明：你不能倾斜容器。


```java
class Solution {
        public int maxArea(int[] height)
        {
            int right = height.length - 1;//双指针一个从前往后 一个从后往前
            int left = 0;
            int res=0;
            while (left < right)
            {
                res = Integer.max(res,(right - left) * Integer.min(height[left], height[right]));//查找最大差值 res就是现储存的值 后面那一大坨就是计算的新的面积的值
                if (height[left] > height[right])//一般来说 如果两个数当中有一个数较小时 移动它 有可能会得到一个大于原来的数 但移动那个大的数 一般来说会越来越小
                {
                    right--;
                }
                else if (height[left] < height[right])
                {
                    left++;
                }
                else
                    left++;
            }
            return res;
        }
    }
```

## 与对应负数同时存在的最大正整数

- 输入：nums = [-1,10,6,7,-7,1]
- 输出：7
- 解释：数组中存在 1 和 7 对应的负数，7 的值更大。

```java
class Solution
        {
            public int findMaxK(int[] nums)
            {
                if(nums.length==1)//先处理一下边界条件 如果只有1的长度 不存在这个对应关系 返回-1
                    return -1;
                int res=-1;//添加一个-1的结果 如果后面没有条件符合 直接返回这个res=-1
                for(int i=0;i<nums.length;i++)//直接暴力解
                {
                   for(int j=1;j<nums.length;j++)
                   {
                       if(nums[i]==nums[j]*-1)//存在这个对应数
                       {
                           if(nums[i]>0)//当先找到的是正数后面有负数对应时
                           {
                               res=Integer.max(res,nums[i]);//res=之前存储的 和后面找到的数中的最大的那个
                               break;//找到了就跳出循环 开始下一轮的查找
                           }
                           else
                           {
                               res=Integer.max(res,(nums[i]*-1));//如果是负数 作对比时应该把这个负数转换为正数再比较
                               break;
                           }
                       }
                   }
                }
               return res;
            }
        }
```

## 最大连续 1 的个数

难度简单356收藏分享切换为英文接收动态反馈

给定一个二进制数组 `nums` ， 计算其中最大连续 `1` 的个数。

 

**示例 1：**

- 输入：nums = [1,1,0,1,1,1]
- 输出：3
- 解释：开头的两位和最后的三位都是连续 1 ，所以最大连续 1 的个数是 3.

```java
class Solution
        {
            public int findMaxConsecutiveOnes(int[] nums)
            {
                int index=0;//添加计数器
                int res=0;//添加结果
                for(int i=0;i<nums.length;i++)//进行循环找值
                {
                    if(nums[i]==1)//如果找到1
                    {
                        index++;//计数器+1
                        res=Integer.max(res,index);//寻找最多出现1的值
                    }
                    else if (nums[i]==0)//如果找到了0 计数器重新计数 重新找值
                    {
                        index=0;
                    }
                }
                return res;
            }
        }
```

## 提莫攻击

难度简单336收藏分享切换为英文接收动态反馈

在《英雄联盟》的世界中，有一个叫 “提莫” 的英雄。他的攻击可以让敌方英雄艾希（编者注：寒冰射手）进入中毒状态。

当提莫攻击艾希，艾希的中毒状态正好持续 `duration` 秒。

正式地讲，提莫在 `t` 发起发起攻击意味着艾希在时间区间 `[t, t + duration - 1]`（含 `t` 和 `t + duration - 1`）处于中毒状态。如果提莫在中毒影响结束 **前** 再次攻击，中毒状态计时器将会 **重置** ，在新的攻击之后，中毒影响将会在 `duration` 秒后结束。

给你一个 **非递减** 的整数数组 `timeSeries` ，其中 `timeSeries[i]` 表示提莫在 `timeSeries[i]` 秒时对艾希发起攻击，以及一个表示中毒持续时间的整数 `duration` 。

返回艾希处于中毒状态的 **总** 秒数。

**示例 1：**

- 输入：timeSeries = [1,4], duration = 2
  输出：4
  解释：提莫攻击对艾希的影响如下：
- 第 1 秒，提莫攻击艾希并使其立即中毒。中毒状态会维持 2 秒，即第 1 秒和第 2 秒。
- 第 4 秒，提莫再次攻击艾希，艾希中毒状态又持续 2 秒，即第 4 秒和第 5 秒。
  艾希在第 1、2、4、5 秒处于中毒状态，所以总中毒秒数是 4 。

```java
class Solution
        {
            public int findPoisonedDuration(int[] timeSeries, int duration)
            {
                int res=duration;//这个是为了避免越界 找不到最后一个数字
                for(int i=0;i< timeSeries.length-1;i++)
                {
                    if(duration<=(timeSeries[i+1]-timeSeries[i]))//如果中毒持续时间小于下一次攻击的时间
                    {
                        res+=duration;
                    }
                    else if(duration>timeSeries[i+1]-timeSeries[i])//如果中毒持续时间大于或等于下一次的攻击时间
                    {
                        res+=(timeSeries[i+1]-timeSeries[i]);//这个就是res+每一次的间隔时间 因为不足中毒时间 就只要两个相差时间就行了
                    }
                }
                return res;
            }
        }
```

## 第三大的数  TreeSet

难度简单391收藏分享切换为英文接收动态反馈

给你一个非空数组，返回此数组中 **第三大的数** 。如果不存在，则返回数组中最大的数。

 

- **示例 1：**

- 输入：[3, 2, 1]
- 输出：1
- 解释：第三大的数是 1 。

```java
class Solution {
        public int thirdMax(int[] nums)
        {
                TreeSet<Integer> ts = new TreeSet<Integer>();
                for (int i=0;i<nums.length;i++)
                {
                    ts.add(nums[i]);//排序顺便不加重复数组进来
                    if(ts.size()>3)//每当这个数组大于3后 就移除最小的那个出去
                    {
                        ts.remove(ts.first());//移除第一个数 由于用了TreeSet所有元素都排序过了 并且没有重复数字
                    }
                }
                if(ts.size()<3)//判断这个数组是否大于3
                    return ts.last();//不大于就返回最大的那个
                return ts.first();//否则返回最小的那个 第三位
        }
    }
```

## 三个数的最大乘积  没啥含金量

难度简单411收藏分享切换为英文接收动态反馈

给你一个整型数组 `nums` ，在数组中找出由三个数组成的最大乘积，并输出这个乘积。

- **示例 1：**

- 输入：nums = [1,2,3]
- 输出：6

```java
class Solution {
    public int maximumProduct(int[] nums) {
        Arrays.sort(nums);//排个序
        int n = nums.length;//加个长度
        return Math.max(nums[0] * nums[1] * nums[n - 1], nums[n - 3] * nums[n - 2] * nums[n - 1]);//由于排过序 要么前面有负数时有最大值 要么后面有最大值 直接用Math.max函数找最大值就好
    }
}
```

## 错误的集合 主要就是看思想

集合 `s` 包含从 `1` 到 `n` 的整数。不幸的是，因为数据错误，导致集合里面某一个数字复制了成了集合里面的另外一个数字的值，导致集合 **丢失了一个数字** 并且 **有一个数字重复** 。

给定一个数组 `nums` 代表了集合 `S` 发生错误后的结果。

请你找出重复出现的整数，再找到丢失的整数，将它们以数组的形式返回。

- **示例 1：**
- 输入：nums = [1,2,2,4]
  输出：[2,3]

```java
class Solution
    {
        public int[] findErrorNums(int[] nums)//这题运用的是数学的求和公式
        {
            int num[]=new int[2];//添加输出的数组
            int i=0;
            int j=1;
            int len=nums.length;
            int sum=0;
            int wrong_sum=0;
            Arrays.sort(nums);//对传进来的数组进行排序
            while(i<len)//先添加值进来
            {
                wrong_sum+=nums[i];//算未改正之前的总和
                i++;
            }
            i=0;
            while(i<len&&j<len)
            {
                if(nums[i]==nums[j])//如果有重复的数字出现
                {
                    sum=(len*(1+len))/2;//求和公式
                    num[0]=nums[j];//让这个重复的数添加到新的数组中去 错误的是2
                    nums[j]+=sum-wrong_sum;//nums[j]+sum-wrong_sum 用这个错误的数字加上正确的总和减去错误的总和 算得差值 比如 1223 2是错误的 应该是4 那么就是 2+10-8=4
                    num[1]=nums[j];//返回正确的值为4
                    break;//退出循环
                }
                else//没找到就进行下一次循环
                {
                    i++;
                    j++;
                }
            }
            return num;//返回这个数组 得到需要的输出结果
        }
    }
```

## 找到所有数组中消失的数字 和上面那个题很类似 TreeSet

给你一个含 `n` 个整数的数组 `nums` ，其中 `nums[i]` 在区间 `[1, n]` 内。请你找出所有在 `[1, n]` 范围内但没有出现在 `nums` 中的数字，并以数组的形式返回结果。 

- **示例 1：**
- 输入：nums = [4,3,2,7,8,2,3,1]
  输出：[5,6]

```java
class Solution
    {
        public List<Integer> findDisappearedNumbers(int[] nums)
        {
            List<Integer>list=new ArrayList<>();
            TreeSet<Integer>ts=new TreeSet<>();//用个树排 防止重复数组出现
            for(int num:nums)
                ts.add(num);//存储不重复的数组 如 1,2,3,4,7,8 缺5,6
            for(int i=1;i<= nums.length;i++)
            {
                if(ts.first()==i&& ts.size()>1)//如果第一个数等于1 第二个数等于2 这种 并且这个size要大于1 否则ts里面会变空
                {
                    ts.remove(ts.first());//移除ts里面的第一个数 接着下一轮比较
                }
                else if(ts.first()==i&& ts.size()==1)//如果只有一个数就接着看 差哪个数字 比如 2,2,2 i等于1时不存在 就存入list i等于2时存在 但是size等于1 不管 继续循环 当i等于3时 不存在 这时将3存入list数组中去
                {
                    continue;
                }
                else
                    list.add(i);
            }
            return list;
        }
    }
```

## 数组中重复的数据

难度中等671收藏分享切换为英文接收动态反馈

给你一个长度为 `n` 的整数数组 `nums` ，其中 `nums` 的所有整数都在范围 `[1, n]` 内，且每个整数出现 **一次** 或 **两次** 。请你找出所有出现 **两次** 的整数，并以数组形式返回。

你必须设计并实现一个时间复杂度为 `O(n)` 且仅使用常量额外空间的算法解决此问题。

- **示例 1：**

- 输入：nums = [4,3,2,7,8,2,3,1]
- 输出：[2,3]

```java
class Solution
    {
        public List<Integer> findDuplicates(int[] nums)
        {
            List<Integer>list=new ArrayList<>();
            Arrays.sort(nums);//排个序
            for(int i=0;i<nums.length-1;i++)
            {
                if(nums[i]==nums[i+1])//有重复的就加入到list数组中
                    list.add(nums[i]);
            }
            return list;//输出重复的数据
        }
    }
```

## 缺失的第一个正数 TreeSet&contains

给你一个未排序的整数数组 `nums` ，请你找出其中没有出现的最小的正整数。

请你实现时间复杂度为 `O(n)` 并且只使用常数级别额外空间的解决方案。

- **示例 1：**
- 输入：nums = [1,2,0]
  输出：3
- **示例 2：**
- 输入：nums = [3,4,-1,1]
  输出：2

```java
class Solution
    {
        public int firstMissingPositive(int[] nums)
        {
           TreeSet<Integer>ts=new TreeSet<>();
           int len=nums.length;
           for(int num:nums)//添加数组到TreeSet中
               ts.add(num);
           for(int i=1;i<=len;i++)//循环遍历
           {
               if(!ts.contains(i))//如果里面没有i这个值 就返回i的值 contains就是查找指定元素有没有出现在数组中
                   return i;
           }
           return len+1;//主要找的就是最后一位数 比如 -1 1 2 3 4 5 这里未出现的就是6 值就是6
        }
    }
```

## 最小操作次数使数组元素相等

难度中等484收藏分享切换为英文接收动态反馈

给你一个长度为 `n` 的整数数组，每次操作将会使 `n - 1` 个元素增加 `1` 。返回让数组所有元素相等的最小操作次数。

- **示例 1：**
- 输入：nums = [1,2,3]
  输出：3
  解释：
  只需要3次操作（注意每次操作会增加两个元素的值）：
  [1,2,3]  =>  [2,3,3]  =>  [3,4,3]  =>  [4,4,4]

```java
class Solution
{
    public int minMoves(int[] nums)
        {
            int length = nums.length;
            int index=0;
            Arrays.sort(nums);//排序
            for(int i=1;i<length;i++)
            {
                index+=nums[i]-nums[0];//index=index+num[i]-num[0] 比如 1 2 3 index=0+2-1=1次 index=1+3-1=3次
                //比如为 1 2 5  index=0+2-1=1 index=1+5-1=5次 可以理解为右一个数在减小 把所有的数减小到数组中的最小值 就是5到1 2到1 一共需要5次
            }
            return index;
        }
}
```

## 两栋颜色不同且距离最远的房子 Math.abs()取绝对值

难度简单20收藏分享切换为英文接收动态反馈

街上有 `n` 栋房子整齐地排成一列，每栋房子都粉刷上了漂亮的颜色。给你一个下标从 **0** 开始且长度为 `n` 的整数数组 `colors` ，其中 `colors[i]` 表示第 `i` 栋房子的颜色。

返回 **两栋** 颜色 **不同** 房子之间的 **最大** 距离。

第 `i` 栋房子和第 `j` 栋房子之间的距离是 `abs(i - j)` ，其中 `abs(x)` 是 `x` 的绝对值。

**示例 1：**

![img](https://assets.leetcode.com/uploads/2021/10/31/eg1.png)

- 输入：colors = [1,1,1,6,1,1,1]
- 输出：3
- 解释：上图中，颜色 1 标识成蓝色，颜色 6 标识成红色。
- 两栋颜色不同且距离最远的房子是房子 0 和房子 3 。
- 房子 0 的颜色是颜色 1 ，房子 3 的颜色是颜色 6 。两栋房子之间的距离是 abs(0 - 3) = 3 。
- 注意，房子 3 和房子 6 也可以产生最佳答案。

```java
class Solution
{
    public int maxDistance(int[] colors)
    {
        int index=0;
        int res=0;
        int len=colors.length;
        for(int i=0;i<len;i++)
        {
            for(int j=1;j<len;j++)//用双循环
            {
                if(colors[i]!=colors[j])//如果不相等 就是有不同颜色的房子
                {
                    index=Math.abs(j-i);//取绝对值 找距离值
                    res=Integer.max(res,index);//找距离最大的值
                }
            }
        }
        return res;
    }
}
```

## 旋转函数

- 输入: nums = [4,3,2,6]
- 输出: 26

- 解释:
  F(0) = (0 * 4) + (1 * 3) + (2 * 2) + (3 * 6) = 0 + 3 + 4 + 18 = 25
  F(1) = (0 * 6) + (1 * 4) + (2 * 3) + (3 * 2) = 0 + 4 + 6 + 6 = 16
  F(2) = (0 * 2) + (1 * 6) + (2 * 4) + (3 * 3) = 0 + 6 + 8 + 9 = 23
  F(3) = (0 * 3) + (1 * 2) + (2 * 6) + (3 * 4) = 0 + 2 + 12 + 12 = 26
  所以 F(0), F(1), F(2), F(3) 中的最大值是 F(3) = 26 。

```java
class Solution
{
    public int maxRotateFunction(int[] nums)
    {
        int len=nums.length;//这个题目总结下来就是F(k)=F(K-1)+numsums-len*sums[len-K];
        int numsums=Arrays.stream(nums).sum();//总和
        int res=0;
        int temp=0;//临时储存每一次轮换的计算值
        for(int i=0;i<len;i++)
            temp+=nums[i]*i;//先计算第一遍的值
        res=temp;
        for(int i=1;i<len;i++)
        {
            temp+=numsums-len*nums[len-i];//公式
            res=Math.max(res,temp);//找最大值
        }
        return res;
    }
}
```

## 检测大写字母  大小写问题Character.isUpperCase和Charcter.isLowerCase

我们定义，在以下情况时，单词的大写用法是正确的：

- 全部字母都是大写，比如 `"USA"` 。
- 单词中所有字母都不是大写，比如 `"leetcode"` 。
- 如果单词不只含有一个字母，只有首字母大写， 比如 `"Google"` 。

给你一个字符串 `word` 。如果大写用法正确，返回 `true` ；否则，返回 `false` 。

-  **示例 1：**
- 输入：word = "USA"
  输出：true

```java
class Solution
{
    public boolean detectCapitalUse(String word)
    {
        int index=0;
        int l=0;
       for(int i=0;i<word.length();i++)
       {
           if(Character.isUpperCase(word.charAt(i)))//全是大写
           {
               index++;
               if(index==word.length())//全是大写时
                   return true;
           }
           if(Character.isUpperCase(word.charAt(0)))
           {
               if(Character.isLowerCase(word.charAt(i)))//第一个是大写 后面是小写时
               {
                   l++;
                   if (l == word.length() - 1)
                       return true;
               }
           }
       }
       l=0;
       for(int i=0;i<word.length();i++)//全时小写时
       {

           if(Character.isLowerCase(word.charAt(i)))
           {
               l++;
               if(l==word.length())
                   return true;
           }
       }
       return false;
    }
}
```

## 字符串中的单词数

统计字符串中的单词个数，这里的单词指的是连续的不是空格的字符。

请注意，你可以假定字符串里不包括任何不可打印的字符。

- **示例:**

- 输入: "Hello, my name is John"
  输出: 5
  解释: 这里的单词是指连续的不是空格的字符，所以 "Hello," 算作 1 个单词。

```java
class Solution
{
    public int countSegments(String s)
    {
        int index=0;
        int j=0;
        for(int i=0;i<s.length();i++)
        {
            if(s.charAt(i)!=' ')//检测不为空格
                j++;//这个j主要是为了后面再次判断 是否还有单词
            else if(s.charAt(i)==' '&&j>=1)//如果是空格
            {
                j=0;
                index++;
            }
        }
        if(j!=0)//如果最后还有一个单词 再将后面那个单词加进来
            index++;
        return index;
    }
}
```

## 最后一个单词的长度 判断是否为字母问题  Character.isLetter判断为英文

难度简单510收藏分享切换为英文接收动态反馈

给你一个字符串 `s`，由若干单词组成，单词前后用一些空格字符隔开。返回字符串中 **最后一个** 单词的长度。

**单词** 是指仅由字母组成、不包含任何空格字符的最大子字符串。

- **示例 1：**

- 输入：s = "Hello World"
  输出：5
  解释：最后一个单词是“World”，长度为5。

```java
class Solution
{
    public int lengthOfLastWord(String s)
    {
        int index=0;
        for(int i=s.length()-1;i>=0;i--)
        {
            if(!Character.isLetter(s.charAt(i)))//如果不是字母 往后走
                continue;
            while(Character.isLetter(s.charAt(i)))//当是字母时 说明是一个连续的单词 开始进入循环查找
            {
                index++;//计数器+1
                 if(i>0)//只要长度大于0 就接着找下一个
                i--;
                else break;//如果小于0了 就跳出循环
            }
            if(index!=0)//如果在上面的循环中找到了最后一个单词的长度 就跳出循环
                break;
        }
        return index;
    }
}
```

## 可被三整除的偶数的平均值 leetcode周赛题

给你一个由正整数组成的整数数组 `nums` ，返回其中可被 `3` 整除的所有偶数的平均值。

注意：`n` 个元素的平均值等于 `n` 个元素 **求和** 再除以 `n` ，结果 **向下取整** 到最接近的整数。

- **示例 1：**

- 输入：nums = [1,3,6,10,12,15]
  输出：9
  解释：6 和 12 是可以被 3 整除的偶数。(6 + 12) / 2 = 9 。

```java
class Solution
{
    public int averageValue(int[] nums)
    {
        int index=0;
        int []num=new int[nums.length];//重新添加一个数组进来
        int res=0;
        for(int i=0;i<nums.length;i++)
        {
            if(nums[i]%3==0&&nums[i]%2==0)//如果这个数是能被3整除的偶数 就让新数组来接收这个数
            {
                num[index]=nums[i];
                index++;
            }
        }
        if(index!=0)//开始看这个数组中是否有这样的数 如果有
        {
            for(int i=0;i<num.length;i++)
            {
                res=res+num[i];//计算新数组储存符合的数的总和
            }
            res=res/index;//用总和去除以数字的个数 来得到平均值
        }
       return res;
    }
}
```


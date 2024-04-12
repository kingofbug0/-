

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

- # 删除排序数组中的重复项
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

## 最后一个单词的长度 Character.isLetter的运用

给你一个字符串 `s`，由若干单词组成，单词前后用一些空格字符隔开。返回字符串中 **最后一个** 单词的长度。

**单词** 是指仅由字母组成、不包含任何空格字符的最大子字符串。

- **示例 1：**
- 输入：s = "Hello World"
- 输出：5
- 解释：最后一个单词是“World”，长度为5。

```java
class Solution
{
    public int lengthOfLastWord(String s)
    {
        int index=0;//计数器
        for(int i=s.length()-1;i>=0;i--)//从尾部开始找
        {
            if(!Character.isLetter(s.charAt(i)))//后面不是英文就跳过
                continue;
            while(Character.isLetter(s.charAt(i)))//找到英文字母了 开始循环 看有几个字母
            {
                index++;
                 if(i>0)//循环遍历尾部的字母
                i--;
                else break;//找完就跳出循环
            }
            if(index!=0)//如果里面是空字符串 直接跳过
                break;
        }
        return index;
    }
}
```

## 反转字符串 II 运用字符串转换为字符数组

给定一个字符串 `s` 和一个整数 `k`，从字符串开头算起，每计数至 `2k` 个字符，就反转这 `2k` 字符中的前 `k` 个字符。

如果剩余字符少于 `k` 个，则将剩余字符全部反转。

如果剩余字符小于 `2k` 但大于或等于 `k` 个，则反转前 `k` 个字符，其余字符保持原样。

- 输入：s = "abcdefg", k = 2
- 输出："bacdfeg"

```java
class Solution
{
    public String reverseStr(String s, int k)
    {
        int len=s.length();
        char[] chars = s.toCharArray();//全部转换为字符数组
        for(int i=0;i<len;i+=2*k)//这里直接找前2K个为一组 然后进行转换
        {
            reverse(chars,i,Math.min(i + k, len) - 1);
        }
        s = new String(chars);//chars转换为String
        return s;
    }
    void reverse(char[]chars,int left,int right)//翻转函数
    {
        while(left<right)
        {
            char temp=chars[left];
            chars[left]=chars[right];
            chars[right]=temp;
            left++;
            right--;
        }
    }
}
```

## 反转字符串中的单词 III

给定一个字符串 `s` ，你需要反转字符串中每个单词的字符顺序，同时仍保留空格和单词的初始顺序。

- **示例 1：**
- 输入：s = "Let's take LeetCode contest"
  输出："s'teL ekat edoCteeL tsetnoc"

```java
class Solution
{
    public String reverseWords(String s)
    {
        char[] chars = s.toCharArray();//转换成字符数组
        int right=0;
        for(int i=0;i<s.length();i++)
        {
            while(right<s.length()&&chars[right]!=32)//当不是空格时 开始计数 就是是英文单词的时候
                right++;
            reverse(chars,i,right-1);//长度从单词的开头到right 也就是结尾部分进行翻转
            i=right;//i从这个单词的尾部开始找
            right++;//因为找完了这个单词 会出现一个空格 ++的目的就是跳过这个空格 空格不参加反转
        }
        return new String(chars);
    }
    void reverse(char[] chars,int left,int right)//还是先来个翻转函数
    {
        while(left<right)
        {
            char temp=chars[left];
            chars[left]=chars[right];
            chars[right]=temp;
            left++;
            right--;
        }
    }
}
```

## 反转字符串中的单词 StringBuilder和s.trim() 就是跳过空格

- 示例 1：

- 输入：s = "the sky is blue"
  输出："blue is sky the"

- 示例 2：
- 输入：s = "  hello world  "
  输出："world hello"
  解释：反转后的字符串中不能存在前导空格和尾随空格。

```java
class Solution
{ 
    public String reverseWords(String s)
    {
        int start=0;
        int end=0;
        String trim = s.trim();//跳过空格后的字符串s 用一个新的字符串来接收
        StringBuilder sb=new StringBuilder();
        for(int i=trim.length()-1;i>=0;i--)//在新字符串中进行查找 因为还要翻转 所有从最后的单词开始查找
        {
            if(trim.charAt(i)==32)//单词间的空格跳过
                continue;
            end=i+1;//开始记录每个单词结束的位置
            while(i>=0&&trim.charAt(i)!=32)//计算单个单词的长度
            i--;
            start=i+1;//记录每个单词的开始位置
            for(int j=start;j<end;j++)
            {
                sb.append(trim.charAt(j));//开始拼接字符串
            }
            sb.append(' ');//每次拼接后 要一个空格
        }
        sb.deleteCharAt(sb.length()-1);//删除最后一个单词拼接出现的空格
        return sb.toString();
    }
}
```

## 找不同 利用ASCII码来计算 转换char

给定两个字符串 `s` 和 `t` ，它们只包含小写字母。

字符串 `t` 由字符串 `s` 随机重排，然后在随机位置添加一个字母。

请找出在 `t` 中被添加的字母。

- 示例 1:

- 输入：s = "abcd", t = "abcde"
  输出："e"
  解释：'e' 是那个被添加的字母。

```java
class Solution
    {
        public char findTheDifference(String s, String t)
        {
            int a=0,b=0;
            for(int i=0;i<s.length();i++)//利用ASCII码来计算
            {
               a+=s.charAt(i);//算s中的ASCII码
            }
            for(int i=0;i<t.length();i++)
            {
                b+=t.charAt(i);//算t中的ASCII码
            }
            if(a>b)//用char转换a-b得到char值
                return (char) (a-b);
            else
                return (char) (b-a);
        }
    }
```

## 赎金信  主要是在用List的remove功能

给你两个字符串：`ransomNote` 和 `magazine` ，判断 `ransomNote` 能不能由 `magazine` 里面的字符构成。

如果可以，返回 `true` ；否则返回 `false` 。

`magazine` 中的每个字符只能在 `ransomNote` 中使用一次。

- **示例 2：**
- 输入：ransomNote = "aa", magazine = "ab"
  输出：false
- **示例 3：**
- 输入：ransomNote = "aa", magazine = "aab"
  输出：true

```java
class Solution
{
    public boolean canConstruct(String ransomNote, String magazine)//m中有r
    {
        int index=0;
        List<Character>list=new ArrayList<Character>();
       for(int i=0;i<magazine.length();i++)
       {
          list.add(magazine.charAt(i));//添加要magazine到list中去
       }
       for(int i=0;i<ransomNote.length();i++)
       {
           for(int j=0;j<list.size();j++)//双循环 一个一个的找 
           {
               if(ransomNote.charAt(i)==list.get(j))//如果字母相同
               {
                   list.remove(j);//移除list中的这个元素 比如aa和aab 第一个a与a找到了 就移除a 变ab
                   index++;//计数器加一个
                   break;//开始下一轮循环
               }
           }
       }
       if(index==ransomNote.length())//如果计数器和ransomNote中的长度相同 就是可以由magazine里面字符构成 就返回true
           return true;
       else
           return false;
    }
}
```

## 有效的括号 用到了队列压栈来做

给定一个只包括 `'('`，`')'`，`'{'`，`'}'`，`'['`，`']'` 的字符串 `s` ，判断字符串是否有效。

- 有效字符串需满足：
- 1. 左括号必须用相同类型的右括号闭合。
  2. 左括号必须以正确的顺序闭合。
  3. 每个右括号都有一个对应的相同类型的左括号。

```java
class Solution
{
    public boolean isValid(String s)//用队列压栈做
    {
        Stack<Character>stack=new Stack<Character>();//创建一个栈
        for(int i=0;i<s.length();i++)
        {
            if(s.charAt(i)=='['||s.charAt(i)=='('||s.charAt(i)=='{')//添加左边的括号进栈
                stack.push(s.charAt(i));//压栈操作
            else if((s.charAt(i)==')')&&(stack.isEmpty()==true||stack.pop()!='('))//如果是第一个就是添加的反括号 或者是有反括号 但是栈顶出来的不是添加的左括号就返回错误 后面的思路都一样
                return false;
            else if((s.charAt(i)==']')&&(stack.isEmpty()==true||stack.pop()!='['))
                return false;
            else if((s.charAt(i)=='}')&&(stack.isEmpty()==true||stack.pop()!='{'))
                return false;
        }
        return stack.isEmpty();//看栈中是否还有元素 如果是空的说明全部匹配到了 如果不为空 就说明有没有匹配到的 返回false
    }
}
```

## 根据字符出现频率排序 用了HashMap  还有一个Collections的排序

给定一个字符串 `s` ，根据字符出现的 **频率** 对其进行 **降序排序** 。一个字符出现的 **频率** 是它出现在字符串中的次数。

返回 *已排序的字符串* 。如果有多个答案，返回其中任何一个。

- **示例 1:**
- 输入: s = "tree"
  输出: "eert"
  解释: 'e'出现两次，'r'和't'都只出现一次。
  因此'e'必须出现在'r'和't'之前。此外，"eetr"也是一个有效的答案。

```java
class Solution
{
    public String frequencySort(String s)
    {
        Map<Character, Integer> map = new HashMap<Character, Integer>();
        int length = s.length();
        for (int i = 0; i < length; i++)
        {
            map.put(s.charAt(i),map.get(s.charAt(i))==null?1:map.get(s.charAt(i))+1);//HashMap计算出现的字母数
        }
        List<Character> list=new ArrayList<>(map.keySet());//用list来存键值
        Collections.sort(list,(a,b)->map.get(b)-map.get(a));//排序 为什么是(a,b)这种我也不晓得
        StringBuffer sb = new StringBuffer();//用sb来拼接
        for (int i = 0; i < list.size(); i++)//找值
        {
            int frequency = map.get(list.get(i));//通过键来判断有几个这样的字母
            for (int j = 0; j < frequency; j++)//比如e有两个 就进行两次拼接
            {
                sb.append(list.get(i));
            }
        }
        return sb.toString();//返回拼接好的字符串
    }
}
```

## 删除链表中的节点

- 输入：head = [4,5,1,9], node = 5

- 输出：[4,1,9]
- 解释：指定链表中值为 5 的第二个节点，那么在调用了你的函数之后，该链表应变为 4 -> 1 -> 9

```java
class Solution
{
    public void deleteNode(ListNode node)
    {
      node.val=node.next.val;//先伪装  这个意思就是让前面的5变成后面那个1 就是4 1 1 9
      node.next=node.next.next;//再杀死 然后让第二个1 直接指向 9 变成4 1 9 
    }
}
```

## 删除链表的倒数第 N 个结点

给你一个链表，删除链表的倒数第 `n` 个结点，并且返回链表的头结点。

- 输入：head = [1,2,3,4,5], n = 2
- 输出：[1,2,3,5]

```java
class Solution
{
    public ListNode removeNthFromEnd(ListNode head, int n)
    {
        ListNode p=head;
        int len=0;
        while(p!=null)//求一下链表长度
        {
            len++;
            p=p.next;
        }
        int pre=len-n;//删除的是第几个元素 因为题目要求的是倒数 这样一减就是正数了
        p=head;//初始化 因为这个时候的p在最后面
        if(pre==0)//长度为1 删除倒数第一个数时 就直接是个空链表了
            return head.next;
        for(int i=0;i<pre-1;i++)//因为pre的最后一个next指针指向的是空 没意义 就要-1
        {
            p=p.next;//比如这里pre是3 那么i就是2 找到要删除结点的前一个结点
        }
       p.next=p.next.next;//让前面一个结点的next指向被删除next的下一个的结点 比如p是2 要删除的是3 2的指针指到4那里去
        return head;
    }

}
```

## 反转链表

难度简单2843收藏分享切换为英文接收动态反馈

给你单链表的头节点 `head` ，请你反转链表，并返回反转后的链表。

 

- **示例 1：**

![img](https://assets.leetcode.com/uploads/2021/02/19/rev1ex1.jpg)

- 输入：head = [1,2,3,4,5]
- 输出：[5,4,3,2,1]

```java
class Solution
{
    public ListNode reverseList(ListNode head)
    {
        int len=0;
        Stack<ListNode>stack=new Stack<>();//用栈来解决
        while(head!=null)//添加头结点进栈中
        {
            stack.push(head);
            head=head.next;
        }
        if(stack.isEmpty())
            return null;
        ListNode L=stack.pop();
        ListNode dummy=L;//确实无法理解为什么要dummy=L
        while(!stack.isEmpty())//出栈 添加到新的链表中
        {
            ListNode temp=stack.pop();//用个临时的链表来存储出栈的数
            L.next=temp;//L的next指向的是这个临时的值
            L=L.next;
        }
        L.next=null;//因为翻转了 让头部的这个结点为空 否则会形成一个循环
        return dummy;//为什么要返回dummy我也不理解
    }
}
```

## 合并两个有序链表

将两个升序链表合并为一个新的 **升序** 链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/10/03/merge_ex1.jpg)

- 输入：l1 = [1,2,4], l2 = [1,3,4]
- 输出：[1,1,2,3,4,4]

```java
class Solution
{
    public ListNode mergeTwoLists(ListNode list1, ListNode list2)
    {
        ListNode dummy=new ListNode(-1);//添加一个坏指针
        ListNode prev=dummy;//添加一个移动下一个的指针
        while(list1!=null&&list2!=null)
        {
            if(list1.val<list2.val)//如果l1中的值小于l2
            {
                prev.next=list1;//让这个移动指针指向list1
                list1=list1.next;//list1往后移动
            }
            else//和上面相同 如果l1中的值大于l2或者等于时
            {
                prev.next=list2;
                list2=list2.next;
            }
            prev=prev.next;//让移动指针也向后移动
        }
        //加个空判断
        prev.next=list1==null?list2:list1;
        return dummy.next;
    }
}
```

## 最优除法 StringBuffer和字符串拼接

- 输入: [1000,100,10,2]
- 输出: "1000/(100/10/2)"

```java
class Solution
{
    public String optimalDivision(int[] nums)
    {
        int len= nums.length;
        StringBuffer sb=new StringBuffer();
        if(len==1)
            return  sb.append(nums[0]).toString();//处理边界条件 只有一个数时直接拼接
        if(len==2)//当有两个数时 不需要括号
            return sb.append(nums[0]).append("/").append(nums[1]).toString();
        else//三个及以上时
        {
            sb.append(nums[0]).append("/(").append(nums[1]);//需要在第一个数后面拼接100/(120/13)这种
            for(int i=2;i<len;i++)
            {
                    sb.append("/");
                    sb.append(nums[i]);
            }
            sb.append(")");
        }
        return sb.toString();
    }
}
```

## 复数乘法  用了split分割和Integer的parseInt存储负数判断正负号

- **示例 1：**
- 输入：num1 = "1+1i", num2 = "1+1i"
  输出："0+2i"
  解释：(1 + i) * (1 + i) = 1 + i2 + 2 * i = 2i ，你需要将它转换为 0+2i 的形式。

```java
class Solution {
    public String complexNumberMultiply(String num1, String num2) {
        String[] split = num1.split("\\+|i");//利用分割 正则表达式 \\是用来正则表达式中转义成\由于+有特殊含义 所有需要\+ |是或的意思 这一行的主要意思就是+|i都要分割
        String[] split1 = num2.split("\\+|i");
        int real1 = Integer.parseInt(split[0]);//由于parseInt可以判断正负号 所有就不用管它的正负号了
        int imag1 = Integer.parseInt(split[1]);
        int real2 = Integer.parseInt(split1[0]);
        int imag2 = Integer.parseInt(split1[1]);
        return (real1*real2-imag1*imag2)+"+"+(real1*imag2+real2*imag1)+"i";
    }
}
```

## 二分查找

- 
  **示例 1:**
- 输入: nums = [-1,0,3,5,9,12], target = 9
  输出: 4
  解释: 9 出现在 nums 中并且下标为 4

```java
class Solution
    {
        public int search(int[] nums, int target)//利用二分查找来做
        {
            int right=nums.length-1;
            int left=0;
            while(left<=right)//使用左闭右闭原则
            {
                int middle=((right+left)/2);//每次二分的点
                if(nums[middle]>target)//说明target在左边区间
                    right=middle-1;
                else if(nums[middle]<target)//说明target在右边区间
                    left=middle+1;
                else return middle;//如果nums[middle]==target的话 就说明找到了 返回middle
            }
            return -1;//未找到
        }
    }
```

## 搜索插入位置

- **示例 1:**
- 输入: nums = [1,3,5,6], target = 5
  输出: 2

```java
class Solution
{
    public int searchInsert(int[] nums, int target)//二分查找来做
    {
        int left=0;
        int right=nums.length-1;
        int middle=0;
        while(left<=right)
        {
            middle=left+(right-left)/2;
            if(nums[middle]>target)//说明在左边
                right=middle-1;
            else if(nums[middle]<target)//说明在右边
                left=middle+1;
            else return middle;//找到这个数了
        }
        //如果循环出来还没有找到这个数 就要添加这个数 在right的右边
            return right+1;
    }
}
```

## 滑动窗口

**精髓代码**

```java
while(sum>=s)
{
		subLength=(j-i+1);//取滑动的长度
		result=result<subLength?result:subLength;
		sum-=nums[i++];//滑动窗口的精髓 不断变更i 序列的位置
}
```

## bfs搜索迷宫 最短路径问题

**下图给出了一个迷宫的平面图，其中标记为** **1** **的为障碍，标记为** **0** **的为可以通行的地方。**

 **010000**

 **000100**

 **001001**

 **110000**

​    **迷宫的入口为左上角，出口为右下角，在迷宫中，只能从一个位置走到这个它的上、下、左、右四个方向之一。**

​    **对于上面的迷宫，从入口开始，可以按DRRURRDDDR的顺序通过迷宫，一共 10 步。其中 D、U、L、R **分别表示向下、向上、向左、向右走.

​    **对于下面这个更复杂的迷宫（30 行 50 列），请找出一种通过迷宫的方式，其使用的步数最少，在步数最少的前提下，请找出字典序最小的一个作为答案。请注意在字典序中D<L<R<U。**

```c++
//从下左右上开始搜索
int direct[4][2] = { {1,0},{0,-1},{0,1},{-1,0} };
char d[4] = { 'D','L','R','U' };
struct Node
{
	int x, y;//代表位置
	string s;//需要字符串
};
void bfs()//bfs要用queue 队列 
{
		Node now, next;//一个表示当前位置,一个表示下一个位置
		queue<Node>que;
		maze[0][0] = '1';//迷宫初始位置意味着走过了
		now.s = "";//初始化一下s
		now.x = now.y = 0;
		que.push(now);
		while (!que.empty())
		{
			now = que.front();//获取现在队列中的值
			que.pop();//获取完成后就删除
			if (now.x == 29 && now.y == 49)//边界条件
				cout << now.s;
			for (int i = 0; i < 4; i++)//四个方向的判断
			{
				next.x = now.x+direct[i][0];//下一步x的位置是 现在x的位置+方向
				next.y = now.y+direct[i][1];
				if (0 <= next.x && next.x <=30 && 0 <= next.y && next.y <= 50 && maze[next.x][next.y] == '0')//如果在这个范围内可移动
				{
					maze[next.x][next.y] = '1';//将下一步要走的地方标记为1
					next.s = now.s + d[i];//s进行叠加
					que.push(next);//添加这个位置
				}
			}
		}
}
```

### 应对所有这种迷宫问题 完全代码

```c++
#include<iostream>
#include"vector"
#include"queue"
using namespace std;
//从下左右上开始搜索
int direct[4][2] = { {1,0},{0,-1},{0,1},{-1,0} };
char d[4] = { 'D','L','R','U' };//注意 这里的位序和上面的方向要相同
int n, m;//n为行 m为列
char maze[100][100];
struct node
{
	int x, y;
	string s;
};
void bfs()
{
		node next, now;
		queue<node>que;
		maze[0][0] = '1';
		now.s = "";
		now.x = now.y = 0;
		que.push(now);
		while (!que.empty())
		{
			now=que.front();
			que.pop();
			if (now.x == n - 1 && now.y == m - 1)
				cout << now.s<<endl;
			for (int i = 0; i < 4; i++)
			{
				next.x = now.x + direct[i][0];
				next.y = now.y + direct[i][1];
				if (0 <= next.x && next.x < n && 0 <= next.y && next.y < m && maze[next.x][next.y] == '0')
				{
					maze[next.x][next.y] = '1';
					next.s = now.s + d[i];
					que.push(next);
				}
			}
		}
}
int main()
{
	cin >> n >> m;
	for (int i = 0; i < n; i++)
		for (int j = 0; j < m; j++)
			cin >> maze[i][j];
	bfs();
	return 0;
}
```

## [2290. 到达角落需要移除障碍物的最小数目](https://leetcode.cn/problems/minimum-obstacle-removal-to-reach-corner/) 1-0的bfs问题 只有1和0的问题

给你一个下标从 0 开始的二维整数数组 grid ，数组大小为 m x n 。每个单元格都是两个值之一：

0 表示一个 空 单元格，
1 表示一个可以移除的 障碍物 。
你可以向上、下、左、右移动，从一个空单元格移动到另一个空单元格。

现在你需要从左上角 (0, 0) 移动到右下角 (m - 1, n - 1) ，返回需要移除的障碍物的 最小 数目。

示例 1：       

```
0 1 1
1 1 0
1 1 0
```

输入：grid = [[0,1,1],[1,1,0],[1,1,0]]
输出：2
解释：可以移除位于 (0, 1) 和 (0, 2) 的障碍物来创建从 (0, 0) 到 (2, 2) 的路径。
可以证明我们至少需要移除两个障碍物，所以返回 2 。
注意，可能存在其他方式来移除 2 个障碍物，创建出可行的路径。

```c++
class Solution
{
	struct node
	{
		int x, y;
	};
public:
	int minimumObstacles(vector<vector<int>>& grid)
	{
		//右 下 左 上
		node now, next;
		int direct[4][2] = { {0,1},{1,0},{0,-1},{-1,0} };
		int n = grid.size(), m = grid[0].size();
		int dis[5][10];
		memset(dis, 20, sizeof(dis));//初始化
		dis[0][0] = 0;
		deque<node>deq;
		now.x = now.y = 0;
		deq.push_back(now);
		while (!deq.empty())
		{
			now = deq.front();//取队头
			deq.pop_front();//出队列
			for (int i = 0; i < 4; i++)
			{
				next.x = now.x + direct[i][0];
				next.y = now.y + direct[i][1];//模拟方向移动
				if (next.x >= 0 && next.x < n && next.y >= 0 && next.y < m)//进行方向判断
				{
					if (dis[now.x][now.y] + grid[next.x][next.y] < dis[next.x][next.y])//如果现在 距离 加上 下一步要走的地方的值(因为是有1和0是可以改变的) 小于 下一步的距离
					{
						dis[next.x][next.y] = dis[now.x][now.y] + grid[next.x][next.y];
						if (grid[next.x][next.y] == 0)//如果下一步的位置是不需要+1来移除路障的 添加到队头
							deq.emplace_front(next);
						else if (grid[next.x][next.y] == 1)//如果是需要移除路障的 添加到队尾 需要移除路障说明距离要长一点 就后面再遍历
							deq.emplace_back(next);
					}
				}
			}
		}
		return dis[n-1][m-1];//得到的最后值 出口位置就是得到的需要移除障碍的数量
	}
};
```



## [344. 反转字符串](https://leetcode.cn/problems/reverse-string/)

编写一个函数，其作用是将输入的字符串反转过来。输入字符串以字符数组 s 的形式给出。

不要给另外的数组分配额外的空间，你必须原地修改输入数组、使用 O(1) 的额外空间解决这一问题。

-  示例 1：


输入：s = ["h","e","l","l","o"]
输出：["o","l","l","e","h"]

```c++
class Solution {
public:
    void reverseString(vector<char>& s) {
         int n = s.size();
        for (int left = 0, right = n - 1; left < right; ++left, --right) {
            swap(s[left], s[right]);//用swap函数进行交换就行了
        }
    }
};
           
```

## [557. 反转字符串中的单词 III](https://leetcode.cn/problems/reverse-words-in-a-string-iii/)

给定一个字符串 `s` ，你需要反转字符串中每个单词的字符顺序，同时仍保留空格和单词的初始顺序。

- 输入：s = "Let's take LeetCode contest"
- 输出："s'teL ekat edoCteeL tsetnoc"

```c++
class Solution {
public:
    string reverseWords(string s) {
       int j = 0;
		for (int i = 0; i <= s.length(); i++)
		{
			while (s[i] == ' ')//每当遇到空格符号时 就开始进行翻转之前的
			{
				reverse(s.begin()+j, s.begin()+i);//开始翻转
				i++;
				j = i;//想当于是个左右指针,j是开始指针,i是移动指针,控制需要翻转的单词范围
			}
			if (i == s.length() - 1)//当在最后一个时,没有空格符号
				reverse(s.begin() + j, s.begin() + i + 1);
		}
		return s;
    }
};
```

[1653. 使字符串平衡的最少删除次数 ](https://leetcode.cn/problems/minimum-deletions-to-make-string-balanced/)  枚举思想

给你一个字符串 s ，它仅包含字符 'a' 和 'b' 。

你可以删除 s 中任意数目的字符，使得 s 平衡 。当不存在下标对 (i,j) 满足 i < j ，且 s[i] = 'b' 的同时 s[j]= 'a' ，此时认为 s 是 平衡 的。

请你返回使 s 平衡 的 最少 删除次数。

- 输入：s = "aababbab"

- 输出：2
- 解释：你可以选择以下任意一种方案：
- 下标从 0 开始，删除第 2 和第 6 个字符（"aababbab" -> "aaabbb"），
- 下标从 0 开始，删除第 3 和第 6 个字符（"aababbab" -> "aabbbb"）。

```c++
class Solution {
public:
    int minimumDeletions(string s) {
        int res = 0, stringa = 0,stringb=0;
		for (int i = 0; i < s.size(); i++)
		{
			if (s[i] == 'a')//由于只有a和b 遇到a时,记录一下a有多少个
				stringa++;
		}
		res = stringa;
		for (int i = 0; i < s.size(); i++)
		{
			if (s[i] == 'a')//重新遍历一遍 遇到a就减少一个 相当于删除 相当于当有a在b的左边时
				stringa--;
			else
				stringb++;
			res = min(res, stringa + stringb);//stringa代表在右边的a stringb代表在左边的b  这是一种枚举思想
		}
		return res;
    }
};
```

## [3. 无重复字符的最长子串](https://leetcode.cn/problems/longest-substring-without-repeating-characters/) 滑动窗口思想

给定一个字符串 `s` ，请你找出其中不含有重复字符的 **最长子串** 的长度。

- 输入: s = "abcabcbb"
- 输出: 3 
- 解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。

```c++
class Solution 
{
public:
    int lengthOfLongestSubstring(string s) 
    {
        unordered_set<char>umap;
		int right = -1, res = 0,len=s.length();
		for (int i = 0; i < len; i++)
		{
			if (i != 0)//当第一次滑动结束后,删除第一个元素 进入下一次的滑动
				umap.erase(s[i-1]);
			while (right + 1 < len && !umap.count(s[right + 1]))//开始滑动 umap.count[s[right+1]]表示的是 在当前umap中的键是否含有s[right+1]的键 如果有就不能进入循环
			{
				umap.insert(s[right+1]);
				right++;
			}
			res = max(res, right - i+1);
		}
		return res;
    }
};
```

## [567. 字符串的排列](https://leetcode.cn/problems/permutation-in-string/) 滑动窗口思想

给你两个字符串 s1 和 s2 ，写一个函数来判断 s2 是否包含 s1 的排列。如果是，返回 true ；否则，返回 false 。

换句话说，s1 的排列之一是 s2 的 子串 。

- 输入：s1 = "ab" s2 = "eidbaooo"
- 输出：true
- 解释：s2 包含 s1 的排列之一 ("ba").

```c++
class Solution 
{
public:
    bool checkInclusion(string s1, string s2) 
    {
        int len1 = s1.length(), len2 = s2.length();
		if (len1 > len2)
			return false;
		vector<int>v1(123), v2(123);//这里我没有转换 直接用123的大小来装 string类型的字母
		for (int i = 0; i < len1; i++)
		{
			v1[s1[i]]++;//找对应的ASCII码的字母 
			v2[s2[i]]++;
		}
		if (v1 == v2)//如果两个string 都是相同的 就直接返回true
			return true;
		for (int i = len1; i < len2; i++)//从len1处开始
		{
            //就是这里体现滑动思想
			v2[s2[i]]++;//添加后面的元素
			v2[s2[i - len1]]--;//删除之前添加的元素 比如eidbaooo 先添加进来的是ei 在这里添加d 删除i 以此类推 一直循环找到子串
			if (v1 == v2)//当存在子串的时候返回
				return true;
		}
		return false;
    }
};
```

## [76. 最小覆盖子串](https://leetcode.cn/problems/minimum-window-substring/) 滑动窗口思想

给你一个字符串 `s` 、一个字符串 `t` 。返回 `s` 中涵盖 `t` 所有字符的最小子串。如果 `s` 中不存在涵盖 `t` 所有字符的子串，则返回空字符串 `""` 。

- 示例 1：

- 输入：s = "ADOBECODEBANC", t = "ABC"
  输出："BANC"
  解释：最小覆盖子串 "BANC" 包含来自字符串 t 的 'A'、'B' 和 'C'。

```c++
class Solution 
{
public:
    string minWindow(string s, string t) 
    {
        int len1 = s.length(), len2 = t.length(), left = 0, count = 0, min = len1+1, start = 0;
		if (len1 < len2)//因为是s中包含t的子串 如果s都大于t了肯定没有子串
			return "";
		unordered_map<char, int>tmap;
		for (auto a : t)//对子串进行添加到哈希表中
			tmap[a]++;
		for (int right=0; right < len1; right++)//进入循环
		{
			if (tmap[s[right]] > 0)//找这个值是否出现过
				count++;
			//在s中查找出现的t 如果出现了 就让那个值--; 需要个count判断 当减的次数等于len1时 进入循环开始滑动
			tmap[s[right]]--;
			while (count == len2)
			{
				if (min > right - left + 1)//记录出现最短子串的距离
				{
					min = right - left + 1;
					start = left;//更新一下开始位置
				}
				if (tmap[s[left]] == 0)//记录结束 减去最开始包含的值 跳出循环
					count--;
				tmap[s[left]]++;//复原
				left++;//左指针移动 接着复原
			}
		}
		return min == s.size() + 1 ? "" : s.substr(start, min);//判断min是不是没有改变,如果没有改变说明不包含子串,返回空,如果改变了 给值是从start位置开始 往后进行min位的字符串拼接
    }
};
```

## [剑指 Offer 47. 礼物的最大价值](https://leetcode.cn/problems/li-wu-de-zui-da-jie-zhi-lcof/) 动态规划思想

在一个 m*n 的棋盘的每一格都放有一个礼物，每个礼物都有一定的价值（价值大于 0）。你可以从棋盘的左上角开始拿格子里的礼物，并每次向右或者向下移动一格、直到到达棋盘的右下角。给定一个棋盘及其上面的礼物的价值，请计算你最多能拿到多少价值的礼物？

- 示例 1:

- 输入: 
  [
    [1,3,1],
    [1,5,1],
    [4,2,1]
  ]
  输出: 12
  解释: 路径 1→3→5→2→1 可以拿到最多价值的礼物

```c++
class Solution 
{
public:
    int maxValue(vector<vector<int>>& grid) 
    {
        int m = grid.size(), n = grid[0].size();
		vector<vector<int>> f(m, vector<int>(n));//定义一个名字为f的vector二维数组 其中调用了vector的构造函数,构造了一个行为m,列为n数组
		//因为每次只能选择向右或者向下 向右时:f(i,j+1) 向下时: f(i+1,j)
		//还需要状态转移 每次移动时 上一步则是 向右后:f(i,j-1) 向下后:f(i-1,j)
		//所以状态转移为: f(i,j)=f(i,j-1)+grid(i,j)||f(i-1,j)+grid(i,j)
		//所以当i或j==0时不进行转移
		for (int i = 0; i < m; i++)
		{
			for (int j = 0; j < n; j++)
			{
				if (i > 0)
					f[i][j] = max(f[i - 1][j], f[i][j]);//状态转移方程,这个其实就和棋盘问题有点点像,进行下和右的判断,找到最大的值进行移动
				if (j > 0)
					f[i][j] = max(f[i][j - 1], f[i][j]);
				f[i][j] += grid[i][j];
			}
		}
		return f[m-1][n-1];
    }
};
```

## [70. 爬楼梯](https://leetcode.cn/problems/climbing-stairs/) 动态规划思想

假设你正在爬楼梯。需要 `n` 阶你才能到达楼顶。

每次你可以爬 `1` 或 `2` 个台阶。你有多少种不同的方法可以爬到楼顶呢？

-  **示例 1：**
- 输入：n = 2
  输出：2
  解释：有两种方法可以爬到楼顶。
- 1. 1 阶 + 1 阶
  2. 2 阶

```c++
class Solution 
{
public:
    int climbStairs(int n) 
    {
        //添加dp数组
        int dp[n+1];
        //设置边界
        dp[0]=dp[1]=1;
        //填充dp
        for(int i=2;i<=n;i++)
            dp[i]=dp[i-1]+dp[i-2];
        return dp[n]; //尾数即为方法
    }
};
```

## [746. 使用最小花费爬楼梯](https://leetcode.cn/problems/min-cost-climbing-stairs/) 动态规划思想

给你一个整数数组 cost ，其中 cost[i] 是从楼梯第 i 个台阶向上爬需要支付的费用。一旦你支付此费用，即可选择向上爬一个或者两个台阶。

你可以选择从下标为 0 或下标为 1 的台阶开始爬楼梯。

请你计算并返回达到楼梯顶部的最低花费。

- 输入：cost = [10,15,20]
  输出：15
  解释：你将从下标为 1 的台阶开始。
- 支付 15 ，向上爬两个台阶，到达楼梯顶部。
  总花费为 15 。

```c++
class Solution 
{
public:
    int minCostClimbingStairs(vector<int>& cost) 
    {
        int n=cost.size();
        vector<int>dp(n+1);//定义dp数组
		dp[0] = 0;//初始化,因为在第0阶和第1阶都是不花费体力的
		dp[1] = 0;
		for (int i = 2; i <= n; i++)
		{
            //dp[i-1]+cost[i-1] 是跳一阶 dp[i-2]+cost[i-2]是跳两阶
			dp[i] = min(dp[i - 1] + cost[i - 1], dp[i - 2] + cost[i - 2]);
		}
		return dp[n];
    }
};
```

## [1590. 使数组和能被 P 整除](https://leetcode.cn/problems/make-sum-divisible-by-p/) 前缀和+哈希表优化

给你一个正整数数组 nums，请你移除 最短 子数组（可以为 空），使得剩余元素的 和 能被 p 整除。 不允许 将整个数组都移除。

请你返回你需要移除的最短子数组的长度，如果无法满足题目要求，返回 -1 。

子数组 定义为原数组中连续的一组元素。

-  示例 1：

- 输入：nums = [3,1,4,2], p = 6
  输出：1
  解释：nums 中元素和为 10，不能被 p 整除。我们可以移除子数组 [4] ，剩余元素的和为 6 。

```c++
class Solution 
{
public:
    int minSubarray(vector<int>& nums, int p) 
    {
       int n = nums.size(), ans = n;
		int s[n+1];
		s[0] = 0;
		for (int i = 0; i < n; ++i)
			s[i + 1] = (s[i] + nums[i]) % p;//存储前缀和对p的取余
		int x = s[n];//尾余等于x
		unordered_map<int, int> last;
		for (int i = 0; i <= n; ++i)
        {
			last[s[i]] = i;//添加余数和对应的数组长度
			auto it = last.find((s[i] - x + p) % p);//找同余?
			if (it != last.end())
				ans = min(ans, i-it->second);
		}
		return ans < n ? ans : -1;//
    }
};
```

## [49. 字母异位词分组](https://leetcode.cn/problems/group-anagrams/) 哈希表运用

给你一个字符串数组，请你将 字母异位词 组合在一起。可以按任意顺序返回结果列表。

字母异位词 是由重新排列源单词的字母得到的一个新单词，所有源单词中的字母通常恰好只用一次。

- 示例 1:

- 输入: strs = ["eat", "tea", "tan", "ate", "nat", "bat"]
  输出: [["bat"],["nat","tan"],["ate","eat","tea"]]

```c++
class Solution 
{
public:
    vector<vector<string>> groupAnagrams(vector<string>& strs) 
    {
       	vector<string>s1;
		unordered_map<string,vector<string>> umap;
		vector<vector<string>>s2;
		int len = strs.size();
		for (int i = 0; i < len; i++)
			s1.push_back(strs[i]);
		for (int i = 0; i < len; i++)
			sort(strs[i].begin(), strs[i].end());//对strs中的每个单独字符串进行排序 
		for (int i = 0; i < len; i++)
			umap[strs[i]].emplace_back(s1[i]);//添加的是umap[排序后的].emplace_back[未排序的] 也就意味着是 比如eat 那么添加的是 aet.emplace_back(s1[0]) 里面的eat
       //是通过排序过后的值去找之前的值
		for (auto it = umap.begin(); it != umap.end(); ++it) 
		{
			s2.emplace_back(it->second);//获取值的个数和对应的键 找原始的值
		}
		return s2;
    }
};
```

## [665. 非递减数列](https://leetcode.cn/problems/non-decreasing-array/) 判断数组是否有序的函数使用

给你一个长度为 n 的整数数组 nums ，请你判断在 最多 改变 1 个元素的情况下，该数组能否变成一个非递减数列。

我们是这样定义一个非递减数列的： 对于数组中任意的 i (0 <= i <= n-2)，总满足 nums[i] <= nums[i + 1]。

- 示例 1:

- 输入: nums = [4,2,3]
  输出: true
  解释: 你可以通过把第一个 4 变成 1 来使得它成为一个非递减数列。
  示例 2:

- 输入: nums = [4,2,1]
  输出: false
  解释: 你不能在只改变一个元素的情况下将其变为非递减数列。

```c++
class Solution 
{
public:
    bool checkPossibility(vector<int>& nums) 
    {
		for (int i = 0; i < nums.size()-1; i++)
		{
				if (nums[i] > nums[i+1])
				{
					int temp = nums[i];
					nums[i] =nums[i+1];
					if (is_sorted(nums.begin(), nums.end()))//查看该数组是否是升序
						return true;
                    //有两种可能 这个数要变大或者变小后称为非递减
					nums[i] = temp;//由于只能改变一次 所以在这里进行操作
					nums[i + 1] = nums[i];
					return (is_sorted(nums.begin(), nums.end()));
				}
		}
		return true;
    }
};
```

## 选择法排序(递归版)

```c++
#include <iostream>
#include<algorithm>
using namespace std;

void selectSort(int a[], int len, int i)
{
    int k,j;
    if (i == len - 1)
        return;
    else
    {
        k = i;
        for (int j = i + 1; j < len; j++)
        {
            if (a[j] < a[k])
                k = j;
        }
        if (k != i)
            swap(a[i], a[k]);
        selectSort(a, len, i + 1);
    }
}
int main() 
{
    int len = 7;
    int a[] = { 1,5,8,7,6,3,2 };
    selectSort(a, len, 0);
    for(int i=0;i<len;i++)
        printf("%d", a[i]);
    return 0;
}
```

## 选择排序(暴力法)

```c++
void SelectSort(int a[], int len)
{
    for (int i = 0; i < len; i++)
    {
        int max = i;
        for (int j = i + 1; j < len; j++)
            if (a[max] > a[j])
                max=j;
        if(max!=i)
            swap(a[i],a[max]);
    }
}
```

##  冒泡排序(递归版)

```c++
void BubbleSort(int a[], int len, int i)
{

    if (i == len - 1)
        return;
    else
    {
        int flag = 0;
        for (int j = len - 1; j >i; j--)
        {
            if (a[j] < a[j - 1])
            {
                swap(a[j], a[j - 1]);
                flag = 1;
            }
        }
        if (flag == 0)
            return;
        else BubbleSort(a, len, i + 1);
    }
}
int main() 
{
    int len = 10;
    int a[] = { 1,5,8,7,6,10,2,9,3,4 };
    BubbleSort(a, len, 0);
    for(int i=0;i<len;i++)
        printf("%d", a[i]);
    return 0;
}
```

## 冒泡排序(暴力法)

```c++
void BubbleSort(int a[], int len)
{
    for(int i=0;i<len;i++)
        for (int j = i + 1; j < len; j++)
        {
            if (a[i] > a[j])
                swap(a[i], a[j]);
        }
}
```

## 全排列(递归版)

```c++
void dfs(int a[], int len, int i)
{
    if (i >= len)
    {
        for (int j = 0; j < len; j++)
            cout << a[j];
        cout << endl;
        return;
    }
    else
    {
        for (int j = i; j < len; j++)
        {
            swap(a[i], a[j]);
            dfs(a, len, i + 1);
            swap(a[i], a[j]);
        }
    }
}
int main() 
{
    int len = 3;
    int a[] = { 1,2,3 };
    dfs(a, len, 0);
    return 0;
}
```

## 斐波那契(递归版)

```c++
int fib(int n)
{
    if (n == 1 || n == 2)
        return 1;
    else return fib(n - 1) + fib(n - 2);
}
int main() 
{
    iiin
    cout<<fib(6);
    return 0;
}
```

## 斐波那契(动态规划)

```c++
int fib(int n)
{
    vector<int>dp(n + 1, 0);
    dp[1] = 1; dp[2] = 1;
    for (int i = 3; i <= n; i++)
    {
        dp[i] = dp[i - 2] + dp[i - 1];
    }
    return dp[n];
}
```

## 快速排序(分治思想)

```c++
void quicksort(int a[], int left, int right)
{
    if (left==right)
    {
        return;
    }
    else if(left<right)
    {
        int i = left, j = right;
        int key = left;//检索的基数
        while (i < j)
        {
            while (a[key] <= a[j] && i < j)
                j--;
            swap(a[key], a[j]);//交换条件是当目前的基数大于右边的j时,才发生交换,也就是大的在右边
            key = j;
            while (a[i] <= a[key] &&i < j)
                i++;
            swap(a[key], a[i]);//小的在左边
            key = i;
        }
        quicksort(a, left, key - 1);//对左边部分进行排序
        quicksort(a, key + 1, right);//对右边部分进行排序
    }
}
```

## 归并排序(分治思想)

```c++
void merge(int arr[],int left,int right)
{
    int mid=(left + right) / 2;
    int len = 500;
    vector<int>temp(len,0);
    int i = left, j = mid+1,pos=0;//pos指针用于temp的自增覆盖
    while (i <= mid&&j<=right)
    {
        if (arr[i] < arr[j])//左半区第一个元素更小
            temp[pos++] = arr[i++];
        else //右边区第一个元素更小 
            temp[pos++] = arr[j++];
    }
    //判断左右剩下的元素 进行填入即可
    while (i<=mid)
    {
        temp[pos++] = arr[i++];
    }
    while (j <= right)
    {
        temp[pos++] = arr[j++];
    }
    //把临时存储的数组赋值到letf到right位置上
    for (int i = 0; i < pos; i++)
        arr[left + i] = temp[i];
}
void mergeSort(int arr[],int left,int right)
{
    if (right == left)
        return;
    else if(left<right)
    {
        int mid = (left + right) / 2;
        mergeSort(arr,left, mid);//分区 左半区
        mergeSort(arr,mid + 1, right);//右半区
        merge(arr,left,right);//合并函数
    }
}
```

## 最大连续子序列的和(暴力法)

```c++
int MaxConSum(int a[], int len)
{
    int maxsum = 0;
    for (int i = 0; i < len; i++)
    {
        int sum = a[i];
        for (int j = i + 1; j < len; j++)
        {
            sum += a[j];
            maxsum = max(sum, maxsum);
        }
    }      
    return maxsum;
}
```

## 背包问题(回溯法+暴力破解)

```c++
int maxvalue(vector<int>w, vector<int>v, int nowweight, int maxw,int i)
{
    if (nowweight > maxw)
        return -1;
    if (i == w.size())
        return 0; 
    else
    {
        //不选
        int p1=maxvalue(w, v, nowweight, maxw, i + 1);
        //选  
        int p2Next=maxvalue(w, v, nowweight + w[i], maxw, i + 1);
        int p2 = -1;
        if (p2Next != -1)
            p2 = v[i] + p2Next;
        return max(p1, p2);
    }    
}
```

## 1-9选数只进行+或-或不选运算符当结果等于100时进行输出所有的解(回溯)

```c++
void dfs(int a[],char op[],int temp,int s,int i)
{
    if (i == 9)
    {
        if (s == 100)//达到目标开始输出
        {
            cout << a[0];
            for (int j = 1; j < 9; j++)
            {
                if (op[j] == ' ')//没有插入符号
                {
                    cout << a[j];
                }
                else//插入符号了
                    cout << op[j] << a[j];
            }
            cout << "=100" << endl;
        }
    }
    else
    {
        int t;
        //选了+号
        op[i] = '+';
        s += a[i];
        dfs(a, op, +a[i], s, i + 1);
        //回溯
        s -= a[i];
        //选了-号
        op[i] = '-';
        s -= a[i];
        dfs(a, op, -a[i], s, i + 1);
        //回溯
        s += a[i];
        //没有选符号
        op[i] = ' ';
        s -= temp;//因为没有选符号 这个位置要先把这个数减去,不能加入进来 要让他与下一位进行运算
        if (temp > 0)
            t = temp * 10 + a[i];
        else t = temp * 10 - a[i];
        s += t;
        dfs(a, op, t, s, i + 1);
        //回溯
        s -= t;//先到没有选符号两个数是合并在一起的状态
        s += temp;//再减去这个数本身比如一开始这个数是34 -34后 再+这个数3
    }
}
```

## 活动安排问题(回溯法)

```c++
#define MAX = 51
struct action
{
    int bengin;
    int end;
};
action a[] = { {1,3},{2,5},{4,8},{6,10} };
int n = 4;//活动数量
int nowx[51];//当前解
int bestx[51];//最优解
int nowsum = 0;//当前的活动
int maxsum = 0;//最多的活动
int laste = 0;//每个活动的最后结束时间
void print()
{
    cout << "最佳排列活动安排为:"<<endl;
    int laste = 0;
    for (int j = 0; j < n; j++)
    {
        if (a[bestx[j]].bengin >= laste)
        {
            cout << "选取活动:" << bestx[j]<<":" << a[bestx[j]].bengin << a[bestx[j]].end << endl;
            laste = a[bestx[j]].end;
        }
    }
    cout << "安排活动的个数是:" << maxsum << endl;
}
void dfs(int i)
{
    if (i == n)
    {
        if (nowsum > maxsum)
        {
            maxsum = nowsum;
            for (int i = 0; i < n; i++)
                bestx[i] = nowx[i];
        }
    }
    else
    {
        for (int j = i; j < n; j++)
        {
            swap(nowx[i], nowx[j]);
            int tempsum = nowsum;
            int templaste = laste;
            if (a[nowx[j]].bengin >= laste)
            {
                nowsum++;
                laste = a[nowx[j]].end;
            }
            dfs(i + 1);
            swap(nowx[i], nowx[j]);
            nowsum = tempsum;
            laste = templaste;
        }
    }
}
int main() 
{
    for (int i = 0; i < n; i++)
        nowx[i] = i;
    dfs(0);
    print();
    return 0;
}
```

## 迷宫问题(回溯法)

```c++
char maze[8][8] = {
'O','X','X','X','X','X','X','X',
'O','O','O','O','O','X','X','X',
'X','O','X','X','O','O','O','X',
'X','O','X','X','O','X','X','O',
'X','O','X','X','X','X','X','X',
'X','O','X','X','O','O','O','X',
'X','O','O','O','O','X','O','O',
'X','X','X','X','X','X','X','O'
};
//上右下左
int direct[4][2] = { {-1,+0},{+0,+1},{+1,+0},{+0,-1} };
void dfs(int i, int j)
{
    if (i == 7 && j == 7)
    {
        maze[i][j] = ' ';
        for (int x = 0; x < 8; x++)
        {
            for (int y = 0; y < 8; y++)
                cout << maze[x][y];
            cout << endl;
        }
           
    }
    else
    {
        //上右下左
        //int direct[4][2] = { {-1,+0},{+0,+1},{+1,+0},{+0,-1} };
        if (i >= 0 && i <= 7 && j >= 0 && j <= 7 && maze[i][j] == 'O')
        {
            maze[i][j] = ' ';
            //开始dfs
            dfs(i + direct[0][0], j + direct[0][1]);
            dfs(i + direct[1][0], j + direct[1][1]);
            dfs(i + direct[2][0], j + direct[2][1]);
            dfs(i + direct[3][0], j + direct[3][1]);
            maze[i][j] = 'O';
        }
    }
}
```

## 求解正数拆分问题(动态规划)

- 例1 对某一个正整数n进行拆分

  拆分的时候最大可以用到的正整数是k

  求对n进行拆分可使用最大为k拆分数，一共有多少种方法？

  举例：

  假设n=5，k=5

  对5进行拆分，可以用到的最大拆分的数5

  第1种组合：5=5

  第2种组合：5=4+1

  第3种组合：5=3+2

  第4种组合：5=3+1+1

  第5种组合：5=2+2+1

  第6种组合：5=2+1+1+1

  第7种组合：5=1+1+1+1+1

  答案7

分析:

f(4,1)=1  f(4,2)=3=f(4-2,2)+f(4,2-1)

f(3,1)=1  f(3,2)=2=1+1=f(3-2,2)+f(3,2-1)    f(3,3)=3=f(3,2)+1

f(2,1)=1  f(2,2)=2=1+1=f(2,1)+1

f(1,1)=1 f(1,2)=1

- 【1】   条件     n==1 或者 k==1 

​     	表达式  f(n,k)=1

​		【2】   条件     n==k

​     	表达式  f(n,k)=f(n,k-1)+1

​		【3】   条件     n>k

​     	表达式  f(n,k)=f(n-k,k)+f(n,k-1)

​		【3】   条件     n<k

​    	 表达式  f(n,k)=f(n,n)

​         	f(3,5)=f(3,3)

```c++
int dp[101][101];
int f(int n, int k)
{
    for(int i=1;i<=n;i++)
        for (int j = 1; j <= k; j++)
        {
            if (i == 1 || j == 1)
                dp[i][j] = 1;
            else if (i == j)
                dp[i][j] = dp[i][j - 1] + 1;
            else if (i > j)
                dp[i][j] = dp[i - j][j] + dp[i][j - 1];
            else if (i < j)
                dp[i][j] = dp[i][i];
        }
    return dp[n][k];
}
```

## 0/1背包问题(动态规划)

```c++
vector<int>weight= {2,2,6,5,4};
int maxweight;
vector<int>value = { 6,3,20,4,6 };
int f()
{
    vector<int> dp(maxweight + 1, 0);
    for (int i = 0; i < weight.size(); i++)
    for (int j = maxweight; j >= weight[i]; j--)
        dp[j] = max(dp[j], dp[j - weight[i]] + value[i]);
    return dp[maxweight];
}
int main() 
{
    cin >> maxweight;
    cout << f();
    return 0;
}
```

## 最长公共子序列(动态规划)

```c++
int longestCommonSubsequence( string& text1,  string& text2, string& lcs) {
    int m = text1.size();
    int n = text2.size();
    vector<vector<int>> dp(m + 1, vector<int>(n + 1, 0));
    for (int i = 1; i <= m; i++) {
        for (int j = 1; j <= n; j++) {
            if (text1[i - 1] == text2[j - 1]) {
                dp[i][j] = dp[i - 1][j - 1] + 1;
            }
            else {
                dp[i][j] = max(dp[i - 1][j], dp[i][j - 1]);
            }
        }
    }
    // 回溯构建最长公共子序列
    int i = m, j = n;
    while (i > 0 && j > 0) {
        if (text1[i - 1] == text2[j - 1]) {
            lcs = text1[i - 1] + lcs;
            i--;
            j--;
        }
        else if (dp[i - 1][j] >= dp[i][j - 1]) {
            i--;
        }
        else {
            j--;
        }
    }
    return dp[m][n];
}

int main() {
    string text1, text2;
    cout << "输入第一个序列: ";
    cin >> text1;
    cout << "输入第二个序列: ";
    cin >> text2;
    string lcs;
    int length = longestCommonSubsequence(text1, text2, lcs);
    cout << "最长公共子序列的长度为: " << length << endl;
    cout << "最长公共子序列为: " << lcs << endl;
    return 0;
}
```

## 内置函数dfs

```c++
function<int(int, int, int, int)>dfs = [&](int i, int y, int ic, int ec)->int
        {

        };
```

## [2496. 数组中字符串的最大值](https://leetcode.cn/problems/maximum-value-of-a-string-in-an-array/)   (stoi的使用)

- stoi也就是对string类型转换为int类型的输出

```c++
class Solution {
public:
    int maximumValue(vector<string>& strs) {
        int len = strs.size();
        int maxnum=0;
        for (int i = 0; i < len; i++)
        {
            int char_num = 0;
            for (int j = 0; j < strs[i].length(); j++)
            {
                if (strs[i][j] >= 'a' && strs[i][j] <= 'z')
                {
                    char_num = strs[i].length();
                    break;
                }
            }
            if (char_num == 0)
                char_num = stoi(strs[i]);//对strs[i]转换为十进制的int数据
            maxnum = max(maxnum, char_num);
        }
        return maxnum;
    }
};
```

## [459. 重复的子字符串](https://leetcode.cn/problems/repeated-substring-pattern/) 对find函数和子字符串的理解

```c++
class Solution {
public:
    bool repeatedSubstringPattern(string s) {
        string ss = s + s;//因为重复的子字符串比如 abcabcabcabc 重复的是abc重复构成,当两个相同的字符串相加后,去掉首位,再去找原字符串,如果能找到就说明存在重复子字符串
        ss.erase(0,1); 
        ss.erase(ss.length()-1,ss.length());
        int a=ss.find(s);
        return a==-1?false:true;
    }
};
```

## [686. 重复叠加字符串匹配](https://leetcode.cn/problems/repeated-string-match/)  对find函数的使用

- 示例 1：

- 输入：a = "abcd", b = "cdabcdab"
  输出：3
  解释：a 重复叠加三遍后为 "abcdabcdabcd", 此时 b 是其子串。

```c++
class Solution {
public:
    int repeatedStringMatch(string a, string b) {
         int index = 1;
        int res1=a.find(b);
        if (res1 != -1)
            return true;
        int len1 = a.length();
        string temp = a;
        int multiple = (b.length() / len1)+2;
        //在根据实际情况模拟后,当这个字符串重复multiple次后还是没有匹配的子串,说明没有匹配子串,根据这个定义得到方法,不断的叠加然后去找这个匹配的b子串
        for (int i = 0; i < multiple; i++)
        {    
            temp += a;
            if (temp.find(b) != temp.npos)//找到了
                return temp.length()/len1;         
        }
        return -1;
    }
};
```

## [647. 回文子串](https://leetcode.cn/problems/palindromic-substrings/)  暴力法

- **示例 2：**
- 输入：s = "aaa"
  输出：6
  解释：6个回文子串: "a", "a", "a", "aa", "aa", "aaa"

```c++
class Solution {
public:
    bool cheack(string s, int i, int j)
    {       
        while (i < j)
        {
            if (s[i] != s[j])
                return false;
            i++, j--;
        }
        return true;
    }
    int countSubstrings(string s) {
        int len = s.length();
            int res=0;
            //也就是不断取值找子串,去判断是否是回文串
            for (int i = 0; i < len; i++)
            {
                for (int j = i; j <len; j++)
                {                      
                    if (cheack(s,i,j))
                        res++;
                }
            }
            return res;
    }
};
```

## [214. 最短回文串](https://leetcode.cn/problems/shortest-palindrome/) substr的使用 

- **示例 1：**
- 输入：s = "aacecaaa"
  输出："aaacecaaa"
- substr是两个参数一般第一个参数代表从开头位置,第二个参数代表截取长度

```c++
class Solution
{
public:
   bool cheak(string s,int i,int j)
    {
        while (i <= j)
        {
            if (s[i] != s[j])
                return false;
            i++, j--;
        }
        return true;
    }
    string shortestPalindrome(string s)
    {
        int i = 0;
        int index = 0;
        int j = s.length() - 1;
        string res;
        for (int i = j; i >= 0; i--)
        {
            if (i == j)
            {
                if (cheak(s, 0, i))
                    return s;
            }
            else
            {
                if (cheak(s, 0, i))//截取位置是从左往右的最大回文串,然后将没有回文部分加入到字符串t中进行翻转操作,再加到头部,相当于是aacecaaa 截取到aacecaa是 最后一个a不是,将最后一个a翻转后添加到头部
                {
                    string t = s.substr(i+1, j-i);
                    reverse(t.begin(), t.end());
                    res = t + s;
                    break;
                }
            }
            
        }
        return res;
    }
};
```

## [1681. 最小不兼容性](https://leetcode.cn/problems/minimum-incompatibility/) (dfs+回溯)

- 输入：nums = [6,3,8,1,3,1,2,2], k = 4

- 输出：6
- 解释：最优的子集分配为 [1,2]，[2,3]，[6,8] 和 [1,3] 。
- 不兼容性和为 (2-1) + (3-2) + (8-6) + (3-1) = 6 。

```c++
class Solution 
{
public:
    int res = INT_MAX;
    void dfs(vector<int>nums,vector<int>count,vector<int>tempnum,int i,int n,int tempres)
    {
        if (tempres >= res)
            return ;
        if (i == nums.size())
        {
            if (tempres < res)
                res = tempres;
            return;
        }
        for (int j = 0; j < count.size(); j++)
        {
            if (tempnum[j] == nums[i])//有相同字符
                continue;
            if (count[j] < n)//没有相同字符且还可以继续往里面添加数字
            {
                int temp = tempnum[j];
                tempnum[j] = nums[i];
                count[j]++;//计算数组大小看是否可以往里面添加数字
                int delta = count[j] >= 2 ? (nums[i] - temp) : 0;//计算临时不兼容性增量 因为必须要有两个以上的数字才可以计算
                dfs(nums, count, tempnum, i + 1, n, tempres+delta);
                count[j]--;
                tempnum[j] = temp;
                if (count[j] == 0)
                    break;
            }
        }
    }
    int minimumIncompatibility(vector<int>& nums, int k) 
    {
        unordered_map<int, int>umap;
        int n = nums.size() / k;//获取每个子集最多可存多少个数
        sort(nums.begin(), nums.end());
        for (auto a : nums)
        {
            if (++umap[a] > k)//有重复数据
                return -1;
        }
        vector<int>tempnum(k), count(k,0);//num是存数,count是存大小    
        dfs(nums, count, tempnum, 0, n, 0);
        return res;             
    }
};
```

## [560. 和为 K 的子数组](https://leetcode.cn/problems/subarray-sum-equals-k/)  (前缀和+哈希优化)

给你一个整数数组 `nums` 和一个整数 `k` ，请你统计并返回 *该数组中和为 `k` 的连续子数组的个数* 。

-  **示例 1：**
- 输入：nums = [3,4,7,2,-3,1,4,2], k = 7
  输出：4

```c++
class Solution {
public:
    int subarraySum(vector<int>& nums, int k) {
        unordered_map<int, int>umap;
        umap.emplace(0, 1);
        int res = 0;
        int temp = 0;
        //前缀和 也就是比如3 4 7 2 -3 1 4 2的数中找和为7的连续子数组
        //先计算它的前缀和为 0 3 7 14 16 13 14 18 20
        //然后用它的前缀和去减去要找的值比如 14-7=7 然后在前缀和umap数组中去找7出现的次数
        //公式:pre[i]-pre[j]=k  
        for (auto a : nums)
        {
            temp += a;//temp就是在计算前缀和
            if (umap.find(temp - k) != umap.end())
                 res += umap[temp - k];
            umap[temp]++;
        }
        return res;
    }
};
```

## [16. 最接近的三数之和](https://leetcode.cn/problems/3sum-closest/)  unordered_map的排序

- 给你一个长度为 `n` 的整数数组 `nums` 和 一个目标值 `target`。请你从 `nums` 中选出三个整数，使它们的和与 `target` 最接近。
- 返回这三个数的和。
- 假定每组输入只存在恰好一个解。

-  示例 1：

- 输入：nums = [-1,2,1,-4], target = 1
  输出：2
  解释：与 target 最接近的和是 2 (-1 + 2 + 1 = 2) 。

```c++
class Solution {
public:
    int threeSumClosest(vector<int>& nums, int target) {
         int len = nums.size();
        int res = 0;
        vector<pair<int, int>>difference;
        unordered_map<int, int>umap;
        sort(nums.begin(), nums.end());
        for (int i = 0; i < len; i++)
        {
            int left = i + 1, right = len - 1;
            while (left < right)
            {
                if (nums[left] + nums[right] + nums[i] < target)
                {
                    umap.emplace(abs(nums[left] + nums[right] + nums[i] - target), nums[left] + nums[right] + nums[i]);
                    left++;
                }
                else if (nums[left] + nums[right] + nums[i] > target)
                {
                    umap.emplace(abs(nums[left] + nums[right] + nums[i] - target), nums[left] + nums[right] + nums[i]);
                    right--;
                }
                else
                {
                    res = nums[left] + nums[right] + nums[i];
                    return res;
                }
            }
        }
        for (auto it : umap)
            difference.push_back(it);
        sort(difference.begin(), difference.end(), [](auto p1, auto p2) {return p1.first < p2.first; });    
        res = difference[0].second;         
        return res;
    }
};
```

## 16. 最接近的三数之和 双指针版本

```c++
class Solution {
public:
    int threeSumClosest(vector<int>& nums, int target) {
        int len = nums.size();
        int ans = nums[0]+nums[1]+nums[2];
        sort(nums.begin(),nums.end());
        for (int i = 0; i < len-2; i++)
        {
            int left = i + 1, right = len - 1;           
            while (left < right)
            {
                int tempSum = nums[left] + nums[right] + nums[i];
                if (abs(tempSum - target) < abs(ans - target))
                {
                    ans = tempSum;
                }
                if (tempSum > target)
                {
                    right--;
                }
                else if (tempSum < target)
                    left++;
                else return tempSum;
            }
        }
        return ans;
    }
};
```

## [523. 连续的子数组和](https://leetcode.cn/problems/continuous-subarray-sum/)   前缀和+哈希

给你一个整数数组 `nums` 和一个整数 `k` ，编写一个函数来判断该数组是否含有同时满足下述条件的连续子数组：

- 子数组大小 **至少为 2** ，且
- 子数组元素总和为 `k` 的倍数。

如果存在，返回 `true` ；否则，返回 `false` 。

如果存在一个整数 `n` ，令整数 `x` 符合 `x = n * k` ，则称 `x` 是 `k` 的一个倍数。`0` 始终视为 `k` 的一个倍数。

```c++
class Solution {
public:
    bool checkSubarraySum(vector<int>& nums, int k) {
        int len = nums.size();
        int temp = nums[0];
        unordered_map<int, int>umap;
        umap[0] = -1;
        int remainder = 0;
        for (int i = 0; i < len; i++)
        {
            remainder = (remainder + nums[i]) % k;//前缀和的余数
            if (umap.count(remainder))//同余定理,当前缀和中存在相同余数,代表这个和能被k整除
            {
                int index = umap[remainder];
                if (i - index >= 2)//当下表的值大于2代表数组大于2
                    return true;
            }
            else
                umap[remainder] = i;//记录下标
        }
        return false;
    }
};
```

## [525. 连续数组](https://leetcode.cn/problems/contiguous-array/)  前缀和+哈希数组

- 给定一个二进制数组 `nums` , 找到含有相同数量的 `0` 和 `1` 的最长连续子数组，并返回该子数组的长度。

```c++
class Solution {
public:
    int findMaxLength(vector<int>& nums) {
        unordered_map<int,int>umap;
        int temp = 0, res = 0;
        umap[0] = -1;
        //给一个0初始化
        for (int i = 0; i < nums.size(); i++)
        {
            if (nums[i] == 0)//当访问为0时给-1
                temp += -1;
            else//访问为1时给1
                temp += 1;
            if (umap.count(temp) && umap.size() > 1)//开始找前缀的值
            {
                int index = umap[temp];//找之前出现的位置
                res = max(res, i - index);//寻找最大值
                continue;//只要在这个哈希数组中存在这个值,就不用进行添加了,我们要找的是最大的
            }
            umap[temp] = i;
        }
        return res;
    }
};
```

## [15. 三数之和](https://leetcode.cn/problems/3sum/) (数组查重+双指针)

- 给你一个整数数组 nums ，判断是否存在三元组 [nums[i], nums[j], nums[k]] 满足 i != j、i != k 且 j != k ，同时还满足 nums[i] + nums[j] + nums[k] == 0 。请

- 你返回所有和为 0 且不重复的三元组。

- 注意：答案中不可以包含重复的三元组。


```c++
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
         int len = nums.size();
        vector<vector<int>>res;
        sort(nums.begin(), nums.end());
        for (int i = 0; i < len; i++)
        {
            if (nums[i] > 0)
                return res;
            if (i > 0 && nums[i] == nums[i - 1])
                continue;
            int left = i + 1, right = len - 1;
            while (left < right)
            {
                if (nums[left] + nums[right] > -nums[i])
                    right--;
                else if (nums[left] + nums[right] < -nums[i])
                    left++;
                else
                {
                    res.push_back(vector<int>{nums[i], nums[left], nums[right]});
                    left++;
                    right--;
                    //查重
                    while (left < right && nums[left] == nums[left - 1])
                        left++;
                    while (left < right && nums[right] == nums[right + 1])
                        right--;
                }
            }
        }
        return res;
    }
};
```

## [874. 模拟行走机器人](https://leetcode.cn/problems/walking-robot-simulation/)  哈希表pair函数运用+方向判断+count函数运用

- 机器人在一个无限大小的 XY 网格平面上行走，从点 (0, 0) 处开始出发，面向北方。该机器人可以接收以下三种类型的命令 commands ：

- -2 ：向左转 90 度
  -1 ：向右转 90 度
  1 <= x <= 9 ：向前移动 x 个单位长度
  在网格上有一些格子被视为障碍物 obstacles 。第 i 个障碍物位于网格点  obstacles[i] = (xi, yi) 。

- 机器人无法走到障碍物上，它将会停留在障碍物的前一个网格方块上，但仍然可以继续尝试进行该路线的其余部分。

- 返回从原点到机器人所有经过的路径点（坐标为整数）的最大欧式距离的平方。（即，如果距离为 5 ，则返回 25 ）


- 输入：commands = [4,-1,4,-2,4], obstacles = [[2,4]]
  输出：65
  解释：机器人开始位于 (0, 0)：
- 1. 向北移动 4 个单位，到达 (0, 4)
  2. 右转
  3. 向东移动 1 个单位，然后被位于 (2, 4) 的障碍物阻挡，机器人停在 (1, 4)
  4. 左转
  5. 向北走 4 个单位，到达 (1, 8)
  距离原点最远的是 (1, 8) ，距离为 12 + 82 = 65


```c++
class Solution {
public:
//上左下右
    int directions[4][2] = { {0,1},{-1,0},{0,-1},{1,0} };
    int robotSim(vector<int>& commands, vector<vector<int>>& obstacles) 
    {
        int len = commands.size();
        int res = 0;
        int x = 0, y = 0, dir = 0;
        //因为c++中没有unordered_map的pair函数,所以这里用set数组,可以使用pair
        set<pair<int, int>>set;
        for (auto num : obstacles)
            set.emplace(num[0], num[1]);
        for (auto a : commands)
        {
            if (a == -1)//右转
            {
                dir = (dir + 3) % 4;

            }
            else if (a == -2)//左转
            {
                dir = (dir + 1) % 4;
            }
            else//直走
            {
                for (int i = 0; i < a; i++)
                {
                    int tempx = x + directions[dir][0];
                    int tempy = y + directions[dir][1];
                    //判断障碍
                    if (set.count({ tempx,tempy }))
                        break;
                    x = tempx;
                    y = tempy;
                    res = max(res, x * x + y * y);
                }
            }
        }
        return res;
    }
};
```

## [5. 最长回文子串](https://leetcode.cn/problems/longest-palindromic-substring/) 中心扩散法+substr

- **示例 1：**
- 输入：s = "babad"
  输出："bab"
  解释："aba" 同样是符合题意的答案。

```c++
class Solution {
public:
    string longestPalindrome(string s)
    {
        int len = s.length();
        if (len < 2)
            return s;
        //记录起始和结束的位置
        int longst = 0, start = 0;
        for (int i = 0; i < len;)
        {
            if (len - i <= longst / 2)
                break;
            int left = i, right = i;
            //找重复字符
            while (right < len - 1 && s[right + 1] == s[right])
                ++right;
            //计算i下一个位置
            i = right + 1;
            //找可拓展区域
            while (right < len - 1 && left>0 && s[left - 1] == s[right + 1])
            {
                right++;
                left--;
            }
            //计算最大值
            if (right - left + 1 > longst)
            {
                start = left;
                longst = right - left + 1;
            }
        }
        return s.substr(start, longst);
    }
};
```

## [503. 下一个更大元素 II](https://leetcode.cn/problems/next-greater-element-ii/)  单调栈

- 给定一个循环数组 `nums` （ `nums[nums.length - 1]` 的下一个元素是 `nums[0]` ），返回 *`nums` 中每个元素的 **下一个更大元素*** 。
- 数字 `x` 的 **下一个更大的元素** 是按数组遍历顺序，这个数字之后的第一个比它更大的数，这意味着你应该循环地搜索它的下一个更大的数。如果不存在，则输出 `-1` 。

- **示例 2:**
- 输入: nums = [1,2,3,4,3]
  输出: [2,3,4,-1,4]

```c++
class Solution {
public:
    vector<int> nextGreaterElements(vector<int>& nums) {
        int len = nums.size();
        vector<int>res(len,-1);
        stack<int>stack;
        for (int i = 0; i < len * 2; i++)
        {   
            //当栈中有元素 且比当前遍历到的数字小时,栈中元素弹出,且当前遍历到的数字作为下一个最大的元素赋值
            while (!stack.empty() && nums[i % len] > nums[stack.top()])
            {
                res[stack.top()] = nums[i % len];
                stack.pop();
            }
            //栈存的是数组下标
            stack.push(i % len);
        }
        return res;
    }
};
```

## [316. 去除重复字母](https://leetcode.cn/problems/remove-duplicate-letters/) 单调栈(我觉得爆难)

- 给你一个字符串 `s` ，请你去除字符串中重复的字母，使得每个字母只出现一次。需保证 **返回结果的字典序最小**（要求不能打乱其他字符的相对位置）。

-  **示例 1：**
- 输入：s = "bcabc"
  输出："abc"

```c++
class Solution {
public:
    string removeDuplicateLetters(string s) {
        int len = s.length();
        vector<int>visit(26);
        vector<int>count(26);
        string ans;
        for (auto c : s)
            count[c - 'a']++;
        for (int i = 0; i < len; i++)
        {
            if (!visit[s[i] - 'a'])//如果当前字符出现过2次以上
            {
                while (!ans.empty() && ans.back() > s[i])//判断现在遍历的这个字符是否大于存在栈中的字符
                {
                    if (count[ans.back() - 'a'] > 0)//如果计数字符还有多余的
                    {
                        visit[ans.back() - 'a'] = 0;//先将可删除字符的判断归0
                        ans.pop_back();//再将目前存在栈中的字符弹出
                    }
                    else break;
                }
                visit[s[i] - 'a'] = 1;//给它一个true代表可以删除前面出现的字符
                ans.push_back(s[i]);//将目前的字符先添加进栈中
            }
            count[s[i] - 'a']--;//每遍历一次后都要删除一次计数 就是看后面是否还有多余的字符
        }
        return ans;
    }
};
```

## [456. 132 模式](https://leetcode.cn/problems/132-pattern/) 单调栈(稍微温柔一点) 维护栈即可

- 给你一个整数数组 nums ，数组中共有 n 个整数。132 模式的子序列 由三个整数 nums[i]、nums[j] 和 nums[k] 组成，并同时满足：i < j < k 和 nums[i] < nums[k] < nums[j] 。

- 如果 nums 中存在 132 模式的子序列 ，返回 true ；否则，返回 false 。


- **示例 2：**
- 输入：nums = [3,1,4,2]
  输出：true
  解释：序列中有 1 个 132 模式的子序列： [1, 4, 2] 。

```c++
class Solution {
public:
    bool find132pattern(vector<int>& nums) {
        int len = nums.size();
        int maxsum = INT_MIN;//维护中间的值132中的2
        stack<int>st;//维护最大值3
        for (int i =len-1; i >= 0; i--)//找值1
        {
            if (nums[i]<maxsum)
                return true;
            while (!st.empty() && st.top() < nums[i])
            {
                maxsum = max(maxsum, st.top());
                st.pop();               
            }
            st.push(nums[i]);
        }
        return false;
    }
};
```

## [402. 移掉 K 位数字](https://leetcode.cn/problems/remove-k-digits/)  单调栈

- 示例 1 ：

- 输入：num = "1432219", k = 3
  输出："1219"
  解释：移除掉三个数字 4, 3, 和 2 形成一个新的最小的数字 1219 。

```c++
class Solution {
public:
    string removeKdigits(string num, int k) {
        vector<char>st;
        string ans;
        int len = num.length();
        int index = 0;
        for (int i = 0; i < len; i++)
        {
            char ch = num[i];
            while (!st.empty()&& st.back() > ch && k)
            {
                st.pop_back();
                k--;
            }
            st.push_back(ch);
        }
        while (k > 0)
        {
            st.pop_back();
            k--;
        }
        bool isZero=true;
        for(auto c:st)
        {
            if(isZero&&c=='0')
            continue;
            isZero=false;
            ans+=c;
        }
        return ans == "" ? "0" : ans;
    }
};
```

## [84. 柱状图中最大的矩形](https://leetcode.cn/problems/largest-rectangle-in-histogram/) 单调栈+左右循环找值

```c++
class Solution {
public:
    int largestRectangleArea(vector<int>& heights) {
         int len = heights.size();
        int ans = 0;
        stack<int>st;
        for (int i = 0; i < len; i++)
        {
            int num = heights[i];
            while (!st.empty() && heights[st.top()] > num)
            {
                int height = heights[st.top()];
                st.pop();
                int width = i;
                if (!st.empty())
                    width = i - st.top() - 1;               
                ans = max(ans, width * height);
            }
            st.push(i);
        }
        while (!st.empty())
        {
            int height = heights[st.top()];
            st.pop();
            int width = len;
            if (!st.empty())
                width = len - st.top() - 1;          
            ans = max(ans, width * height);
        }
        return ans;
    }
};
```

## [42. 接雨水](https://leetcode.cn/problems/trapping-rain-water/) 双指针 

- 给定 `n` 个非负整数表示每个宽度为 `1` 的柱子的高度图，计算按此排列的柱子，下雨之后能接多少雨水。

```c++
class Solution {
public:
    int trap(vector<int>& height) {
        int len = height.size();
        int left = 0, right = len - 1;
        int leftMax = 0, rightMax = 0,ans=0;
        while (left < right)
        {
            leftMax = max(leftMax, height[left]);//计算左边挡板高度
            rightMax = max(rightMax, height[right]);//计算右边挡板高度
            if (leftMax<rightMax)//计算面积的公式是当前最大挡板减去现在遍历的小挡板,根据两边挡板不一样变化答案
            {
                ans = ans + leftMax - height[left];
                ++left;
            }
            else
            {
                ans = ans + rightMax - height[right];
                right--;
            }
        }
        return ans;
    }
};
```

## [438. 找到字符串中所有字母异位词](https://leetcode.cn/problems/find-all-anagrams-in-a-string/)  滑动窗口妙用

- **示例 1:**
- 输入: s = "cbaebabacd", p = "abc"
  输出: [0,6]
  解释:
  起始索引等于 0 的子串是 "cba", 它是 "abc" 的异位词。
  起始索引等于 6 的子串是 "bac", 它是 "abc" 的异位词。

```c++
class Solution {
public:
    vector<int> findAnagrams(string s, string p) {
        vector<int>umap(26),umaps(26);
        vector<int>res;
        int len = s.size(),len2=p.size();
        for (auto ch : p)
            umap[ch-'a']++;
        for (int i = 0; i < len; i++)
        {
            umaps[s[i] - 'a']++;
            if (i >= len2-1)
            {
                if (umap == umaps)
                    res.push_back(i - len2 + 1);
                umaps[s[i - len2 + 1] - 'a']--;
            }            
        }
        return res;
    }
};
```

## [567. 字符串的排列](https://leetcode.cn/problems/permutation-in-string/) 滑动窗口妙用(2)

- **示例 1：**
- 输入：s1 = "ab" s2 = "eidbaooo"
  输出：true
  解释：s2 包含 s1 的排列之一 ("ba")

```C++
class Solution {
public:
    bool checkInclusion(string s1, string s2) {
        vector<int>ns1(26), ns2(26);
        int len2 = s2.size(), len1 = s1.size();
        for (auto ch : s1)
            ns1[ch - 'a']++;
        for (int i = 0; i < len2; i++)
        {
            ns2[s2[i] - 'a']++;
            if (i >= len1 - 1)
            {
                if (ns1 == ns2)
                    return true;
                //减的是包含完长度s1的最开始的加入的那个数字
                ns2[s2[i - len1 + 1] - 'a']--;
            }
        }
        return false;
    }
};
```

# 双周赛112场

## [2839. 判断通过操作能否让字符串相等 I ](https://leetcode.cn/problems/check-if-strings-can-be-made-equal-with-operations-i/)  这个题目和2840相同 运用计数和cmp函数比较

给你两个字符串 `s1` 和 `s2` ，两个字符串的长度都为 `4` ，且只包含 **小写** 英文字母。

你可以对两个字符串中的 **任意一个** 执行以下操作 **任意** 次：

- 选择两个下标 `i` 和 `j` 且满足 `j - i = 2` ，然后 **交换** 这个字符串中两个下标对应的字符。

如果你可以让字符串 `s1` 和 `s2` 相等，那么返回 `true` ，否则返回 `false` 。

- **示例 1：**
- 输入：s1 = "abcd", s2 = "cdab"
  输出：true
  解释： 我们可以对 s1 执行以下操作：
- - 选择下标 i = 0 ，j = 2 ，得到字符串 s1 = "cbad" 。
  - 选择下标 i = 1 ，j = 3 ，得到字符串 s1 = "cdab" = s2 。

 

```c++
class Solution {
public:
    bool checkStrings(string s1, string s2) {
          //统计两个字符在奇偶出现的次数
          int count1[2][26]{},count2[2][26]{};
        for(int i=0;i<s1.size();i++)
        {
            //因为可以无限换 所以只要统计他们在奇偶出现的次数即可,比如
            //s1= a b c d s2= c d a b 只要出现在相同奇偶位次数相同就返回true
            count1[i%2][s1[i]-'a']++;
            count2[i%2][s2[i]-'a']++;
        }
        //比较字符串函数
        return memcmp(count1,count2,sizeof(count1))==0;
    }
};
```

## [2841. 几乎唯一子数组的最大和](https://leetcode.cn/problems/maximum-sum-of-almost-unique-subarray/)   滑动窗口和统计

给你一个整数数组 `nums` 和两个正整数 `m` 和 `k` 。

请你返回 `nums` 中长度为 `k` 的 **几乎唯一** 子数组的 **最大和** ，如果不存在几乎唯一子数组，请你返回 `0` 。

如果 `nums` 的一个子数组有至少 `m` 个互不相同的元素，我们称它是 **几乎唯一** 子数组。

子数组指的是一个数组中一段连续 **非空** 的元素序列。

- **示例 1：**
- 输入：nums = [2,6,7,3,1,7], m = 3, k = 4
  输出：18
  解释：总共有 3 个长度为 k = 4 的几乎唯一子数组。分别为 [2, 6, 7, 3] ，[6, 7, 3, 1] 和 [7, 3, 1, 7] 。这些子数组中，和最大的是 [2, 6, 7, 3] ，和为 18 。

```c++
class Solution {
public:
    long long maxSum(vector<int>& nums, int m, int k) {
        int len = nums.size();
        unordered_map<int,int>umap;
        long long res = 0,sum=0;
        //先统计k-1个数 方便进入滑动
        for(int i=0;i<k-1;i++)
        {
            sum+=nums[i];
            umap[nums[i]]++;
        }
        for (int i = k-1; i < len; i++)
        {
            //开始进入滑动窗口 现在正好是k个数
            sum+=nums[i];
            umap[nums[i]]++;
            //有重复大于m个数出现 统计结果
            if(umap.size()>=m)
            {
                res=max(res,sum);
            }
            //查看滑出的数字是哪个 减去它
            int out =nums[i-k+1];
            sum-=out;
            //判断它在umap中是否还存在
            if(--umap[out]==0)
                umap.erase(out);
        }
        return res;
    }
};
```

## [207. 课程表](https://leetcode.cn/problems/course-schedule/)  拓扑算法 bfs+二维向量定义

你这个学期必须选修 `numCourses` 门课程，记为 `0` 到 `numCourses - 1` 。

在选修某些课程之前需要一些先修课程。 先修课程按数组 `prerequisites` 给出，其中 `prerequisites[i] = [ai, bi]` ，表示如果要学习课程 `ai` 则 **必须** 先学习课程 `bi` 。

- 例如，先修课程对 `[0, 1]` 表示：想要学习课程 `0` ，你需要先完成课程 `1` 。

请你判断是否可能完成所有课程的学习？如果可以，返回 `true` ；否则，返回 `false` 。

-  **示例 1：**
- 输入：numCourses = 2, prerequisites = [[1,0]]
  输出：true
  解释：总共有 2 门课程。学习课程 1 之前，你需要完成课程 0 。这是可能的。

```c++
class Solution {
public:
    bool canFinish(int numCourses, vector<vector<int>>& prerequisites) {
         vector<int> sub[numCourses];//定义一个二维向量 行数为numCourses 列数不固定的二维向量
        vector<int> in_degree(numCourses);
        for (auto e : prerequisites)
        {
            sub[e[1]].push_back(e[0]);//也就是添加前置课表对应的数组.push_back需要完成的课表
            in_degree[e[0]]++;//把要完成的课表添加进图中
        }
        queue<int>q;
        for (int i = 0; i < numCourses; i++)
        {
            if (!in_degree[i])//如果这个课不存在前置课了,就加入队列中
                q.push(i);
        }
        int cnt = 0;
        while (!q.empty())//当队列中有值时 删除该节点 移除它的所有出边
        {
           int temp = q.front();
           q.pop();
           cnt++;
           for (auto j : sub[temp])
           {
               if (--in_degree[j] == 0)//寻找入度为0的节点
                   q.push(j);
           }
        }
        
        return cnt==numCourses;
    }
};
```

## [210. 课程表 II](https://leetcode.cn/problems/course-schedule-ii/) 拓扑算法+bfs

现在你总共有 `numCourses` 门课需要选，记为 `0` 到 `numCourses - 1`。给你一个数组 `prerequisites` ，其中 `prerequisites[i] = [ai, bi]` ，表示在选修课程 `ai` 前 **必须** 先选修 `bi` 。

- 例如，想要学习课程 `0` ，你需要先完成课程 `1` ，我们用一个匹配来表示：`[0,1]` 。

返回你为了学完所有课程所安排的学习顺序。可能会有多个正确的顺序，你只要返回 **任意一种** 就可以了。如果不可能完成所有课程，返回 **一个空数组** 。

- **示例 1：**
- 输入：numCourses = 2, prerequisites = [[1,0]]
  输出：[0,1]
  解释：总共有 2 门课程。要学习课程 1，你需要先完成课程 0。因此，正确的课程顺序为 [0,1] 。

```c++
class Solution {
public:
    vector<int> findOrder(int numCourses, vector<vector<int>>& prerequisites) {
        vector<int>sub[numCourses];
        vector<int>in_degree(numCourses);
        vector<int>res;
        //构造树
        for (auto e : prerequisites)
        {
            sub[e[1]].push_back(e[0]);
            in_degree[e[0]]++;
        }
        queue<int>q;
        //放入入度为0的节点
        for (int i = 0; i < numCourses; i++)
        {
            if (!in_degree[i])
                q.push(i);
        }
        while (!q.empty())
        {
            int temp = q.front();
            q.pop();
            res.push_back(temp);
            for (auto j : sub[temp])
            {
                //如果相邻节点入度为0,就要添加进队列中
                if (--in_degree[j] == 0)
                    q.push(j);                
            }
        }
        if (res.size()!= numCourses)
            return {};
        return res;
    }
};
```

## [55. 跳跃游戏](https://leetcode.cn/problems/jump-game/)  贪心算法

- **示例 1：**
- 输入：nums = [2,3,1,1,4]
  输出：true
  解释：可以先跳 1 步，从下标 0 到达下标 1, 然后再从下标 1 跳 3 步到达最后一个下标。

```c++
class Solution 
{
public:
    bool canJump(vector<int>& nums) 
    {
        int len = nums.size(),reach=0;
        for (int i = 0; i < len; i++)
        {
            if (i > reach)
                return false;
            reach = max(reach, i + nums[i]);
        }
        return true;
    }
};
```

## [630. 课程表 III](https://leetcode.cn/problems/course-schedule-iii/)  优先队列+贪心反悔(有点回溯的意思)

```c++
class Solution {
public:
    int scheduleCourse(vector<vector<int>>& courses) {
        sort(courses.begin(), courses.end(), [](auto a, auto& b)
        {
            return a[1] < b[1];//根据结束时间排序
        });
        int needTime = 0;
        priority_queue<int>q;//优先队列,越大的数优先级越高 排序也就越靠前
        for (auto c : courses)
        {
            int tempTime=c[0],endTime=c[1];
            if (needTime +tempTime<=endTime)//如果修该门课需要的时间+已经耗费的时间<=这门课的结课时间
            {
                needTime+=tempTime;//将该门课程纳入学习范围
                q.push(tempTime);
            }
            else if (!q.empty() && tempTime < q.top())//需要的时间小于之前加入的最大时间 就要进行反悔
            {
                needTime -= q.top() - tempTime;//意思就是 减去之前的学习时间 加入现在的学习时间
                q.pop();
                q.push(tempTime);//加入现在的学习时间
            }
        }
        return q.size();
    }
};
```

## [2596. 检查骑士巡视方案](https://leetcode.cn/problems/check-knight-tour-configuration/)  回溯+迷宫

```c++
class Solution {
public:
    bool checkValidGrid(vector<vector<int>>& grid) {
        int direct[8][2] = { {2,1},{2,-1},{-2,1},{-2,-1},{1,2},{1,-2},{-1,2},{-1,-2} };
        int size = grid.size();
        int x = 0, y = 0;
        if (grid[x][y] != 0)
            return false;
        for (int i = 1; i < size * size; i++)
        {
            bool flag = true;
            for (auto d : direct)
            {
                 int now_x = d[0]+x;
                 int now_y = d[1]+y;
                 if (now_x >= 0 && now_x < size && now_y >= 0 && now_y < size && grid[now_x][now_y] == i)
                 {
                     x += d[0];
                     y += d[1];
                     flag = false;
                     break;
                 }
            }
            if (flag)
                return false;
        }
        return true;
    }
};
```

## [213. 打家劫舍 II](https://leetcode.cn/problems/house-robber-ii/) 动态规划

```c++
class Solution {
public:
   int rob(vector<int>& nums)
    {
       int len = nums.size();
        if (len == 1)
            return nums[0];
        vector<int>dp(len + 2);
        vector<int>dp2(len + 2);
        for (int i = 0; i < len-1 ; i++)
        {
            //偷第一家 [0,len-2)
            //由于未初始化,在max(dp[0]+nums[0],dp[1])时 就默认要偷第一家  在第二次时 是dp[1]+nums[1]和dp[2]也就是不偷第一家和偷第一家进行比较看是否有更好的结果
            dp[i+2] = max(dp[i] + nums[i], dp[i+1]);
        }
        //不偷第一家 [1,len)
        for (int i = 1; i < len; i++)
        {
            //不偷第一家从 dp2[2],dp2[1]+nums[1]也就是从第二家开始算 是否要偷
            dp2[i + 2] = max(dp2[i + 1], dp2[i] + nums[i]);
        }
        return max(dp2.back(),dp[len]);
    }

};
```



## [337. 打家劫舍 III](https://leetcode.cn/problems/house-robber-iii/) 树形dp

```c++
struct SubtreeStatus {
    int selected;
    int notSelected;
};

class Solution {
public:
    SubtreeStatus dfs(TreeNode* node) {
        if (!node) {
            return {0, 0};
        }
        auto l = dfs(node->left);
        auto r = dfs(node->right);
        int selected = node->val + l.notSelected + r.notSelected;
        int notSelected = max(l.selected, l.notSelected) + max(r.selected, r.notSelected);
        return {selected, notSelected};
    }

    int rob(TreeNode* root) {
        auto rootStatus = dfs(root);
        return max(rootStatus.selected, rootStatus.notSelected);
    }
};
//灵神的代码
class Solution {
    pair<int,int>dfs(TreeNode *node)
    {
        if(node==nullptr)
        return {0,0};
        auto [l_rob,l_not_rob]=dfs(node->left);//左子树递归
        auto [r_rob,r_not_rob]=dfs(node->right);//右子树递归
        int rob=l_not_rob+r_not_rob+node->val;//要抢劫
        int not_rob=max(l_rob,l_not_rob)+max(r_rob,r_not_rob);
        return {rob,not_rob};
    }
public:
    int rob(TreeNode* root) {
            auto [root_rob,root_not_rob]=dfs(root);
            return max(root_rob,root_not_rob);
    }
};
```

## [146. LRU 缓存](https://leetcode.cn/problems/lru-cache/)  双向链表+哨兵节点

```c++
class Node {
public:
    int key, value;
    Node *prev, *next;

    Node(int k = 0, int v = 0) : key(k), value(v) {}
};

class LRUCache {
private:
    int capacity;
    Node *dummy; // 哨兵节点
    unordered_map<int, Node*> key_to_node;

    // 删除一个节点（抽出一本书）
    void remove(Node *x) {
        x->prev->next = x->next;
        x->next->prev = x->prev;
    }

    // 在链表头添加一个节点（把一本书放在最上面）
    void push_front(Node *x) {
        x->prev = dummy;
        x->next = dummy->next;
        x->prev->next = x;
        x->next->prev = x;
    }

    Node *get_node(int key) {
        auto it = key_to_node.find(key);
        if (it == key_to_node.end()) // 没有这本书
            return nullptr;
        auto node = it->second; // 有这本书
        remove(node); // 把这本书抽出来
        push_front(node); // 放在最上面
        return node;
    }

public:
    LRUCache(int capacity) : capacity(capacity), dummy(new Node()) {
        dummy->prev = dummy;
        dummy->next = dummy;
    }

    int get(int key) {
        auto node = get_node(key);
        return node ? node->value : -1;
    }

    void put(int key, int value) {
        auto node = get_node(key);
        if (node) { // 有这本书
            node->value = value; // 更新 value
            return;
        }
        key_to_node[key] = node = new Node(key, value); // 新书
        push_front(node); // 放在最上面
        if (key_to_node.size() > capacity) { // 书太多了
            auto back_node = dummy->prev;
            key_to_node.erase(back_node->key);
            remove(back_node); // 去掉最后一本书
            delete back_node; // 释放内存
        }
    }
};
/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache* obj = new LRUCache(capacity);
 * int param_1 = obj->get(key);
 * obj->put(key,value);
 */
```

## [219. 存在重复元素 II](https://leetcode.cn/problems/contains-duplicate-ii/)   哈希表(索引+查找)

```java
class Solution {
    public boolean containsNearbyDuplicate(int[] nums, int k) {
          int len=nums.length;
            HashMap<Integer,Integer>hashMap=new HashMap<Integer,Integer>();
            for(int i=0;i<len;i++)
            {
                int num=nums[i];
                if(hashMap.containsKey(num)&&i-hashMap.get(num)<=k)
                    return true;
                hashMap.put(num,i);
                
            }
            return false;
    }
}
```

## [128. 最长连续序列](https://leetcode.cn/problems/longest-consecutive-sequence/) Set去重 add方法的返回 有值返回false 无值返回true

```java
class Solution {
    public int longestConsecutive(int[] nums) {
         int res=1;
            int len=nums.length;
            if(len==0)
            return 0;
            Arrays.sort(nums);
            Set<Integer>ts=new TreeSet<>();
            int tempRes=1;
            for(int i=1;i<len;i++)
            {
                //如果存在就继续
               if(!ts.add(nums[i]))
                   continue;
               if(nums[i]==nums[i-1]+1)
               {
                   tempRes++;
                   res=Math.max(tempRes,res);
               }
               else
                   tempRes=1;
            }
            return res;
    }
}
```

## [56. 合并区间](https://leetcode.cn/problems/merge-intervals/) 二维数组排序+二维数组的list集合

```java
class Solution {
    public int[][] merge(int[][] intervals) {
           Arrays.sort(intervals, new Comparator<int[]>() {
                @Override
                public int compare(int[] o1, int[] o2) {
                    return o1[0]-o2[0];
                }
            });
            int len=intervals.length;
            int i=0;
            List<int[]>merged=new ArrayList<int[]>();
            while(i<len)
            {
                int start=i;
                int num=intervals[start][1];
                while(i<len-1&&num>=intervals[i+1][0])
                {
                    i++;
                    num=Math.max(intervals[i][1],num);
                }
                if(start<i)
                {
                    int temp[]= {intervals[start][0],num};
                    merged.add(temp);
                }
                else
                {
                    int temp[]= {intervals[start][0],intervals[start][1]};
                    merged.add(temp);
                }
                i++;
            }
            return merged.toArray(new int[merged.size()][]);
    }
}
```

## [452. 用最少数量的箭引爆气球](https://leetcode.cn/problems/minimum-number-of-arrows-to-burst-balloons/) 解决因为数字过大导致排序无法正常进行的问题

```java
class Solution {
    public int findMinArrowShots(int[][] points) {
        List<int[]>list=new ArrayList<int[]>();
        	int len=points.length;
        	Arrays.sort(points,new Comparator<int []>() {
        		@Override
        		public int compare(int []o1,int []o2)
        		{
        			if(o1[0]>o2[0])
                        return 1;
                    else if(o1[0]<o2[0])
                        return -1;
                    else return 0;
        		}
        	});
        	int i=0;
        	while(i<len)
        	{
        		int start=i;
        		long num=points[start][1];
        		while(i<len-1&&num>=points[i+1][0])
        		{
        			i++;
        			num=Math.min(points[i][1], num);
        		}
        		int nums[]= {points[start][0],points[i][1]};
        		list.add(nums);
        		i++;
        	}
        	return list.size();
    }
}
```

```java
package test_01;
import java.util.*;
// 注意类名必须为 Main, 不要有任何 package xxx 信息
// 注意类名必须为 Main, 不要有任何 package xxx 信息
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scan = new Scanner(System.in);
        int n=scan.nextInt();
        int []x=new int[n];
        int [][]magic=new int[n-1][2];
        for(int i=0;i<n;i++)
        {
        	x[i]=scan.nextInt();
        }
        for(int i=0;i<n-1;i++)
        {
        	for(int j=0;j<2;j++)
        		magic[i][j]=scan.nextInt();
        }        
        //选择是否走向魔法阵传送
        double []dp=new double[n];
        //初始化dp数组
        for(int i=0;i<n;i++)
        	Arrays.fill(dp,Double.MAX_VALUE);
        dp[0]=x[0];
        int Mindex=0;
        int nowPosition[][]=new int[n][2];
        for(int i=0;i<n;i++)
        {
        	nowPosition[i][0]=0;
        	nowPosition[i][1]=0;
        }
        for(int i=1;i<n;i++)
        {
        	//使用魔法阵要考虑向上爬 向上只有0.7 也就是7/10;
        	//计算一下到达下一个魔法阵的时间
        	//要考虑第几次使用
        	System.out.println();
        	double down=(magic[Mindex][1]/(double)(13.0/10));
        	double up= magic[Mindex][1]/(double)(7.0/10);
        	double upOrDown=up+down;
        	double timeToMagic=magic[Mindex][0]-dp[i-1]+upOrDown;
        	//判断该线段上是否还有魔法阵
        	if(nowPosition[i-1][0]==magic[Mindex][0])
        	{
        		if(nowPosition[i-1][1]-magic[Mindex][1]==0)
        		{
        			up=0;
        			down=0;
        		}
        		else if(nowPosition[i-1][1]-magic[Mindex][1]>0)
        		{
        			up=0;
        		}
        		else 
        			down=0;
        		upOrDown=up+down;
        		timeToMagic=magic[Mindex][0]-nowPosition[i-1][0]+upOrDown;
        	}
        	if(down!=0||up!=0)
        		nowPosition[i][1]=magic[Mindex][1];
        	double timeNoMagic=x[i]-x[i-1]+(nowPosition[i-1][1]>0?down:0);
        	//使用魔法更快
        	if(timeToMagic<timeNoMagic&&magic[Mindex][0]-nowPosition[i-1][0]>=0&&upOrDown<timeNoMagic)
        	{
        		dp[i]=dp[i-1]+timeToMagic;
        		//y轴位置
        		nowPosition[i][1]=magic[Mindex][1];
        	}
        	else 
        		dp[i]=dp[i-1]+timeNoMagic;
        	//X轴位置
        	nowPosition[i][0]=x[i];
        	Mindex++;
        }
        System.out.printf("%.2f",dp[n-1]);
        //在此输入您的代码...
        scan.close();
    }
}
```

## 挑战赛 位运算

### 找可结合的元素对

```java
import java.util.*;
// 1:无需package
// 2: 类名必须Main, 不可修改

public class Main {
   public static void main(String[] args) {
    	Scanner scan = new Scanner(System.in);
    	int N=scan.nextInt();
    	int arr[]=new int[N];
    	long res=0;
    	for(int i=0;i<N;i++)
    		arr[i]=scan.nextInt();
    	HashMap<Integer,Integer>hm=new HashMap<Integer,Integer>();
    	for(int i=0;i<N;i++)
    	{
    		for(int j=0;j<32;j++)
    		{
    			int diff=(int)Math.pow(2,j)-arr[i];
    			res+=hm.getOrDefault(diff,0);
    		} 		
    		hm.put(arr[i],hm.getOrDefault(arr[i],0)+1);
    	}
    	System.out.println(res);
        //在此输入您的代码...
        scan.close();
    }
    
}
```

## [71. 简化路径](https://leetcode.cn/problems/simplify-path/) 栈

```java
class Solution {
    public String simplifyPath(String path) {
        String[]temp=path.split("/");
        	Deque<String>stack=new LinkedList();
        	for(String s:temp)
        	{
        		//先处理..的 因为要返回上级目录
        		if(("..".equals(s)))
        		{
        			if(!stack.isEmpty())
        			{
        				
        				stack.pollLast();
        			}
        		}
        		else if(!".".equals(s)&&s.length()>0)
        			stack.add(s);
        	}
        	StringBuilder sb=new StringBuilder();
        	if(stack.isEmpty())
        		sb.append('/');
        	else 
        	{
        		while(!stack.isEmpty())
            	{
            		sb.append('/');
            		sb.append(stack.poll());
            	}
        	}
        	return sb.toString();
    }
}
```

## [224. 基本计算器](https://leetcode.cn/problems/basic-calculator/) 栈 

```java
class Solution {
    public int calculate(String s) {
        int len = s.length();
            int res = 0;
            int sign = 1;
            Deque<Integer> dequeOperator = new LinkedList();
            dequeOperator.add(sign);
            for (int i = 0; i < len;) {
                if (s.charAt(i) == ' ') {
                    i++;
                    continue;
                } else if (s.charAt(i) == '-') {
                    i++;
                    sign = -dequeOperator.peekLast();
                } else if (s.charAt(i) == '+') {
                    i++;
                    sign = dequeOperator.peekLast();
                } else if (s.charAt(i) == '(') {
                    i++;
         
                    dequeOperator.add(sign);
                } else if (s.charAt(i) == ')') {
                    i++;
                    dequeOperator.pollLast();
                } else {
                    int num = 0;
                    while (i < len && Character.isDigit(s.charAt(i))) {
                        num = num * 10 + s.charAt(i) - '0';
                        i++;
                    }
                    res += sign * num;
                }
            }
            return res;
    }
}
```

## [141. 环形链表](https://leetcode.cn/problems/linked-list-cycle/) 快慢指针

```java
public class Solution {
    public boolean hasCycle(ListNode head) 
    {            
            if(head==null||head.next==null)
                return false;
            ListNode slow=head;
            ListNode fast=head.next;
            while(slow!=fast)
            {
            	if(fast==null||fast.next==null)
            		return false;
            	fast=fast.next.next;
            	slow=slow.next;
            }
            return true;
    }
}
```

## 飞机降落 dfs问题

```java
public class Main {
	static int N=15;
	static boolean st[]=new boolean[N];
	static Plane[] plane=new Plane[N];
    public static void main(String[] args) {
    	Scanner scan = new Scanner(System.in);
    	int T=scan.nextInt();
    	for(int i=0;i<T;i++)
    	{
    		//N是飞机数量
    		N=scan.nextInt();
    		for(int j=0;j<N;j++)
    		{
    			plane[j]=new Plane();
    			//到达时间
    			plane[j].Ti=scan.nextInt();
    			//盘旋时间
    			plane[j].Di=scan.nextInt();
    			//降落时间
    			plane[j].Li=scan.nextInt();
    		}
    		if(dfs(0,0))
				System.out.println("YES");
			else 
				System.out.println("NO");
			for(int x=0;x<N;x++)
				st[x]=false;
    	}
    	
    	
        //在此输入您的代码...
        scan.close();
    }
    //time表示前一架飞机的降落时间
    static boolean dfs(int planeNum,int time)
    {
    	//判断飞机的数量是否达标了
    	if(planeNum>=N)
    		return true;
    	for(int i=0;i<N;i++)
    	{
    		if(!st[i])
    		{
    			st[i]=true;
        		//无法降落情况 前一架飞机还未完成降落 现在这架飞机就已经到达且无法继续盘旋
        		if(plane[i].Ti+plane[i].Di<time)
        		{
        			//回溯
        			st[i]=false;
        			return false;
        		}
        		//可以降落 找到最大的降落时间
        		int temp=Math.max(time,plane[i].Ti)+plane[i].Li;
        		if(dfs(planeNum+1,temp))
        			return true;
        		//回溯
        		st[i]=false;
    		} 		
    	}
    	return false;
    }
    static class Plane
    {
    	public int Ti;
    	public int Di;
    	public int Li;
    }
```

## 利用BigInteger求阶乘

- BigInteger是继承Number的类，他可以计算比long还要大的单位
- 其中有pow方法 就是次方 还有multiply就是计算阶乘 这里的初始化是3 然后循环5次 也就是 1\*2\*3\*3\*4*5 如果正常求 就初始化为1
- 他的tostring(int index)方法是直接转换为index进制的string字符串

```java
public static void main(String[] args) {
    	 
    	 long sum=1;
    	 long ssum=1;
    	 BigInteger bInteger=new BigInteger("3");
    	 for(int i=1;i<=5;i++)
    	 {
    		 BigInteger b= BigInteger.valueOf(i);
    		 System.out.println("b="+b);
    		 bInteger=bInteger.multiply(b);
    		 System.out.println("multiply:"+bInteger);
    	 }
    	 System.out.println("BIT="+bInteger);
    	 	System.out.println(bInteger.toString(2).length());

 
    }
```

## 简单dfs  地图问题

- 9 6
  ....#.
  .....#
  ......
  ......
  ......
  ......
  ......
  #@...#
  .#..#.

  .黑色 @红色 
  @我所站的地方
  上下左右开始走 
  合法状态 ：黑色
  答案是45

```java
public class Main {
	//上右下左
	static int dir[][]= {{-1,0},{0,+1},{1,0},{0,-1}};
	static int ans=0;
    public static void main(String[] args) {
    	 Scanner scan = new Scanner(System.in);
    	 int line=scan.nextInt();
    	 int row=scan.nextInt();
    	 char [][]maze=new char[line][row];
    	 for(int i=0;i<line;i++)
    		 //直接转换成字符数组
    		 maze[i]=scan.next().toCharArray();
    	 for(int i=0;i<line;i++)
    	 {
    		 for(int j=0;j<row;j++)
    		 {
    			 //寻找初始开始位置 找到后就进入dfs
    			 if(maze[i][j]=='@')
    				 dfs(i,j,maze);
    		 }
    	 }
    	 System.out.println(ans);
         scan.close();
    }
    static void dfs(int x,int y,char maze[][])
    {
    	//能够进入说明是合法状态
    	ans++;
    	maze[x][y]='#';
    	//然后进行搜索 只用判断四个方向搜索就行
    	for(int i=0;i<4;i++)
    	{
    		int nx=x+dir[i][0];
    		int ny=y+dir[i][1];
    		//到新地方后判断是否合法
    		//不合法就继续找新地方
    		if(nx<0||nx>=maze.length||ny<0||ny>=maze[0].length||maze[nx][ny]!='.')
    			continue;
    		//合法
    		dfs(nx,ny,maze);
    	}
    }
}
```

## 简单回溯（全排列）

```java
public class Main {
	//存放答案
	static List<List<Integer>> ansList=new ArrayList();
    public static void main(String[] args) {
    	 Scanner scan = new Scanner(System.in);
    	 //1-n的数字全排列
    	 int n=scan.nextInt();
    	 //判断是否合法
    	 int []visit=new int[n+1];
    	 List<Integer>list=new ArrayList();
    	 dfs(n,visit,list);
    	 for(List<Integer> list2:ansList)
    	 {
    		 for(Integer ans:list2)
    			 System.out.print(ans+" ");
    		 System.out.println();
    	 }
         scan.close();
    }
    static void dfs(int n,int []v,List<Integer>list)
    {
    	//找到一组答案
    	if(list.size()==n)
    	{
    		ansList.add(new ArrayList(list));
    		return;
    	}
    	//从1开始
    	for(int i=1;i<=n;i++)
    	{
    		//先找不合法情况
    		if(v[i]==1)
    			continue;
    		//然后找合法
    		v[i]=1;
    		list.add(i);
    		dfs(n,v,list);
    		//找完一组后开始回溯
    		v[i]=0;
    		list.remove(list.size()-1);
    	}
    }
}
```

## 回溯+dfs  和前面的1-9选数很像

```java
public class Main {
  static long maxLong=Long.MIN_VALUE,minLong=Long.MAX_VALUE;
    public static void main(String[] args) {
       Scanner scan = new Scanner(System.in);
    	 char []c=scan.next().toCharArray();
    	 int k=scan.nextInt();
    	 //dfs中需要的参数 当前位置 剩余的+号 拼接的string
    	 StringBuilder sb=new StringBuilder();
    	 dfs(c,k,0,sb);
    	 long res=maxLong-minLong;
    	 System.out.println(res);
         scan.close();
    }
     static void dfs(char c[],int k,int nowPos,StringBuilder s)
    {
    	//先找到退出逻辑
    	//当+号字符没有了 或者是到最后一位数字了
    	if(nowPos==c.length)
    	{
    		//没有+号 并且是最后一位数字了 才开始拼接
    		if(k==0)
    		{
    			//通过字符串分割找到每组数字
    			String []sArr=s.toString().split("\\+");
    			//开始计算值
    			long res=0;
    			for(String x:sArr)
    				res+=Long.valueOf(x);
    			maxLong=Math.max(maxLong,res);
    			minLong=Math.min(minLong,res);
    		}
    		return ;
    	}
    	//符合要求
    	s.append(c[nowPos]);
    	dfs(c,k,nowPos+1,s);
    	s.deleteCharAt(s.length()-1);
    	//判断是否还有+以及是否还有数字 
    	if(k>0&&nowPos<c.length-1)
    	{
    		s.append(c[nowPos]);
    		s.append('+');
    		dfs(c,k-1,nowPos+1,s);
    		s.deleteCharAt(s.length()-1);
    		s.deleteCharAt(s.length()-1);
    	}
    	
    	
    }
}
```

## dfs 扩散 找距离是否在范围内

```java
public class Main {
	static int N=1020;
	static int d;
	static int coordinate[][]=new int [N][2];
	//0代表没人 1代表有人 2代表感染
	static int isInfect[]=new int[N];
	static int num=0;
    public static void main(String[] args) {
    	 Scanner scan = new Scanner(System.in);
    	 N=scan.nextInt();
    	 Arrays.fill(isInfect,0);
    	 for(int i=0;i<N;i++)
    	 {
    		coordinate[i][0]=scan.nextInt();
    		coordinate[i][1]=scan.nextInt();
    	 }
    	 d=scan.nextInt();
    	 //第一位已经被感染
    	 isInfect[0]=1;
    	 //传入x,y,传染距离
    	 dfs(0);
    	 for(int i=0;i<N;i++)
    	 {
    			System.out.println(isInfect[i]);
    	 }
         scan.close();
    }
    static void dfs(int x)
    {
    	int nx=coordinate[x][0];
    	int ny=coordinate[x][1];
    	//其实就是计算下一个位置是不是在当前感染区域 
    	//如果在就感染 然后带入下一个感染区域接着感染
    	//所以先计算当前区域
    	for(int i=0;i<N;i++)
    	{
    		if(isInfect[i]==1)
    			continue;
    		int distance=(coordinate[i][0]-nx)*(coordinate[i][0]-nx)+(coordinate[i][1]-ny)*(coordinate[i][1]-ny);
    		if(distance<=d*d)
    		{
    			isInfect[i]=1;
        		dfs(i);
    		}
    	}
    	
    	
    }
}
```

## dfs 收集问题 和迷宫很像

```java
import java.util.Scanner;
// 1:无需package
// 2: 类名必须Main, 不可修改

public class Main {
    static int dire[][]= {{-1,0},{1,0},{0,-1},{0,1}};
	static int N=101,M=101;
	static long res=0;
	static long getWater=0;
	static int isWater[][]=new int[N][M];
    public static void main(String[] args) {
    	 Scanner scan = new Scanner(System.in);
    	 N=scan.nextInt();
    	 M=scan.nextInt();
    	 int arr[][]=new int [N][M];

    	 for(int i=0;i<N;i++)
    	 {
    		 for(int j=0;j<M;j++)
    		 {
    			 arr[i][j]=scan.nextInt();
    		 }
    	 }
    	 //寻找开始位置
    	 for(int i=0;i<N;i++)
    	 {
    		 for(int j=0;j<M;j++)
    		 {
    			 if(arr[i][j]!=0&&isWater[i][j]==0)
    				dfs(i,j,arr);
    			 getWater=0;
    		 }
    	 }
    	 System.out.println(res);
         scan.close();
    }
    static void dfs(int x,int y,int [][]arr)
    {
    	
    	getWater+=arr[x][y];
    	//进来就收集 并且标记
    	isWater[x][y]=1;
    	//往下一步走
    	for(int i=0;i<4;i++)
    	{
    		int nx=x+dire[i][0];
    		int ny=y+dire[i][1];
    		//寻找下一个有水的地方
    		if(nx<0||nx>=arr.length||ny<0||ny>=arr[0].length||arr[nx][ny]==0||isWater[nx][ny]==1)
    			continue;
    		//合法 继续dfs
    		dfs(nx,ny,arr);
    	}
    	res=Math.max(res,getWater);
}
}
```

## dfs+回溯 寻找操作 （这类问题基本都是需要一个visit来查看操作是否还可以进行 ）

- 一般进行操作的都需要在循环中进行 循环结束后 找到一次完整的搜索结果 然后在每次寻找完一次完整结果后进行判断是否有正确的值进行返回

```java
import java.util.*;
// 1:无需package
// 2: 类名必须Main, 不可修改

public class Main {
   static int count=0;
	static int visit[];
    public static void main(String[] args) {
    	 Scanner scan = new Scanner(System.in);
    	 int n=scan.nextInt();
    	 char[]arr1=scan.next().toCharArray();
    	 char[]arr2=scan.next().toCharArray();
    	 int k=scan.nextInt();
    	 int [][]op=new int[k][3];
    	 visit=new int[k];
    	 for(int i=0;i<k;i++)
    	 {
    		 op[i][0]=scan.nextInt();
    		 op[i][1]=scan.nextInt();
    		 op[i][2]=scan.nextInt();
    	 }
    	 count=k;
    	 if(dfs(arr1,arr2,k,op))
    		 System.out.println("Yes");
    	 else 
    		 System.out.println("No");
    	 
    	 
         scan.close();
    }
    static boolean dfs(char[]arr1,char []arr2,int k,int [][]op)
    {
    	//结束条件
    	if(Arrays.equals(arr1,arr2))
    		return true;
    	//查询可执行的操作
    	for(int i=0;i<k;i++)
    	{
    		if(visit[i]==1)
    			continue;
    		if(op[i][0]==2)
        	{
        		swap(arr1,op[i][1],op[i][2]);
        	}
        	else if(op[i][0]==1)
        	{
        		int num=arr1[op[i][1]]-'0';
        		int num2=op[i][2];
        		int res=(num+num2)%10;
        		arr1[op[i][1]]=(char)(res+'0');
        	}
    		visit[i]=1;
    		//查看是否还可以操作
    		count--;
    		if(dfs(arr1,arr2,k,op))
    			return true;
    		//回溯
    		visit[i]=0;
    		count++;
    	}
    	return false;
    }
    static void swap(char []arr1,int Sx,int Sy)
    {
    	char temp=arr1[Sx];
    	arr1[Sx]=arr1[Sy];
    	arr1[Sy]=temp;
    }
}
```

## dfs+回溯  1-9选择问题

```java
static int count=0;
	static int visit[];
	static char op[]= {'*','+','-','/'};
	static char ischose[];
	static int res=0;
	static int n=10;
    public static void main(String[] args) {
    	 Scanner scan = new Scanner(System.in);
    	 n=scan.nextInt();
    	 int arr[]=new int[n];
    	 visit=new int[4];
    	 ischose=new char[n+1];
    	 count=n;
    	 for(int i=0;i<n;i++)
    		 arr[i]=scan.nextInt();
    	 StringBuilder sb=new StringBuilder();
    	 visit[0]=1;
    	 res+=arr[0];
    	 if(dfs(sb,res,arr,1))
    	 {
    		 System.out.println(sb);
    		 System.out.println("YES");
    		 
    	 }
    	 else 
    		 System.out.println("NO");
         scan.close();
    }
    static boolean dfs(StringBuilder sb,int res,int []arr,int i)
    {
    	if(i==arr.length)
    	{
    		//找到结果开始拼接
    		if(res==24)
    		{
    			for(int j=0;j<n;j++)
    			{
    				if(j!=0)
    				sb.append(ischose[j]);
    				sb.append(arr[j]);
    			}
    			return true;
    		}
    		return false;
    	}
    	//比如先选择了*
    	res=res*arr[i];
    	ischose[i]='*';
    	if(dfs(sb,res,arr,i+1))
    		return true;
    	//回溯
    	res/=arr[i];
    	//选了+号
    	res+=arr[i];
    	ischose[i]='+';
    	if(dfs(sb,res,arr,i+1))
    		return true;
    	res-=arr[i];
    	//-号
    	res-=arr[i];
    	ischose[i]='-';
    	if(dfs(sb,res,arr,i+1))
    		return true;
    	res+=arr[i];
    	// /号
    	res/=arr[i];
    	ischose[i]='/';
    	if(dfs(sb,res,arr,i+1))
    		return true;
    	res*=arr[i];
    	return false;
    }
 }
```


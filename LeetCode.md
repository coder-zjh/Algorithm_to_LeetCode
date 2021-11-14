# LeetCode

> LeetCode刷题笔记，语言Java，记录刷题过程中的某些思路、代码、涉及知识点和解题Tips。

## Easy

#### [1. 两数之和](https://leetcode-cn.com/problems/two-sum/)

1. 双循环嵌套做法，思路直接但较低效，代码略。

2. 哈希表做法，利用hash表存放数组的值与下标，如果target减去当前数组值的所得结果在哈希表中，则得出答案。

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        HashMap<Integer,Integer> hm = new HashMap<>();
        for(int i=0;i<nums.length;i++){
            if(hm.containsKey(target-nums[i])){
                return new int[]{hm.get(target-nums[i]),i};
            }else{
                hm.put(nums[i],i);
            }
        }
        return new int[]{0};
    }
}
```

#### [7. 整数反转](https://leetcode-cn.com/problems/reverse-integer/)

1. 字符串做法，直接利用StringBuffer的reverse()方法，利用api不训练码力，代码略。
2. 数学做法，具体解释见TSP：从后向前还原数字的代码。

```java
class Solution {
    public int reverse(int x) {
        long n = 0;
        // 3、当x是0的时候，说明输入数已经从后往前还原完毕
        while(x!=0){
            // 1、这个公式将不断从后往前还原输入数x
            n = n*10+x%10;
            // 2、如果当前数小于10，则/10后等于0
            x = x/10;
        }
        // 此时n就是反转之后的x
        return (int)n==n?(int)n:0;
    }
}
```

#### [9. 回文数](https://leetcode-cn.com/problems/palindrome-number/)

1. 字符串做法，直接利用StringBuffer的reverse()方法，利用api不训练码力，代码略。
2. 数学做法，具体解释见TSP：从后向前还原数字的代码。

```java
class Solution {
    public boolean isPalindrome(int x) {
        if(x==0){
            return true;
        }
        if(x<0||x%10==0){
            return false;
        }
        int reversed = 0;
        // reversed是从后往前复现这个数
        while(x>reversed){
            reversed = reversed*10+x%10;
            x/=10;
        }
        //如果复现的数和x相等的话，则倒推和正推是相等的，即是回文数
        return x==reversed||x==reversed/10;

    }
}
```

#### [13. 罗马数字转整数](https://leetcode-cn.com/problems/roman-to-integer/)

找到罗马数字组成的规律，就很好解决。

```java
class Solution {
    public int romanToInt(String s) {
        // 规律是：从左到右，如果前一个数小于后一个数，则后数减去前数;反之前数加后数
        int result = 0;
        int preNum = getValue(s.charAt(0));
        for(int i=1;i<s.length();i++){
            int num = getValue(s.charAt(i));
            if(preNum < num){
                result = result-preNum;
            }else{
                result = result+preNum;
            }
            preNum = num;
        }
        result += preNum;
        return result;
    }
  
// 先做好字母与数字的映射
    public int getValue(char x){
        switch(x){
            case 'I':return 1;
            case 'V':return 5;
            case 'X':return 10;
            case 'L':return 50;
            case 'C':return 100;
            case 'D':return 500;
            case 'M':return 1000;
            default: return 0;
        }
    }
}
```

#### [14. 最长公共前缀](https://leetcode-cn.com/problems/longest-common-prefix/)



```java
class Solution {
    public String longestCommonPrefix(String[] strs) {
        if(strs.length==0){
            return "";
        }
        // 理解这句话：公共前缀比所有字符串都短，所以可以随便选一个
        // 随便先选第一个字符串的值作为公共前缀
        String s = strs[0];
        // 遍历每一个数组元素
        for(String str:strs){
            while(!str.startsWith(s)){
                //如果公共前缀的长度被缩小到0，退出，说明没有公共前缀
                if(s.length()==0){
                    return "";
                }
                //继续缩小公共前缀的范围
                s = s.substring(0,s.length()-1);
            }
        }
        return s;
    }
}
```

#### [20. 有效的括号](https://leetcode-cn.com/problems/valid-parentheses/)

利用栈，遍历字符串中每个字符，遇到题中所提字符，则用栈存放该字符的对应字符，如果下一个字符与栈中最新元素相等，则说明匹配上了，而如果栈是空，则说明出现了非所提字符的情况，或是下一个字符与栈中最新元素不等，则说明出现了不匹配的情况。

```java
class Solution {
    public boolean isValid(String s) {
        Stack<Character> stack = new Stack<Character>();
        // 遍历字符串的每一个字符
        // 遇到([]{时，在栈中记录下需匹配的字符，继续向下匹配，
        // 如果下一个字符是栈中最新的字符，则表示下一个字符与上一个字符匹配，继续向下遍历
        for(char c: s.toCharArray()){
            if(c=='('){
                stack.push(')');
            }
            else if(c=='['){
                stack.push(']');
            }
            else if(c=='{'){
                stack.push('}');
            }
            // stack.isEmpty()：字符串中不存在左半部分
            // c!=stack.pop()：当目前字符与栈中不匹配时，则退出
            else if(stack.isEmpty()||c!=stack.pop()){
                return false;
            }
        }
        return stack.isEmpty();
    }
}
```

#### [58. 最后一个单词的长度](https://leetcode-cn.com/problems/length-of-last-word/)

1. 
2. 从后往前的做法

```java
class Solution {
    public int lengthOfLastWord(String s) {
      // 去首尾空格后，从后往前推，遇到第一个空格为止，则最后一个单词就在这个范围内
        s = s.trim();
        return s.length()-s.lastIndexOf(" ")-1;
    }
}
```

#### [70. 爬楼梯](https://leetcode-cn.com/problems/climbing-stairs/)

```java
class Solution {
    public int climbStairs(int n) {
        int a = 1,b=2,tmp;
        if(n<=2){
            return n;
        }
        for(int i=3;i<=n;i++){
            tmp=a;
            a=b;
            b=tmp+b;
        }
        return b;
    }
}
```

#### [121. 买卖股票的最佳时机](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock/)

DP做法，

```java
class Solution {
    public int maxProfit(int[] prices) {
        if(prices.length <= 1)
            return 0;
        //截止到当日，最小的价格min，因为第一天，所以最小的价格就是第一天的价格
        //截止到当日，最大的差值max，因为第一天还没卖，所以最大价差还是0
        int min = prices[0], max = 0;
        // 从第二天开始，将之前的最大价差，与(今日价格-之前最低价)做比较，留下比较后的最大价差
        // 然后，比较今日价格与之前的最低价，留下比较后的最低价
        // 注意，max要先算，不能在min更新后再计算max
        for(int i = 1; i < prices.length; i++) {
            max = Math.max(max, prices[i] - min);
            min = Math.min(min, prices[i]);
        }
        return max;
    }
}
```

#### [136. 只出现一次的数字](https://leetcode-cn.com/problems/single-number/)

```java
class Solution {
    public int singleNumber(int[] nums) {
        // 如果a、b两个值不相同，则异或结果为1。如果a、b两个值相同，异或结果为0。
        // 不需要额外空间的方法，就往位运算上想
        // 异或运算有以下三个性质：
        // 1、任何数和 0 做异或运算，结果仍然是原来的数
        // 2、任何数和其自身做异或运算，结果是 0
        // 3、异或运算满足交换律和结合律

        return Arrays.stream(nums).reduce((a,b)->a^b).getAsInt();
    }
}
```

#### [169. 多数元素](https://leetcode-cn.com/problems/majority-element/)

```java
class Solution {
    public int majorityElement(int[] nums) {
        // 摩尔投票法
        /**
        思路：三国交战，且交战时，每个士兵都和一个士兵同归于尽。
        假设我国人数大于三国总人数的一半，遇到一个敌方士兵减一，遇到己方士兵加一
        按这个算法，遍历到最后，我方人数一定是大于0，
        ===========================================================================
        疑问：为什么等于0的时候要换数？
        解答：等于0的时候说明之前选定的国至此已全部抵消，后面如果这个国人数还是占优，那最后还是这个国胜利
             那就先看当前这个国能撑多久。
         */
        int cnt = 1;
        int role = nums[0];
        for(int i=1;i<nums.length;i++){
            if(role==nums[i]){
                cnt++;
            }else{
                cnt--;
            }
            if(cnt==0){
                role = nums[i];
                cnt = 1;
            }
        }
        return role;
    }
}
```

#### [509. 斐波那契数](https://leetcode-cn.com/problems/fibonacci-number/)

1. 递归做法

```java
// 有多种做法
class Solution {
    public int fib(int n) {
        if(n<=1){
            return n;
        }
        return fib(n-1)+fib(n-2);
    }
}
```

2. DP做法

```java
```



#### [1118. 一月有多少天](https://leetcode-cn.com/problems/number-of-days-in-a-month/)

这题不讨论，主要是对闰年及其所属月份的了解。

```java
class Solution {
    public int numberOfDays(int Y, int M) {
        int[] runnian = {31, 29, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31}; // 闰年
        int[] norunnian = {31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31}; // 非闰年
        if((Y % 100 != 0 && Y % 4 == 0) || Y % 400 == 0) {
            return runnian[M-1];
        }
        return norunnian[M-1];
    }
}
```

#### [217. 存在重复元素](https://leetcode-cn.com/problems/contains-duplicate/)

1. 去重做法，去重后长度小于原长度，则表明存在重复值。

```java
class Solution {
    public boolean containsDuplicate(int[] nums) {
        Set<Integer> s = new HashSet<>();
        for(int num:nums){
            s.add(num);
        }
        return s.size()<nums.length?true:false;
    }
}
```

#### [1876. 长度为三且各字符不同的子字符串](https://leetcode-cn.com/problems/substrings-of-size-three-with-distinct-characters/)

```java
class Solution {
    public int countGoodSubstrings(String s) {
        if(s.length()<3){
            return 0;
        }
        int count =0;
        //注意循环结束条件的取值范围,指针只要取到倒数第三位即可
        for(int i=0;i<s.length()-2;i++){
            if((s.charAt(i)!=s.charAt(i+1))&&(s.charAt(i+1)!=s.charAt(i+2))&&(s.charAt(i)!=s.charAt(i+2))){
                count++;
            }
        }
        return count;
    }
}
```

#### [LCP 01. 猜数字](https://leetcode-cn.com/problems/guess-numbers/)

不讨论，较为简单。

```java
class Solution {
    public int game(int[] guess, int[] answer) {
        int count = 0;
        for(int i=0;i<3;i++){
            if(guess[i]==answer[i]){
                count++;
            }
        }
        return count;
    }
}
```

#### [1085. 最小元素各数位之和](https://leetcode-cn.com/problems/sum-of-digits-in-the-minimum-number/)

先得出数组最小值，然后根据TSP：从后向前还原数字的代码 做各数位加和，最后判断奇偶。

```java
class Solution {
    public int sumOfDigits(int[] nums) {
        int min = nums[0];
      // 需要了解一下为什么不用Arrays.sort()?
        for(int i=0;i<nums.length;i++){
            min = Math.min(min,nums[i]);
        }
        int sum=0;
        while(min!=0){
            sum+=min%10;
            min/=10;
        }
        return sum%2==0?1:0;
    }
}
```

#### [1119. 删去字符串中的元音](https://leetcode-cn.com/problems/remove-vowels-from-a-string/)

不讨论，利用正则即可。

```java
class Solution {
    public String removeVowels(String s) {
        // 正则做法
        return s.replaceAll("[aeiou]","");
    }
}
```

#### [LCP 17. 速算机器人](https://leetcode-cn.com/problems/nGK0Fy/)

较简单，不讨论。

```java
class Solution {
    public int calculate(String s) {
        int x=1,y=0;
        for(char c:s.toCharArray()){
            if(c=='A'){
                x = 2*x+y;
            }else{
                y = 2*y+x;
            }
        }
        return x+y;
    }
}
```

#### [2000. 反转单词前缀](https://leetcode-cn.com/problems/reverse-prefix-of-word/)

```java
class Solution {
    public String reversePrefix(String word, char ch) {
        int ind = word.indexOf(ch);
        StringBuffer s = new StringBuffer(word.substring(0,ind+1));
    return s.reverse().append(word.substring(ind+1)).toString();
    }   
}
```

#### [2011. 执行操作后的变量值](https://leetcode-cn.com/problems/final-value-of-variable-after-performing-operations/)

较简单，不讨论。

```java
class Solution {
    public int finalValueAfterOperations(String[] operations) {
        int x = 0;
        for(String t:operations){
            if(t.contains("+")){
                x++;
            }else{
                x--;
            }
        }
        return x;
    }
}
```

#### [1491. 去掉最低工资和最高工资后的工资平均值](https://leetcode-cn.com/problems/average-salary-excluding-the-minimum-and-maximum-salary/)

排序，然后加和范围是去掉最大最小值的中间那些数。

```java
class Solution {
    public double average(int[] salary) {
        Arrays.sort(salary);
        int sum=0;
        for(int i=1;i<salary.length-1;i++){
            sum+=salary[i];
        }
        return sum/(salary.length-2.0);
    }
}
```

#### [1550. 存在连续三个奇数的数组](https://leetcode-cn.com/problems/three-consecutive-odds/)

计数思路，遇到奇数就加1，当计数cnt到达3就退出。

```java
class Solution {
    public boolean threeConsecutiveOdds(int[] arr) {
        int cnt = 0;
        for(int a:arr){
            if(a%2!=0){
                cnt++;
            }else{
                cnt=0;
            }
            if(cnt==3){
                return true;
            }
        }
        return false;
    }
}
```

#### [441. 排列硬币](https://leetcode-cn.com/problems/arranging-coins/)

当前硬币数大于等于下一层阶梯的位置数时，则当前硬币数为可排满下一层，如不满足，返回上一层台阶的序号。

```java
class Solution {
    public int arrangeCoins(int n) {
        // 每层可放置的个数，同时也是台阶序号
        int cnt = 1;
        while(n>=cnt){
            n = n-cnt;
            cnt++;
        }
        return cnt-1;
    }
}
```

#### [485. 最大连续 1 的个数](https://leetcode-cn.com/problems/max-consecutive-ones/)

遍历数组，当遇到1时计数，遇到0时说明1的序列断开，此时统计下max，同时计数清零。循环结束后，拿此时的cnt和统计的max再做一次比较。

```java
class Solution {
    public int findMaxConsecutiveOnes(int[] nums) {
        int cnt = 0;
        int max = 0;
        for(int i:nums){
            if(i==1){
                cnt++;
            }else{
                max = Math.max(max,cnt);
                cnt=0;
            }
        }
        return Math.max(max,cnt);
    }
}
```

#### [LCP 06. 拿硬币](https://leetcode-cn.com/problems/na-ying-bi/)

找到规律的做法

```java
class Solution {
    public int minCount(int[] coins) {
        int cnt = 0;
        for(int i:coins){
            if(i%2==0){
                cnt+=i/2;
            }else{
                cnt+=i/2+1;
            }
        }
        return cnt;
    }
}
```

另一种办法，

```java
class Solution {
    public int minCount(int[] coins) {
        int cnt = 0;
        for(int i:coins){
            while(i>0){
                cnt++;
                i-=2;
            }
        }
        return cnt;
    }
}
```

#### [1281. 整数的各位积和之差](https://leetcode-cn.com/problems/subtract-the-product-and-sum-of-digits-of-an-integer/)

利用TSP：从后向前还原数字的代码的思路。

```java
class Solution {
    public int subtractProductAndSum(int n) {
        int ji = 1,he = 0;
        while(n!=0){
            ji *= n%10;
            he += n%10;
            n/=10;
        }
        return ji-he;
    }
}
```

#### [1295. 统计位数为偶数的数字](https://leetcode-cn.com/problems/find-numbers-with-even-number-of-digits/)

1. String.valueOf()方法，不提升码力，代码略。
2. 使用TSP：从后往前还原数字的代码 的思路。

```java
class Solution {
    public int findNumbers(int[] nums) {
        //偶数个数的计数
        int cnt =0;
        for(int i:nums){
            // 位数的计数n
            int n  = 0;
            while(i>0){
                i/=10;
                n++;
            }
            cnt+=n%2==0?1:0;//这种风格可以学下
        }
        return cnt;
    }
}
```

#### [1323. 6 和 9 组成的最大数字](https://leetcode-cn.com/problems/maximum-69-number/)

要最大数字，肯定是把高位的6改成9。利用String类的replaceFirst方法。

```java
class Solution {
    public int maximum69Number (int num) {
        return Integer.valueOf(String.valueOf(num).replaceFirst("6","9"));
    }
}
```

#### [1475. 商品折扣后的最终价格](https://leetcode-cn.com/problems/final-prices-with-a-special-discount-in-a-shop/)

1. 双循环做法，比较直观，易理解。

```java
class Solution {
    public int[] finalPrices(int[] prices) {
        for(int i=0;i<prices.length-1;i++){
            for(int j=i+1;j<prices.length;j++){
                if(prices[i]>=prices[j]){
                    prices[i] -=prices[j];
                    break;
                }
            }
        }
        return prices;
    }
}
```

2. 单调栈做法，学习一下

```java
class Solution {
    public int[] finalPrices(int[] prices) {
        Stack<Integer> s=new Stack<>();
        for(int i=0;i<prices.length;i++){
            //能在栈里面呆着说明还没找到右边第一个比它小的
            while(!s.isEmpty()&&prices[s.peek()]>=prices[i]){
                prices[s.pop()]-=prices[i];
            }
            s.push(i);
        }
        return prices;
    }
}
```







## Medium







## Hard







## Tips Of Solving Problems

#### 摩尔投票法

待完成...

#### 从后向前还原数字的代码

```java
//原数字
int x = 1023;
//逆向还原的数字
int n = 0;
/**
 * 主逻辑：从原数字最后一位开始，每经过一次循环，复现从后往前数的n位数字
 *             n     x
 * 进入循环时    0    1023
 * ================================================
 *            n*10+x%10             x/10     n      x
 * 第一次循环      3                  102     3      102
 * 第二次循环   3*10+102%10=32        10      32     10
 * 第三次循环   32*10+10%10=320       1       320     1
 * 第四次循环   320*10+1%10=3201      0       3201    0
 */
while (x != 0) {
    /**
     * 每执行一次，就是将n升一个数位再加上x的最后一位
     * 本质上是不断追加原数字的高位数字，从而逆向还原原数字
     */
    n = n * 10 + x % 10;
    /**
     * 效果上是，从后往前，每次截去原数字的最后一位，如果只有个位数了，就返回0，
     * 同时，如果到这个式子，x只有个位数了，
     * 则说明上面那个式子的"x % 10"中，x已经到了原数据的最高位，所以用x!=0判断未到达最高位
     * 本质上就是不断去除原数据的低位数字。
     */
    x = x / 10;
    System.out.println(n + "====" + x);
}
System.out.println("n=" + n);//3201
```

#### 欧几里得算法/辗转相除法

```java
/**
 * 欧几里得算法是用来求两个正整数最大公约数的算法。古希腊数学家欧几里得在其著作《The Elements》中最早描述了这种算法,所以被命名为欧几里得算法。
 * 扩展欧几里得算法可用于RSA加密等领域。
 * 假如需要求 1997 和 615 两个正整数的最大公约数,用欧几里得算法，是这样进行的：
 * 1997 / 615 = 3 (余 152)
 * 615 / 152 = 4(余7)
 * 152 / 7 = 21(余5)
 * 7 / 5 = 1 (余2)
 * 5 / 2 = 2 (余1)
 * 2 / 1 = 2 (余0)
 * 至此，最大公约数为1
 * 以除数和余数反复做除法运算，当余数为 0 时，取当前算式除数为最大公约数，所以就得出了 1997 和 615 的最大公约数 1。
 */
int gcd(int m,int n)
{   if(n == 0){
        return m; 
    }
    int r = m%n;
    return gcd(n,r);
}
```



## 题中涉及的Java知识点

#### Arrays.sort()详解



## 常用代码片段

#### test


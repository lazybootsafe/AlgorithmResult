# LeetCode 122  |    买卖股票的最佳时机 II

+++

## 原题地址

<https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-ii/>



## 题意

给定一个数组，它的第 i 个元素是一支给定股票第 i 天的价格。

设计一个算法来计算你所能获取的最大利润。你可以尽可能地完成更多的交易（多次买卖一支股票）。

注意：你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。

 

示例 1:

~~~
输入: [7,1,5,3,6,4]
输出: 7
解释: 在第 2 天（股票价格 = 1）的时候买入，在第 3 天（股票价格 = 5）的时候卖出, 这笔交易所能获得利润 = 5-1 = 4 。
     随后，在第 4 天（股票价格 = 3）的时候买入，在第 5 天（股票价格 = 6）的时候卖出, 这笔交易所能获得利润 = 6-3 = 3 。
~~~

示例 2:

~~~
输入: [1,2,3,4,5]
输出: 4
解释: 在第 1 天（股票价格 = 1）的时候买入，在第 5 天 （股票价格 = 5）的时候卖出, 这笔交易所能获得利润 = 5-1 = 4 。
     注意你不能在第 1 天和第 2 天接连购买股票，之后再将它们卖出。
     因为这样属于同时参与了多笔交易，你必须在再次购买前出售掉之前的股票。
~~~

示例 3:

~~~
输入: [7,6,4,3,1]
输出: 0
解释: 在这种情况下, 没有交易完成, 所以最大利润为 0。
~~~





## 题解

解法一、贪心算法1
贪心算法(greedy algorithm)就是这样的算法，它在每一步都做出当时看起来最佳的选择，
也就是说，它总是做出局部最优的选择，寄希望这样的选择能导致全局最优解。

~~~
算法设计：
今天持股票   ：如果明天涨，继续持有不卖，如果明天跌，今天卖出，不持有
今天不持有股票： 如果明天涨，今天买入，如果明天跌，继续不持有
~~~

代码如下：

~~~c

int maxProfit(int* prices, int pricesSize) {
    if(pricesSize<2)
        return 0;
	int res = 0;//收益
	int cur = 0;//1:持有股票,0: 不持有
	for (int i = 0; i < pricesSize - 1; i++)
	{
		//卖出：如果持有，且明天股票跌(第1天不能卖，第一天cur=0)
		if (cur ==1 && (prices[i] > prices[i + 1])) {
			res += prices[i];
			cur = 0;
		}
		//买入： 如果没有股票，且明天股票涨(最后一天不能买)
		else if (cur == 0 && (prices[i + 1] > prices[i])) {
			res -= prices[i];
			cur = 1;
		}	
	}
    return cur?(res+prices[pricesSize-1]):res;
}
~~~



解法二、贪心算法2
如果明天涨，利润=prices[明天]-prices[今天]

~~~~ c

int maxProfit(int* prices, int pricesSize) {
    int sum = 0;
    for (int i = 0; i < pricesSize-1; i++)
    {
        if (prices[i + 1] > prices[i])
            sum += (prices[i + 1] - prices[i]);
    }
    return sum;
}
~~~~


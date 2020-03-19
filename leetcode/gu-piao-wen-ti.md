# 股票问题

## 309.Best Time to Buy and Sell Stock with Cooldown

#### 解法一

$$
f[i]=max\{f[i],max\{f[k-2]+price[i]-price[k]\quad 0\leq k\lt i\}\}
$$

时间复杂度 $$O(N^2)$$ ，空间复杂度 $$O(N)$$ 。

```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int len = prices.size();
        vector<int> cnt (len+1, 0);
        int max_prof = INT_MIN;
        for(int i = 2; i <= len; i++){
            cnt[i] = max(cnt[i], prices[i-1] - prices[0]);
            for(int k = 2; k < i; k++){
                cnt[i] = max(cnt[i], cnt[k-2] + prices[i-1] - prices[k-1]);
            }
            if(cnt[i] > max_prof) max_prof = cnt[i];
            else cnt[i] = max_prof;
        }
        for(int i = 1; i <= len; i++) cout << cnt[i] << " ";
        return cnt[len];
    }
};
```

#### 解法二

分别计算在第 $$i$$ 天买入/卖出的最大值：如果要在第 $$i$$ 天买入，考虑的有**（1）**前 $$[0...i-1]$$ 天最终是买入状态，将买入日期更新为第 $$i$$ 天；**（2）**前 $$[0...i-1]$$ 天最终是卖出状态，则基于已有卖出最大值减去今天买入的金额；取这两种情况的最大值。如果要在第 $$i$$ 天卖出，考虑的有**（1）**前 $$[0...i-1]$$ 天最终是卖出状态，将卖出日期更新为第 $$i$$ 天；**（2）**前 $$[0...i-1]$$ 天最终是买入状态，则基于已有买入最大值加上今天卖出的金额；

$$
\text{sell}[i]=max\{\text{sell}[i-1]-\text{prices}[i-1]+\text{prices}[i],\text{buy}[i-1]+\text{prices}[i]\}\\
\text{buy}[i]=max\{\text{buy}[i-1]+\text{prices}[i-1]-\text{prices}[i],\text{sell}[i-1]-\text{prices}[i]\}
$$

```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int len = prices.size();
        if(len <= 1) return 0;

        int pre_buy = -prices[1];
        int pre_sell[2] = {0, prices[1] - prices[0]};

        int max_prof = max(0, pre_sell[1]);

        for(int i = 2; i < len; i++){
            int cur_buy = max(pre_sell[0] - prices[i], pre_buy + prices[i-1] - prices[i]);
            int cur_sell = max(pre_sell[1] - prices[i-1] + prices[i], pre_buy + prices[i]);
            pre_buy = cur_buy;
            pre_sell[0] = pre_sell[1];
            pre_sell[1] = cur_sell;
            max_prof = max(max_prof, cur_sell);
        }

        return max_prof;
    }
};
```

## 123.Best Time to Buy and Sell Stock III

## 参考资源

[https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/discuss/108870/Most-consistent-ways-of-dealing-with-the-series-of-stock-problems](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/discuss/108870/Most-consistent-ways-of-dealing-with-the-series-of-stock-problems)


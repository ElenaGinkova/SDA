 ```c
int coinChange(vector<int>& coins, int amount) {
        vector<int> dp(amount + 1, INT_MAX);
        dp[0] = 0;
        for(int i = 1; i <= amount; i++)
        {
            for(int j = 0; j < coins.size(); j++)
            {
                if(coins[j] <= i && dp[i - coins[j]] != INT_MAX)
                {
                    dp[i] = min(dp[i], dp[i - coins[j]] + 1);
                }
            }
            
        }
        return dp[amount] == INT_MAX ? -1 : dp[amount];
    }
```
```c
int lengthOfLIS(vector<int>& nums) {
        vector<int> dp(nums.size());
        for(int i = 0; i < nums.size(); i++)
        {
            dp[i] = 1;
            for(int j = 0; j < i; j++)
            {
                if(nums[j] < nums[i])
                dp[i] = max(dp[j] + 1, dp[i]);
            }
        }
        return  *max_element(dp.begin(), dp.end());
    }
```

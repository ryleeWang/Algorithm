# 斐波那契

## 状态转移方程

$$
f(n)=f(n-1)+f(n-2)
$$

## 解决方案

### 解法1——递归

时间复杂度： $$O(2^n)$$ ，空间复杂度 $$O(1)$$ 

```cpp
int fibonacci(int n){
    if(n <= 1) return 1;
    if(n == 2) return 2;
    return fibonacci(n-1) + fibonacci(n-2);
}
```

### 解法2——动态规划（推荐）

时间复杂度： $$O(n)$$ ，空间复杂度： $$O(n)$$ 

```cpp
int fibonacci(int n){
    if(n <= 1) return 1;
    if(n == 2) return 2;
    int dp[n+1];
    for(int i = 3; i <= n; i++){
        dp[i] = dp[i-1] + dp[i-2];
    }
    return dp[n];
}
```

**推荐：**时间复杂度： $$O(n)$$ ，空间复杂度： $$O(1)$$ 

```cpp
long long fibonacci(int n){
    if(n <= 1) return n;
    long long pre1 = 0, pre2 = 1;
    long long current;
    for(int i = 2; i <= n; i++){
        current = pre1 + pre2;
        pre1 = pre2;
        pre2 = current;
    }
    return current;
}
```

### 解法3——矩阵乘法

$$
\begin{bmatrix}
f(n) & f(n-1) \\
f(n-1) & f(n-2)
\end{bmatrix}
=
\begin{bmatrix}
1 & 1 \\
1 & 0
\end{bmatrix}^n\quad (n\geq2)
$$

时间复杂度： $$O(log_2n)$$ ，空间复杂度： $$O(1)$$ 还是 $$O(log_2n)$$ ？

```cpp
// 求两矩阵的乘积
vector<vector<int>> fibmult(vector<vector<int>>& f1, vector<vector<int>>& f2){
    vector<vector<int>> result (2, vector<int> (2));
    result[0][0] = f1[0][0] * f2[0][0] + f1[0][1] * f2[1][0];
    result[0][1] = f1[0][0] * f2[0][1] + f1[0][1] * f2[1][1];
    result[1][0] = f1[1][0] * f2[0][0] + f1[1][1] * f2[1][0];
    result[1][1] = f1[1][0] * f2[0][1] + f1[1][1] * f2[1][1];
    return result;
}

// 递归做矩阵乘法，每次都计算一半的矩阵乘积
vector<vector<int>> fibpower(vector<vector<int>>& init, int n){
    if(n == 1) return init;
    vector<vector<int>> half = fibpower(init, n/2);
    vector<vector<int>> relt = fibmult(half, half);
    if(n % 2 == 0) return relt;
    relt[0][1] = (relt[0][0] += relt[0][1]) - relt[0][1];
    relt[1][1] = (relt[1][0] += relt[1][1]) - relt[1][1];
    return relt;
}

int fibonacci(int n){
    if(n <= 1) return n;
    vector<vector<int>> init (2, vector<int> (2));
    init[0][0] = 1;
    init[0][1] = 1;
    init[1][0] = 1;
    init[1][1] = 0;
    vector<vector<int>> result = fibpower(init, n);
    return result[0][0];
}
```


# 输入输出训练

> OJ在线编程常见输入输出练习场：[https://ac.nowcoder.com/acm/contest/320](https://ac.nowcoder.com/acm/contest/320)

## A+B\(1\)

输入描述:

> 输入包括两个正整数a,b\(1 &lt;= a, b &lt;= 10^9\),输入数据包括多组。

输出描述:

> 输出a+b的结果

输入输出示例：

![&#x8F93;&#x5165;\[\[a=1, b=5\], \[a=10, b=20\]\]&#xFF0C;&#x8F93;&#x51FA;\[6, 30\]&#xFF0C;&#x6362;&#x884C;&#x8868;&#x793A;&#x7ED3;&#x675F;](../.gitbook/assets/image%20%281%29.png)

```cpp
#include <iostream>
#include <string>
#include <sstream>
#include <vector>

using namespace std;

int main()
{
    string str, word;
    vector<int> result;
    int a, b;
    while(getline(cin, str)){
        if(str.size() == 0) break;
        istringstream iss(str);
        iss >> word;
        a = atoi(word.c_str());
        iss >> word;
        b = atoi(word.c_str());
        result.push_back(a+b);
    }
    for(int i: result)
        cout << i << endl;
    return 0;
}
```

## A+B\(2\)

输入描述：

> 输入第一行包括一个数据组数 t\(1 &lt;= t &lt;= 100\)  
> 接下来每行包括两个正整数 a, b\(1 &lt;= a, b &lt;= 10^9\)

输出描述：

> 输出a+b的结果

输入输出示例：

```cpp
#include <iostream>
#include <vector>

using namespace std;

int main()
{
    int lncnt;
    cin >> lncnt;
    int a, b;
    vector<int> result(lncnt);
    for(int i = 0; i < lncnt; i++){
        cin >> a >> b;
        result[i] = a + b;
    }
    for(int i = 0; i < lncnt; i++){
        cout << result[i] << endl;
    }
    return 0;
}
```

## A+B\(7\)

输入描述：

> 输入数据有多组, 每行表示一组输入数据。  
> 每行不定有n个整数，空格隔开。\(1 &lt;= n &lt;= 100\)。

输出描述：

> 每组数据输出求和的结果

输入输出示例：

![&#x8F93;&#x5165;\[\[1, 2, 3\], \[4, 5\], \[0, 0, 0, 0, 0\]\]&#xFF0C;&#x8F93;&#x51FA;\[6, 9, 0\]](../.gitbook/assets/image%20%282%29.png)

```cpp
#include <iostream>
#include <vector>
#include <string>
#include <sstream>

using namespace std;

int main(){
    string line, word;
    vector<int> result;
    while(getline(cin, line)){
        if(line.size() == 0) break;
        istringstream iss(line);
        int current = 0;
        while(iss >> word){
            current += atoi(word.c_str());
        }
        result.push_back(current);
    }
    for(int i: result){
        cout << i << endl;
    }
}
```

## 字符串排序\(3\)

输入描述：

> 多个测试用例，每个测试用例一行。每行通过 ',' 隔开，有n个字符，n＜100

输出描述：

> 对于每组用例输出一行排序后的字符串，用','隔开，无结尾空格

输入输出示例：

![&#x8F93;&#x5165;\[\[&apos;a&apos;, &apos;c&apos;, &apos;bb&apos;\], \[&apos;f&apos;, &apos;dddd&apos;\], \[&apos;nowcoder\]\]&#xFF0C;&#x8F93;&#x51FA;\[\[&apos;a&apos;, &apos;bb&apos;, &apos;c&apos;\], \[&apos;dddd&apos;, &apos;f&apos;\], \[&apos;nowcoder&apos;\]\]](../.gitbook/assets/image%20%283%29.png)

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <sstream>
#include <algorithm>

using namespace std;

int main(){
    string line, word;
    vector<vector<string>> result;
    while(getline(cin, line)){
        if(line.size() == 0) break;
        vector<string> current;
        istringstream iss(line);
        while(getline(iss, word, ',')){
            current.push_back(word);
        }
        sort(current.begin(), current.end());
        result.push_back(current);
    }
    for(vector<string> current: result){
        for(int j = 0; j < current.size(); j++){
            cout << current[j];
            if(j != current.size() - 1)
                cout << ",";
        }
        cout << endl;
    }
}
```

##  自测本地通过提交为0

输入描述：

> 输入有多组测试用例，每组空格隔开两个整数

输出描述：

> 对于每组数据输出一行两个整数的和

输入输出示例：

![&#x8F93;&#x5165;\[\[1, 1\], \[3, 5\], \[6, 7\], \[123456789123456789123456789123456789123456789123456789123456789, 1\], \[9999999999999999999999999999999999999999999999999999999999999999999999999999999, 1\]\]&#xFF0C;&#x8F93;&#x51FA;\[2, 8, 13, 123456789123456789123456789123456789123456789123456789123456790, 10000000000000000000000000000000000000000000000000000000000000000000000000000000\]](../.gitbook/assets/image%20%284%29.png)

{% hint style="info" %}
如果存为整型的话一定会溢出，所以要将两个数分别存为字符串，从最后一位开始往前计算。
{% endhint %}

```cpp
#include <iostream>
#include <string>
#include <sstream>

using namespace std;

int main()
{
    string line;
    string word1, word2;
    while(getline(cin, line)){
        if(line.size() == 0) break;
        istringstream iss(line);
        iss >> word1 >> word2;
        if(word1.size() < word2.size())
            word1.swap(word2);
        int loc1 = word1.size() - 1, loc2 = word2.size() - 1;
        int c = 0;
        int current;
        while(loc1 >= 0){
            if(loc2 >= 0){
                current = (word1[loc1] - '0' + word2[loc2] - '0' + c) % 10;
                c = (word1[loc1] - '0' + word2[loc2] - '0' + c) / 10;
            }
            else{
                current = (word1[loc1] - '0' + c) % 10;
                c = (word1[loc1] - '0' + c) / 10;
            }
            word1[loc1] = current + '0';
            loc1--; loc2--;
        }
        if(c)
            cout << c;
        cout << word1 << endl;
    }
    return 0;
}
```






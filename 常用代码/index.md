# 常用代码


# c++常用函数

## b进制转换

```c++
char get(int x)//将x转换为字符形式
{
    if (x <= 9) return x + '0';
    return x - 10 + 'A';
}

string base(int n, int b)//将n转换为b进制，返回对应字符串
{
    string res;
    while (n)
    {
        res += get(n % b);
        n /= b;
    }
    reverse(res.begin(), res.end());//翻转回高位在左
    return res;
}
```

## dfs

```c++
void dfs(int x,int y)
{
    g[x][y]='#';
    cnt++;
    for(int i=0;i<4;i++)
    {
        int a=x+dx[i],b=y+dy[i];
        if(a<0 || a>=n || b<0 || b>=m || g[a][b]=='#') continue;
        dfs(a,b);
    }
}
```

## bfs

```c++
#include <iostream>
#include <queue>
#include <algorithm>

#define x first
#define y second

using namespace std;
typedef pair<int,int> PII;
const int N = 25;
int n,m;
char g[N][N];

int bfs(int sx,int sy){
    queue<PII> q;
    q.push({sx,sy});
    g[sx][sy] = '#';
    int res = 0;
    int dx[] = {-1,0,1,0},dy[] = {0,1,0,-1};			//重点 ，四个方向，上，右，下，左
    while(q.size()){
        auto t = q.front();
        q.pop();
        res++;
        for(int i=0;i<4;i++){
            int x = t.x + dx[i],y = t.y + dy[i];
            if(x<0||x>=n||y<0||y>=m||g[x][y]!='.') continue;
            g[x][y] = '#';
            q.push({x,y});
            
        }
    }
    return res;
}
```

## 最小上升子序列（dp）

```c++
#include <iostream>

using namespace std;

const int N = 1010;

int n;
int w[N], f[N];

int main() {
    cin >> n;
    for (int i = 0; i < n; i++) cin >> w[i];

    int mx = 1;    // 找出所计算的f[i]之中的最大值，边算边找
    for (int i = 0; i < n; i++) {
        f[i] = 1;    // 设f[i]默认为1，找不到前面数字小于自己的时候就为1
        for (int j = 0; j < i; j++) {
            if (w[i] > w[j]) f[i] = max(f[i], f[j] + 1);    // 前一个小于自己的数结尾的最大上升子序列加上自己，即+1
        }
        mx = max(mx, f[i]);
    }

    cout << mx << endl;
    return 0;
}
```

## 下一排列

```c++
w[], 1-n
    
   next_permutation	
    
int k = n;
while(w[k-1]>w[k]) k--;  //找到反向升序列的第一个位置（从后往前）
int t = k;
while(w[t+1]>w[k-1]) t++;       //再反向升序列中找到比第一个位置的前一个位置的值大的最小值得位置
swap(w[k-1],w[t]);
reverse(w+k,w+n+1);
```



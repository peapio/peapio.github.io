# 刷题技巧


# 刷题技巧

> 记录c++刷题过程中的技巧

## vector

​	***vector<类型>标识符(最大容量，初始所有值)***

```c++
vector<vector<int> > cnt(m, vector<int>(5));
stoi(字符串(str),起始位置(0),n进制(2))         //将字符串转为十进制数参数为const string
int atoi(const char *str)   参数为const char*
```

## 多项选择判断

***a,b,c,d,e***建立hash表

```c++
hash[] = {1,2,4,8,16} //a1,b10,c100,d1000,e10000
^ 异或，判断学生选项与正确选项是否相同，哪道题错，哪位是1
 | 或，判断是否没选全，学生答案填上正确选项位，如果和正确选项一致，那么说明学生只是漏选
 & 与，与每个选项计算，判断哪个选项选错
```

```c++
	int temp;
	scanf("(%d", &temp);
	for (int k = 0; k < temp; k++) {
		char c;
		scanf(" %c)", &c);
		cout<<c<<endl; 
	}
```

## string

```c++
string (长度，赋值)
```

## cctype头文件的使用

参数为字符

| 函数名     | 返回值                                                       |
| ---------- | ------------------------------------------------------------ |
| isalnum()  | 如果参数是字母数字，即字母或者数字，函数返回true             |
| isalpha()  | 如果参数是字母，函数返回true                                 |
| iscntrl()  | 如果参数是控制字符，函数返回true                             |
| isdigit()  | 如果参数是数字（0－9），函数返回true                         |
| isgraph()  | 如果参数是除空格之外的打印字符，函数返回true                 |
| islower()  | 如果参数是小写字母，函数返回true                             |
| isprint()  | 如果参数是打印字符（包括空格），函数返回true                 |
| ispunct()  | 如果参数是标点符号，函数返回true                             |
| isspace()  | 如果参数是标准空白字符，如空格、换行符、水平或垂直制表符，函数返回true |
| isupper()  | 如果参数是大写字母，函数返回true                             |
| isxdigit() | 如果参数是十六进制数字，即0－9、a－f、A－F，函数返回true     |
| tolower()  | 如果参数是大写字符，返回其小写，否则返回该参数               |
| toupper()  | 如果参数是小写字符，返回其大写，否则返回该参数               |

## 很绝的代码 B1084

```c++
#include <iostream>
using namespace std;
int main() {
    string s;
    int n, j;
    cin >> s >> n;
    for (int cnt = 1; cnt < n; cnt++) {
        string t;
        for (int i = 0; i < s.length(); i = j) {
            for (j = i; j < s.length() && s[j] == s[i]; j++); ///注意这里,其实就是一个判断
            t += s[i] + to_string(j - i);
        }
        s = t;
    }
    cout << s;
    return 0;
}
```

## map迭代器的访问遍历

```c++
int main(){
    map<int, string>mp;
    mp[3] = "asdf";
    mp[5] = "zxcv";
    mp[4] = "xvzcv";
    for(auto it = mp.begin();it!=mp.end();it++){
        cout<<it->second<<endl;
    }
    return 0;
}
```


## 使用 ``` i<a&&i<b 取最小值,i<a||i<b 取最大值 ```

c++各变量取值大小

| type                     | min                        | max                  |
| ------------------------ | -------------------------- | -------------------- |
| unsigned int             | 0                          | 4294967295           |
| int                      | -2147483648(2^31)          | 2147483647           |
| unsigned long            | 0                          | 4294967295           |
| long                     | -2147483648                | 2147483647           |
| long long                | -9223372036854775807(2^63) | 9223372036854775808  |
| unsigned long long       |                            | 18446744073709551615 |
| __int64的最大值          | -9223372036854775808       | 9223372036854775807  |
| unsigned __int64的最大值 |                            | 18446744073709551615 |


| 数据类型 | 32位 | 64位 | 取值范围 |
| -------- | ---- | ---- | -------- |
| char     | 1    | 1    | -128~127 |


## 反向迭代,最大元素

```c++
string str = "1234567890";
    for(auto it = str.rbegin();it!=str.rend();it++){
            cout<<*it;
        }
cout<<*max_element(str.begin(),str.end());
//按字典序
```


## pat甲级有疑问的

- 1012
- 1044


## 常用的代码

```c++
//判断是否是素数
bool isPrime(int a){
    if(a<=1) return false;
    float tmp = (int)sqrt(a*1.0);
    for(int i=2;i<=tmp;i++){
        if(a%i==0) return false;
    }
    return true;
}
```

> 二次探测法 hash(key) = (key%m+d)%m === (key+d)%m; (d=1^2,-1^2,2^2,-2^2,......);
> 查找次数小于m.



待补充。。


# C++_STL常用函数




# C++STL

## 1.vector

向量:长度根据需要自动改变的数组

```c++
#include <iostream>
#include <stdio.h>
#include <string.h>
#include <vector>
using namespace std;

int main(){
    vector<int> name;
    for(int i=1;i<=5;i++){
        name.push_back(i);
    }
    name.insert(name.begin()+name.size(),-1);
    name.erase(first,last);
    //利用迭代器的两种遍历方式
    for(vector<int>::iterator it=name.begin();it!=name.end();it++){
        cout<<*it;

    }
    vector<int>::iterator it=name.begin();
    for(int i=0;i<5;i++){
        cout<<*(it+i);
    }
    cout<<"\n"<<name.size();
}
```

### vector常用函数

| 方法              | 时间复杂度 | 作用                        |
| ----------------- | ---------- | --------------------------- |
| push_back()       | O(1)       | 在vector的后面添加一个元素x |
| pop_back()        | O(1)       | 删除vector尾元素            |
| size()            | O(1)       | 获得vector中元素的个数      |
| clear()           | O(n)       | 清除vector中所有元素        |
| insert(it,x)      | O(n)       | 像it处插入一个元素x         |
| erase(it)         | O(n)       | 删除it处的元素              |
| erase(first,last) | O(n)       | 删除区间内的元素,左闭右开   |

==作用:动态存储==

## 2.set

集合:内部自动有序且不含重复元素的容器

set不可以*(set++)

```c++
#include <iostream>
#include <stdio.h>
#include <string.h>
#include <set>
using namespace std;

int main(){
    set<int> name;
    name.insert(3);
    name.insert(5);
    name.insert(2);
    name.insert(7);
    name.insert(4);
    set<int>::iterator it = name.find(5);
    name.erase(name.find(5));
    name.size();
    for(set<int>::iterator it = name.begin();it!=name.end();it++){
        cout<<*it;
    }
}

```

### set常用函数

| 方法              | 时间复杂度    | 作用                                      |
| :---------------- | ------------- | ----------------------------------------- |
| insert(x)         | O(logN)       | 将x插入到set容器中,并自动递增排序并去重   |
| find(value)       | O(logN)       | 返回set中对应值为value的迭代器            |
| erase(it)         | O(1)          | 删除单个元素迭代器st.erase(st.find(100)); |
| erase(value)      | O(logN)       | 删除单个元素的值,value为确切值            |
| erase(first,last) | O(last-first) | 参数为迭代器地址,删除区间元素,左闭右开    |
| size()            | O(1)          | 获得set内元素个数                         |
| clear()           | O(N)          | 清空set内所有元素                         |

==作用:排序去重==

## 3.String

```c++
#include <iostream>
#include <stdio.h>
#include <string.h>
#include <string>
using namespace std;

int main(){
    string str = "gffd";
    for(string::iterator it = str.begin();it != str.end();it++){
        cout<<*it;
   }
    cout<<str;
    printf("%s",str.c_str());
    for(int i=0;i<str.length();i++){
        printf("%c",str[i]);
    }
    //几种遍历方法
}

```

### String常用函数

| 方法                  | 时间复杂度      | 作用                                                      |
| --------------------- | --------------- | --------------------------------------------------------- |
| compare operator      |                 | 两个字符串可以直接使用==,!=,<,<=等比大小,比较规则是字典序 |
| length()/size()       | O(1)            | 返回string的长度                                          |
| insert(pos,string)    | O(N)            | 在pos处插入string,0,1,2,3,第一个字符前是0                 |
| insert(it,it2,it3)    | O(N)            | it为原字符欲插入位置,it2,it3为待插字符串首尾迭代器        |
| erase(it)             | O(N)            | 删除元素迭代器                                            |
| erase(first,last)     | O(N)            | 删除区间,左闭右开                                         |
| erase(pos,length)     | O(N)            | pos为起始位置,length为删除字符个数                        |
| clear()               | O(1)            | 清空                                                      |
| substr(pos,len)       | O(len)          | 返回从pos开始len长的子串                                  |
| find(str2)            | O(mn)           | 返回str第一次出现的位置,否则返回string::npos              |
| find(str2,pos)        | O(mn)           | 从pos处开始匹配,返回值与上相同                            |
| replace(pos,len,str2) | O(str.length()) | 把从str从pos号位开始长度为len的子串替换为str2             |

string::npos是一个常数,其本身为-1,但由于是unsigned_int类型,因此也可以认为是unsigned_int的最大值,可等于4294967295string::npos用以作为find函数失配的返回值

n,m分别为str,str2的长度

## 4.map

映射: array[0]=25, 0-->25 0映射到25,map可以将任何基本类型(包括STL容器)映射到任何基本类型(包括STL容器)

```c++
#include <iostream>
#include <stdio.h>
#include <string.h>
#include <string>
#include <map>

using namespace std;

int main(){
    map<char,int> mp;
    mp['m'] = 20;
    mp['r'] = 30;
    mp['a'] = 40;
    //map<char,int>::iterator it = mp.begin();
    //cout<<it->first<<it->second<<endl;
    for(map<char,int>::iterator it = mp.begin();it!=mp.end();it++){
        cout<<it->first<<it->second<<endl;
        //打印键和值
    }
    cout<<mp['r'];
}
```

map会以键从小到大的顺序自动排序

### map常用函数



| 方法              | 时间复杂度    | 作用                                     |
| ----------------- | ------------- | ---------------------------------------- |
| find(key)         | O(logN)       | 返回键为key的映射迭代器                  |
| erase(it)         | O(1)          | 删除元素的迭代器,mp.erase(mp.find('d')); |
| erase(key)        | O(logN)       | key为欲删除映射的键                      |
| erase(first,last) | O(last-first) | 删除区间,左闭右开                        |
| size()            | O(1)          | 获得映射map的对数                        |
| clear()           | O(N)          | 清除map中所有元素                        |

## 5.queue

队列:先进先出

```c++
#include <iostream>
#include <stdio.h>
#include <queue>
using namespace std;
int main(){
    queue<int> q;
    for(int i=0;i<5;i++){
        q.push(i);
    }
    cout<<q.front()<<endl;
    cout<<q.back()<<endl;
    //输出头和尾
}
```

### queue常用函数

| 方法    | 时间复杂度 | 作用          |
| ------- | ---------- | ------------- |
| push()  | O(1)       | 将x入队(尾进) |
| pop()   | O(1)       | 出队(头出)    |
| empty() | O(1)       | 判空          |
| size()  | O(1)       | 返回元素个数  |
| front() | O(1)       | 获取头元素    |
| back()  | O(1)       | 获取尾元素    |

## 6.priority_queue

优先队列:其底层是用堆来实现的,优先队列中队首元素一定是当前队列优先级最高的

优先队列没有front(),back(),只能通过top()函数获取队首元素(对顶元素).也就是优先级最高的元素

### priority_queue常用函数

| 方法    | 时间复杂度 | 作用                   |
| ------- | ---------- | ---------------------- |
| push(x) | O(logN)    | 将x入队                |
| top()   | O(1)       | 获取对顶元素(队首元素) |
| empty() | O(1)       | 判空                   |
| size()  | O(1)       | 返回优先队列元素个数   |

### priority_queue内元素优先级的设置

1. *基本数据类型的优先级设置*

int,char,double,等数字越大优先级越高(如果是char型,字典序最大)

```c++
pritority_queue<int> q;
pritority_queue<int,vector<int>,less<int> > q;
```

相比第一种第二种多出两个参数,vector<int>表示承载底层数据结构堆的(heap)容器,==less<int>表示数字大的优先级越大,greater<int>表示数字小的优先级越大==

2. *结构体的优先级设置*

```c++
struct fruit{
    string name;
    int price;
};
```

现在希望按水果的价格高的优先级高,需用重载(overload)小于号"<".重载是指对已有的运算符进行重新定义,也就是说可以改变小于号的功能

```c++
struct fruit {
    string name;
    int price;
    friend bool operator < (fruit f1,fruit f2){
        return f1.price<f2.price;
    }
};
```

friend为友元

重载>号会出错?

```c++
#include <iostream>
#include <string>
#include <queue>
using namespace std;
struct fruit{
    string name;
    int price;
}f1,f2,f3;
struct cmp{
    bool operator () (fruit f1,fruit f2){
        return f1.price>f2.price;
    }
};
int main(){
    pritority_queue<fruit,vector<fruit>,cmp> q;
    f1.name = "桃子";
    f1.price = 3;
    f2.name = "梨子";
    f2.price = 4;
    f3.name = "苹果";
    f3.price = 1;
    q.push(f1);
    q.push(f2);
    q.push(f3);
    cout<<q.top().name<<" "<<q.top().price<<endl;
    return 0;
    //第二种方式,常用方式
}
```

## 7.stack

栈:后进后出

```c++
#include <iostream>
#include <stdio.h>
#include <stack>
using namespace std;
int main(){
    stack<int> st;
    for(int i=0;i<5;i++){
        st.push(i);
    }
    cout<<st.top();
}
```

### stack常用函数

| 方法    | 时间复杂度 | 作用                  |
| ------- | ---------- | --------------------- |
| push()  | O(1)       | 入栈                  |
| top()   | O(1)       | 获得栈顶元素          |
| pop()   | O(1)       | 弹出栈顶元素          |
| empty() | O(1)       | 判空                  |
| size()  | O(1)       | 返回stack内元素的个数 |

## 8. pair

当需要将两个元素捆绑在一起作为一个合成元素,又不想因此定义一个结构体时,使用pair作为一个替代品.

```c++
#include <iostream>
#include <string>
#include <utility>
//如果记不住utility可以使用map,因为map实现设计pair
using namespace std;
int main(){
    pair<string,int> p;
    p.first = "haha";
    p.second = 5;
    cout<< p.first <<" "<< p.second<<endl;
    p = make_pair("xixi",55);
    cout<< p.first <<" "<< p.second<<endl;
    p = pair<string,int>("heihei",555);
    cout<< p.first <<" "<< p.second<<endl;
	//实现Pair的几种方式
}
```

### pair常用函数

####　比较操作数

两个ｐａｉｒ类型的数据可以直接使用==,!=,<=,>,>=等比较大小比较规则以first的大小为标准,只有first相等时,才去判断second的大小

## 9.algorithm头文件下的常用函数

| 方法               | 作用                                                         |
| ------------------ | ------------------------------------------------------------ |
| max(x,y)           | 返回x,y中的最大值(可以是浮点数),三个数最大值max(x,max(y,z))  |
| min(x,y)           | 返回x,y中的最小值(可以是浮点数)                              |
| abs(x)             | 返回x的绝对值(必须是正数,浮点数用math下的fabs)               |
| swap(x,y)          | 交换x和y的值                                                 |
| reverse(it,it2)    | 可将数组指针在[it,it2)之间的元素或容器的迭代器的其范围内的元素进行进行反转 |
| next_permutation() | 给出一个序列在全排列中的下一个序列                           |
|                    |                                                              |

**next_permutation()**

```c++
#include <iostream>  
#include <algorithm>  
using namespace std;  
int main()  
{  
    int num[3]={1,2,3};  
    do  
    {  
        cout<<num[0]<<" "<<num[1]<<" "<<num[2]<<endl;  
    }while(next_permutation(num,num+3));  
    return 0;  
}  
```

**fill():可以把数组或容器中的某一段区间赋为某个相同的值.和memset不同,这里的赋值可以是数组类型对应范围中的任意值**

```c++
#include <iostream>
#include <algorithm>
using namespace std;
int main(){
    int a[5] = {1,2,3,4,5};
    fill(a,a+5,233);
    for(int i=0;i<5;i++){
        cout<<a[i];
    }
}
```

**sort():用来排序的函数**

```c++
#include <iostream>  
#include <algorithm>  
using namespace std;  
int main()  
{  
    int a[6] = {9,4,2,5,6,-1};
    double b[] = {1.4,-2.1,9};
    char c[] = {'T','W','A','K'};
    sort(a,a+4);
    for(int i=0;i<6;i++){
        cout<<a[i];
    }
    cout<<"\n";
    sort(a,a+6);
    for(int i=0;i<6;i++){
        cout<<a[i];
    }
    cout<<"\n";
    sort(b,b+3);
    for(int i=0;i<3;i++){
        cout<<b[i];
    }
    cout<<"\n";
    sort(c,c+4);
    for(int i=0;i<4;i++){
        cout<<c[i];
    }
     return 0;  
}
```

1. sort有三个参数前两个是容器的首尾迭代器,左闭右开,第三个就是比较函数cmp,不添默认按照从小到大排序

```c++
#include <iostream>  
#include <algorithm>  
using namespace std;  
template <typename T> bool cmp(T a,T b){
    return a>b;
}
int main()  
{  
    int a[6] = {9,4,2,5,6,-1};
    double b[] = {1.4,-2.1,9};
    char c[] = {'T','W','A','K'};
    sort(c,c+3,cmp<char>);
    for(int i=0;i<3;i++){
        cout<<c[i];
    }
     return 0;  
}  
```

2. 结构体数组的排序

	```c++
	struct node{
	    int x,y;
	}ssd[10];
	```

	```c++
	bool cmp(node a,node b){
	    return a.x>b.x;
	}
	```

3. 容器的排序

	```c++
	#include <stdio.h>
	#include <vector>
	#include <algorithm>
	using namespace std;
	bool cmp(int a,int b){
	    return a>b;
	}
	int main(){
	    vector<int> vi;
	    vi.push_back(3);
	    vi.push_back(1);
	    vi.push_back(2);
	    sort(vi.begin(),vi.end(),cmp);
	    for(int i=0;i<3;i++){
	        printf("%d",vi[i]);
	    }
	    return 0;
	}
	```

	string的排序

	```c++
	#include <iostream>
	#include <vector>
	#include <algorithm>
	using namespace std;
	int main(){
	    string str[3] = {"bbbb","cc","aaa"};
	    sort(str,str+3);
	    for(int i=0;i<3;i++){
	        cout<<str[i]<<endl;
	    }
	    return 0;
	}
	```

	按照字符串的从小到大排序

	```c++
	#include <iostream>
	#include <vector>
	#include <algorithm>
	using namespace std;
	bool cmp(string str1,string str2){
	    return str1.length()<str2.length();
	}
	int main(){
	    string str[3] = {"bbbb","cc","aaa"};
	    sort(str,str+3,cmp);
	    for(int i=0;i<3;i++){
	        cout<<str[i]<<endl;
	    }
	    return 0;
	}
	```

	

**lower_bound()和upper_bound()**

lower_bound(forst,last,val)用来寻找在数组或容器的[first,lasr)范围内==第一个值大于或等于val的元素的位置==,如果是数组,则返回该位置的指针;如果是容器,则返回该位置的迭代器

upper_bound(forst,last,val)用来寻找在数组或容器的[first,lasr)范围内==第一个值大于val的元素的位置==,如果是数组,则返回该位置的指针;如果是容器,则返回该位置的迭代器

如果数组或容器中没有需要寻找的元素,则均返回可以插入该元素的位置的指针或迭代器(==即假设存在该元素时,该元素应当在的位置==)

时间复杂度均为O(log(last-fast))

```c++
#include <iostream>
#include <algorithm>
using namespace std;
int main(){
    int a[10] = {1,2,2,3,3,3,5,5,5,5};//注意数组下标从0开始
    //寻找-1
    int *lowerPos = lower_bound(a,a+10,-1);
    int *upperPos = upper_bound(a,a+10,-1);
    cout<<lowerPos-a<<" "<<upperPos-a<<endl;
//寻找1
    lowerPos = lower_bound(a,a+10,1);
    upperPos = upper_bound(a,a+10,1);
    cout<<lowerPos-a<<" "<<upperPos-a<<endl;
//寻找3
    lowerPos = lower_bound(a,a+10,3);
    upperPos = upper_bound(a,a+10,3);
    cout<<lowerPos-a<<" "<<upperPos-a<<endl;
//寻找4
    lowerPos = lower_bound(a,a+10,4);
    upperPos = upper_bound(a,a+10,4);
    cout<<lowerPos-a<<" "<<upperPos-a<<endl;
//寻找6
    lowerPos = lower_bound(a,a+10,6);
    upperPos = upper_bound(a,a+10,6);
    cout<<lowerPos-a<<" "<<upperPos-a<<endl;
}
```

如果只想获得欲查询的元素的下标,就可以不用临时指针,而==直接令返回值减去数组首地址即可==



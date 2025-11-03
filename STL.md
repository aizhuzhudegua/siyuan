# STL

# STL

## 容器：数组、链表、树、栈、队列、集合、映射表

### vector

为了获得连续的空间，vector在容量不够时会找一片新的连续空间（似乎是原来空间的两倍），然后将原有的数据和新的数据拷贝到新的空间。

```c++
#include<vector>
//构造函数
vector<T>() //默认
vector<int> v2(v1.begin(),v1.end()) //区间复制
vector<T>(n,elem) //n个elem方式
vector(const vector &vec) //拷贝构造
vector<int> vec6 = {10, 20, 30, 40};
vector<int> vec6 = vector<int>({10, 20, 30, 40});
vector<int> abc(10);    //初始化了10个默认值为0的元素
 
//插入元素
vector<int> v;  //初始化容器
v.push_back(e); //插入元素e

//遍历
//方法一
vector<int>::iterator itBegin = v.begin(); //起始迭代器
vector<int>::iterator itEnd = v.end(); //结束迭代器，指向最后一个元素的下一个位置

while(itBegin!=itEnd){
    cout<< *itBegin <<endl;
    itBegin++;
}

//方法二
for(vector<int>::iterator it = v.begin();v.begin()!=v.end();it++){
     cout<< *it <<endl;
}

//方法三，用算法for_each

void myPrint(int val){
    cout<<val<<endl;
}
// 取尾，去尾
v.back();
v.pop_back();

#include<algorithm>
for_each(v.begin(),v.end(),myPrint); #用到了回调的技术
```

### string

```c++
#include <string> 
using namespace std;

//默认构造
string();
//用char *
string(const char *);
//拷贝构造
string(const string& str);
//用n个c初始化
string(int n,char c);
    
//赋值操作
string & operator=(const char* str);
string & operator=(const string &s);
string & operator=(char c);
string & assign(const char *s);
str.assign("hello C++");
string & assign(const char *s,int n); //把字符串s的前n个赋值
string & assign(const string &s);
string & assign(int n,char c);//用n个字符c赋给当前字符串

//追加字符串
string & operator+=(const char* str);
string & operator+=(const string &str);
string & operator+=(char c);
string & append(const char *s);
string & append(const char *s,int n); //把字符串s的前n个追加
string & append(const string &s);
string & append(const string &s,int pos,int n);//字符串pos开始的n个字符串
// push_back(s) append(s)

//比较字符串
int compare(const string &s) const;
int compare(const char *s) const;

//字符存取
char& operator[](int n);
char& at(int n);

//插入删除
string & insert(int pos,const char *s);
string & insert(int pos,const string& str);
string & insert(int pos,int n,char c);
string & erase(int pos,int n=npos); //从pos开始删除n个字符
string str = "hello";
str.erase(1,3);
// pop_back()
// back()

// 子串
返回由pos开始的n个字符组成的字符串
string subStr = str.substr(1, 3);
```

### unordered_map(不去重)

```c++
// 构造
unordered_map<string, int> myMap; // 定义一个字符串到整数的哈希表

// 插入
myMap.insert({"Alice", 18}); // 插入键值对{"Alice", 18}
myMap["Bob"] = 20; // 使用数组下标方式插入键值对{"Bob", 20}

// 判断键"Alice"是否存在
if (myMap.count("Alice")) { 
    // 存在
} else {
    // 不存在
}

// 遍历哈希表
for (auto it = myMap.begin(); it != myMap.end(); it++) {
    string key = it->first; // 访问键
    int value = it->second; // 访问值
    // 处理键值对
}

// 删除
myMap.erase("Alice"); // 删除键为"Alice"的键值对
myMap.clear(); // 清空哈希表中所有的键值对
```

### queue

```c++
//push()：在队列尾部插入一个元素。
//pop()：移除队列头部的元素。注意，如果队列为空，执行此操作将引发未定义行为。
//front()：返回队列头部的元素，但不移除它。
//back()：返回队列尾部的元素，但不移除它。
//empty()：检查队列是否为空，如果为空则返回true，否则返回false。
//size()：返回队列中的元素数量。
```

### stack

```c++
//empty()：//判断stack是否为空
//size()：//stack的大小
//top()：//栈顶元素
//push()：//入栈
//pop()：；//出栈
```

## priority_queue

```c++
#include <iostream>
#include <queue>
#include <algorithm>

using namespace std;

struct custom
{
    int a;
    int b;
    int c;
    bool operator < (const custom& cust) const{
        if (a == cust.a) {
            if (b == cust.b) {
                return c < cust.c; 
            } else {
                return b < cust.b; 
            }
        } else {
            return a < cust.a; 
        }
    }
};

int main() {
    priority_queue<custom> que;
    que.push(custom{4, 2, 7});
    que.push(custom{4, 2, 3});
    que.push(custom{2, 3, 1});
    que.push(custom{5, 6, 9});

    while (!que.empty()) {
        custom top = que.top();
        cout << top.a <<  top.b <<  top.c << " "; 
        que.pop();
    }

    cout << endl;
    return 0;
}

```

## 算法

```c++
#include <algorithm>
```

## sort

### 基本类型排序

```c++
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

int main() {

    vector<int> v;
    v.push_back(3);
    v.push_back(1);
    v.push_back(4);
    v.push_back(3);

    sort(v.begin(),v.end());

    for(auto it = v.begin();it < v.end(); it ++)
    {   
        cout << *it << " ";
    }
    cout << endl;
    return 0;
}
```

### 自定义类型排序——自定义cmp（更灵活）

```c++
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

struct custom
{
    int a;
    int b;
    int c;
};

bool cmp (const custom& A,const custom& B)
{
    return A.a < B.a;
}


int main() {
    vector<custom> v;
    v.push_back(custom{3,2,7});
    v.push_back(custom{4,1,3});
    v.push_back(custom{2,3,1});
    v.push_back(custom{5,6,9});

    sort(v.begin(),v.end(),cmp);

    for(auto it = v.begin();it < v.end(); it ++)
    {   
        cout << it->a << it->b << it->c << " ";
    }
    cout << endl;
    return 0;
}
```

### 自定义类型排序——重载运算符

```c++
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

struct custom
{
    int a;
    int b;
    int c;
    bool operator < (const custom& c){
        return b > c.b;
    }

};

int main() {
    vector<custom> v;
    v.push_back(custom{3,2,7});
    v.push_back(custom{4,1,3});
    v.push_back(custom{2,3,1});
    v.push_back(custom{5,6,9});

    sort(v.begin(),v.end());

    for(auto it = v.begin();it < v.end(); it ++)
    {   
        cout << it->a << it->b << it->c << " ";
    }
    cout << endl;
    return 0;
}
```

## 迭代器：算法要通过迭代器访问容器

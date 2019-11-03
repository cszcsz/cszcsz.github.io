---
title: PAT算法知识点回顾
date: 2019-09-22 19:44:14
categories: 算法
tags: [算法,PAT]
keywords: 算法, PAT
---



# 数据结构与算法知识点总结：



#### 实用技巧：

##### 1.  fill()函数的使用

​	填充一维数组：

```c++
    int arr[10];
    fill(arr, arr + 10, 2);

 	vector<int> v{0, 1, 2, 3, 4, 5, 6, 7, 8, 9};
    fill(v.begin(), v.end(), -1);
    return 0;
```

​	填充二维数组：

```c++
	fill(dis[0], dis[0]+maxn*maxn, INF);
	// 因为dis[0]才是dis的首元素dis[0][0]的地址fill()函数的使用
```

##### 2. memset()函数的使用

```c++
    int main(){
        int a[20];
        memset(a, 0, sizeof a); 
        //注意：memset为字节填充，如果填充整形数组只能填充0和-1
        return 0;
    }
```

##### 3. count用于统计数组或向量中某个值出现的次数

```c++
	//向量计数
	cout << count(v.begin(), v.end(), 1) << endl;
	cout << count(v.begin(), v.end(), 5) << endl;
	cout << count(v.begin(), v.end(), 6) << endl;
	cout << endl;
	//数组计数
	cout << count(a, a + 10, 0) << endl;
	cout << count(a, a + 10, 1) << endl;
	cout << count(a, a + 10, 4) << endl;

```

##### 4.erase()和remove()结合起来删除容器中的指定元素

```c++
vec.erase( remove(vec.begin(), vec.end(), 'A'), vec.end() );
```



##### 5.利用find()查找所有子串或字符在原字符串中的位置

```c++
while((pos=str.find(c,pos))!=string::npos)
{
	// 其它代码
	pos++;
}
```



##### 5.C语言读入一行带空格的字符串(读到的回车符丢掉)

```c
scanf("%[^\n]",str);    //^表示非，意思只要没有遇到回车符\n，都读进来
```



##### 7.大整数乘法核心代码

```c++
    for(int i=0;i<num1.size();i++)
    {
        for(int j=0;j<num2.size();j++)
        {
            result[i+j]+=num1[i]*num2[j];       //核心
        }
    }
    for(int i=0;i<result.size();i++)
    {
        if(result[i]>=10)                       //统一处理进位
        {
            result[i+1]+=result[i]/10;       
            result[i]=result[i]%10;
        }
    }
```

<!--more-->



#### 数据结构与算法（补充部分，以防万一~）

#### 算法部分：

#### 1、动态规划（DP）

##### N阶楼梯上楼问题：

​	一次可以走两阶或一阶，问有多少种上楼方式。

```c++
        int f[100];
        f[1]=1;f[2]=2;
        for(int i=3;i<=n;i++)
        {
            f[i]=f[i-1]+f[i-2];
        }
        cout<<f[n]<<endl;

```





#### 数据结构部分：

#### 1、树：

##### 后序和中序构造二叉树：

```c++
int leftChild[100];
int rightChild[100];

int buildTree(int post[],int in[],int n)
{
    if(n==0)
        return 0;
    int root = post[n-1];
    int i=0;
    while(in[i]!=root&&i<n)
        i++;
    leftChild[root]=buildTree(post,in,i);
    rightChild[root]=buildTree(post+i,in+i+1,n-i-1);
    return root;
}

```

##### 层序遍历:

```c++
void levelOrder(int root)
{
    int flag=0;
    queue<int> q;
    q.push(root);
    while(!q.empty())
    {
        if(flag==0)
        {
          cout<<q.front();
          flag=1;
        }
        else
            cout<<" "<<q.front();
        if(leftChild[q.front()]!=0)
            q.push(leftChild[q.front()]);
        if(rightChild[q.front()]!=0)
            q.push(rightChild[q.front()]);
        q.pop();
    }
}

```





#### 2、图：

##### djikstra+dfs求最短路径：

```c++
void djikstra()
{
    for(int i=0;i<n;i++)
    {
        int k=-1,temp_min=INF;
        for(int j=0;j<n;j++)
        {
            if(dis[j]<temp_min&&!visited[j])
            {
                temp_min=dis[j];
                k=j;
            }
        }
        if(k==-1)
            break;
        visited[k]=1;
        for(int j=0;j<n;j++)
        {
            if(!visited[j])
            {
                if(dis[k]+edge[k][j]<dis[j]&&edge[k][j]!=INF)
                {
                    dis[j]=dis[k]+edge[k][j];
                    pre[j].clear();
                    pre[j].push_back(k);            //pre[]用于后面用dfs求出最短路径上的点
                }
                else if(dis[k]+edge[k][j]==dis[j]&&edge[k][j]!=INF)
                {
                    pre[j].push_back(k);
                }
            }
        }
    }
}


//打印出多条最短路径
void dfs(int v)                       
{
    temppath.push_back(v);
    if(v==0)
    {
        int need=0,back=0;
        for(int i=temppath.size()-1;i>=0;i--)
        {
            int id=temppath[i];
			cout<<id<<" ";
        }
        cout<<endl;
        temppath.pop_back();
        return;
    }
    for(int i=0;i<pre[v].size();i++)
    {
        dfs(pre[v][i]);
    }
    temppath.pop_back();
}

```



#### 3、并查集：

联想江湖掌门帮派的例子~

**find（查）函数：**

```c++
int find(int root)
{
    int son,tmp;
    son = root;
    while(root!=pre[root])
        root=pre[root];
    while(son!=root)
    {
        tmp=pre[son];
        pre[son]=root;
        son=tmp;
    }
    return root;
}

```

**union（并）函数：**

```c++
void union(int r1,int r2)
{
    int x,y;
    x=find(r1);
    y=find(r2);
    if(x!=y)
        pre[x]=y;
}

```



#### 3、动态规划（01背包问题）：

```c++
int n,m;
int v[1005],w[1005];
int dp[1005][1005];

cin>>n>>m;
for(int i=1;i<=n;i++)
    cin>>v[i]>>w[i];
for(int i=1;i<=n;i++)
{
    for(int j=1;j<=m;j++)
    {
        dp[i][j]=dp[i-1][j];
        if(j>=v[i])
        {
            dp[i][j]=max(dp[i-1][j-v[i]]+w[i],dp[i-1][j]);
        }

    }
}
cout<<dp[n][m];

```


---
title: Day 2
urlname: d2
categories: "Training"
tags:
- "Algorithm"
- "c/c++"
- "STL"
- "math"
- "Thinking"
- "HDU"
- "CodeForces"
image: https://i.loli.net/2019/07/18/5d30162a8c07454276.jpg
---
### 前m大的数
Description:
还记得Gardon给小希布置的那个作业么？（上次比赛的1005）其实小希已经找回了原来的那张数表，现在她想确认一下她的答案是否正确，但是整个的答案是很庞大的表，小希只想让你把答案中最大的M个数告诉她就可以了。 
给定一个包含N(N<=3000)个正整数的序列，每个数不超过5000，对它们两两相加得到的N\*(N-1)/2个和，求出其中前M大的数(M<=1000)并按从大到小的顺序排列。
Input
>输入可能包含多组数据，其中每组数据包括两行： 
第一行两个数N和M， 
第二行N个数，表示该序列。 

Output
>对于输入的每组数据，输出M个数，表示结果。输出应当按照从大到小的顺序排列。

Sample Input
>4 4
1 2 3 4
4 5
5 3 6 4

Sample Output
>7 6 5 5
11 10 9 9 8

Problem solving:
I have nothing to say about this \*\*\* problem,just do it without thinking.

Code:
```
#include<cstdio>
#include<iostream>
#include<algorithm>
using namespace std;
const int maxn=1e7;
int a[maxn],b[4000];
int main()
{
	int n,m;
	while(~scanf("%d %d",&n,&m))
	{
		int k=0;
		for(int i=0;i<n;i++)
			scanf("%d",&b[i]);
		for(int i=0;i<n-1;i++)
		{
			for(int j=i+1;j<n;j++)
			{
				a[k]=b[i]+b[j];
				k++;
			}
		}
		sort(a,a+k);
		for(int i=k-1;i>0;i--)
		{
			if(m==0)	break;
			if(i==k-1)	cout<<a[i];
			else	cout<<" "<<a[i];
			m--;
		}
		puts("");
	}
}
```


### 稳定排序
Description:
大家都知道，快速排序是不稳定的排序方法。 
如果对于数组中出现的任意a[i],a[j](i<j),其中a[i]==a[j]，在进行排序以后a[i]一定出现在a[j]之前，则认为该排序是稳定的。 

某高校招生办得到一份成绩列表，上面记录了考生名字和考生成绩。并且对其使用了某排序算法按成绩进行递减排序。现在请你判断一下该排序算法是否正确，如果正确的话，则判断该排序算法是否为稳定的。 
Input
>本题目包含多组输入，请处理到文件结束。 
对于每组数据，第一行有一个正整数N(0<N<300)，代表成绩列表中的考生数目。 
接下来有N行，每一行有一个字符串代表考生名字(长度不超过50，仅包含'a'~'z'),和一个整数代表考生分数(小于500)。其中名字和成绩用一个空格隔开。 
再接下来又有N行，是上述列表经过某排序算法以后生成的一个序列。格式同上。

Output
>对于每组数据，如果算法是正确并且稳定的，就在一行里面输出"Right"。如果算法是正确的但不是稳定的，就在一行里面输出"Not Stable"，并且在下面输出正确稳定排序的列表，格式同输入。如果该算法是错误的，就在一行里面输出"Error",并且在下面输出正确稳定排序的列表，格式同输入。 
注意，本题目不考虑该排序算法是错误的，但结果是正确的这样的意外情况。

Sample Input
>3
aa 10
bb 10
cc 20
cc 20
bb 10
aa 10
3
aa 10
bb 10
cc 20
cc 20
aa 10
bb 10
3
aa 10
bb 10
cc 20
aa 10
bb 10
cc 20

Sample Output
>Not Stable
cc 20
aa 10
bb 10
Right
Error
cc 20
aa 10
bb 10

Problem solving:
Attention: we'd better make the order in which it arrears.And then just sort for structures.Compare the second input with the right and stable result.If the score's order is wrong,output 'Error',if the name's order is wrong,output 'Not Stable',if all order are right,output 'Right'.

Code:
```
#include<cstdio>
#include<iostream>
#include<algorithm>
using namespace std;
struct node{
	string na;
	int s,i;
}p[305],pp[305];
bool cmp(node x,node y)
{
	if(x.s==y.s)	return x.i<y.i;
	return x.s>y.s;
}
int main()
{
	int n;
	while(~scanf("%d",&n))
	{
		for(int i=0;i<n;i++)
		{
			cin>>p[i].na>>p[i].s;
			p[i].i=i;
		}
		for(int i=0;i<n;i++)
		{
			cin>>pp[i].na>>pp[i].s;
		}
		sort(p,p+n,cmp);
		int flag=0;
		for(int i=0;i<n-1;i++)
		{
			if(pp[i].s<pp[i+1].s)	
			{
				flag=1;
				break;
			}
		}
		if(flag)
		{
			puts("Error");
			for(int i=0;i<n;i++)
			{
				cout<<p[i].na<<" "<<p[i].s<<"\n";
			}
		}
		else
		{
			for(int i=0;i<n;i++)
			{
				if(p[i].na!=pp[i].na)
				{
					flag=1;
					break;
				}
			}
			if(flag)
			{
				puts("Not Stable");
				for(int i=0;i<n;i++)
				{
					cout<<p[i].na<<" "<<p[i].s<<"\n";
				}
			}
			else
			{
				puts("Right");
			}
		}
	}
	return 0;
}
```

### 开门人和关门人
Description:
每天第一个到机房的人要把门打开，最后一个离开的人要把门关好。现有一堆杂乱的机房签 
到、签离记录，请根据记录找出当天开门和关门的人。 
Input
>测试输入的第一行给出记录的总天数N ( > 0 )。下面列出了N天的记录。 
每天的记录在第一行给出记录的条目数M ( > 0 )，下面是M行，每行的格式为 
证件号码 签到时间 签离时间 
其中时间按“小时:分钟:秒钟”（各占2位）给出，证件号码是长度不超过15的字符串。 

Output
>对每一天的记录输出1行，即当天开门和关门人的证件号码，中间用1空格分隔。 
注意：在裁判的标准测试输入中，所有记录保证完整，每个人的签到时间在签离时间之前， 
且没有多人同时签到或者签离的情况。 

Sample Input
>3
1
ME3021112225321 00:00:00 23:59:59
2
EE301218 08:05:35 20:56:35
MA301134 12:35:45 21:40:42
3
CS301111 15:30:28 17:00:10
SC3021234 08:00:00 11:25:25
CS301133 21:45:00 21:58:40

Sample Output
>ME3021112225321 ME3021112225321
EE301218 MA301134
SC3021234 CS301133

Problem solving:
The earliest person and the lastest person is what we should output.The way we get these two person's name is sort,sort for structures.The best thing is we can find this efficient through sort string.You can look my code carefully to understand this. 
Code:
```
#include<cstdio>
#include<iostream>
#include<algorithm>
using namespace std;
struct node{
	string n,b,e;
}p[1000];
bool cmp(node x,node y)
{
	return x.b<y.b;
}
bool ccmp(node x,node y)
{
	return x.e>y.e;
}
int main()
{
	int n;
	scanf("%d",&n);
	while(n--)
	{
		int m;
		scanf("%d",&m);
		for(int i=0;i<m;i++)
		{
			cin>>p[i].n>>p[i].b>>p[i].e;
		}
		sort(p,p+m,cmp);
		cout<<p[0].n<<" ";
		sort(p,p+m,ccmp);
		cout<<p[0].n;
		puts("");
	}
}
```
### EXCEL排序
Description:
Excel可以对一组纪录按任意指定列排序。现请你编写程序实现类似功能。
Input
>测试输入包含若干测试用例。每个测试用例的第1行包含两个整数 N (<=100000) 和 C，其中 N 是纪录的条数，C 是指定排序的列号。以下有 N 
行，每行包含一条学生纪录。每条学生纪录由学号（6位数字，同组测试中没有重复的学号）、姓名（不超过8位且不包含空格的字符串）、成绩（闭区间[0, 100]内的整数）组成，每个项目间用1个空格隔开。当读到 N=0 时，全部输入结束，相应的结果不要输出。 

Output
>对每个测试用例，首先输出1行“Case i:”，其中 i 是测试用例的编号（从1开始）。随后在 N 行中输出按要求排序后的结果，即：当 C=1 时，按学号递增排序；当 C=2时，按姓名的非递减字典序排序；当 C=3 
时，按成绩的非递减排序。当若干学生具有相同姓名或者相同成绩时，则按他们的学号递增排序。 

Sample Input
>3 1
000007 James 85
000010 Amy 90
000001 Zoe 60
4 2
000007 James 85
000010 Amy 90
000001 Zoe 60
000002 James 98
4 3
000007 James 85
000010 Amy 90
000001 Zoe 60
000002 James 90
0 0

Sample Output
>Case 1:
000001 Zoe 60
000007 James 85
000010 Amy 90
Case 2:
000010 Amy 90
000002 James 98
000007 James 85
000001 Zoe 60
Case 3:
000001 Zoe 60
000007 James 85
000002 James 90
000010 Amy 90

Problem solving:
Look the problem description carefully,and sort for structures.Easy.
Code:
```
#include<cstdio>
#include<iostream>
#include<algorithm>
using namespace std;
struct node{
	string id,na;
	int s;
}p[100008];
bool cmp1(node x,node y)
{
	return x.id<y.id;
}
bool cmp2(node x,node y)
{
		if(x.na==y.na)
		return x.id<y.id;
	return x.na<y.na;
}
bool cmp3(node x,node y)
{
	if(x.s==y.s)
		return x.id<y.id;
	return x.s<y.s;
}
int main()
{
	int n,c,j=0;
	while(scanf("%d %d",&n,&c)&&n)
	{
		j++;
		for(int i=0;i<n;i++)
		cin>>p[i].id>>p[i].na>>p[i].s;
		if(c==1)
		{
			sort(p,p+n,cmp1);
		}
		if(c==2)
		{
			sort(p,p+n,cmp2);
		}
		if(c==3)
		{
			sort(p,p+n,cmp3);
		}
		printf("Case %d:\n",j);
		for(int i=0;i<n;i++)
		cout<<p[i].id<<" "<<p[i].na<<" "<<p[i].s<<endl;
	}
}
```
### 统计同成绩学生人数
Description:
读入N名学生的成绩，将获得某一给定分数的学生人数输出。 
Input
>测试输入包含若干测试用例，每个测试用例的格式为 
第1行：N 
第2行：N名学生的成绩，相邻两数字用一个空格间隔。 
第3行：给定分数 
当读到N=0时输入结束。其中N不超过1000，成绩分数为（包含）0到100之间的一个整数。 

Output
>对每个测试用例，将获得给定分数的学生人数输出。 

Sample Input
>3
80 60 90
60
2
85 66
0
5
60 75 90 55 75
75
0

Sample Output
>1
0
2

Problem solving:
We can solve this by loop for,but I think map is exciting.
Code:
```
#include<bits/stdc++.h>
using namespace std;
int main()
{
	int n,a,m;
	while(scanf("%d",&n)&&n)
	{		
		map<int,int> ma;
		for(int i=0;i<n;i++)
		{
			scanf("%d",&a);
			ma[a]++;
		}
		scanf("%d",&m);	
		printf("%d\n",ma[m]);
	}
	return 0;
}
```
### What Is Your Grade?
Description:
“Point, point, life of student!” 
This is a ballad（歌谣）well known in colleges, and you must care about your score in this exam too. How many points can you get? Now, I told you the rules which are used in this course. 
There are 5 problems in this final exam. And I will give you 100 points if you can solve all 5 problems; of course, it is fairly difficulty for many of you. If you can solve 4 problems, you can also get a high score 95 or 90 (you can get the former(前者) only when your rank is in the first half of all students who solve 4 problems). Analogically（以此类推）, you can get 85、80、75、70、65、60. But you will not pass this exam if you solve nothing problem, and I will mark your score with 50. 
Note, only 1 student will get the score 95 when 3 students have solved 4 problems. 
I wish you all can pass the exam! 
Come on! 
Input
>Input contains multiple test cases. Each test case contains an integer N (1<=N<=100, the number of students) in a line first, and then N lines follow. Each line contains P (0<=P<=5 number of problems that have been solved) and T（consumed time）. You can assume that all data are different when 0\<p. 
A test case starting with a negative integer terminates the input and this test case should not to be processed. 

Output
>Output the scores of N students in N lines for each case, and there is a blank line after each case. 

Sample Input
>4
5 06:30:17
4 07:31:27
4 08:12:12
4 05:23:13
1
5 06:30:17
-1

Sample Output
>100
90
90
95
100

Problem solving:
'only when your rank is in the first half of all students who solve 4 problems'->This is important.What we should pay more attention to is the meaning of this problem.
Code:
```
#include<cstdio>
#include<iostream>
#include<algorithm>
using namespace std;
struct node{
	int na;
	string t;
	int s;
	int i;
}p[105];
bool cmp(node x,node y)
{
	if(x.s==y.s)	return x.t<y.t;
	return x.s>y.s;
}
bool cmp1(node x,node y)
{
	return x.i<y.i;
}
int main()
{
	int n;
	while(scanf("%d",&n)&&n>0)
	{
		int mid=0,aa=0,bb=0,cc=0,dd=0;
		for(int i=0;i<n;i++)
		{
			p[i].i=i;
			cin>>p[i].na>>p[i].t;
			if(p[i].na==5)	p[i].s=100;
			if(p[i].na==0)	p[i].s=50;
			if(p[i].na==4)	{p[i].s=90;aa++;}
			if(p[i].na==3)	{p[i].s=80;bb++;}
			if(p[i].na==2)	{p[i].s=70;cc++;}
			if(p[i].na==1)	{p[i].s=60;dd++;}
		}
		aa/=2;
		bb/=2;
		cc/=2;
		dd/=2;
		sort(p,p+n,cmp);
		
		for(int i=0;i<n;i++)
		{
			if(p[i].s==90&&aa)
			{
				p[i].s=95;
				aa--;
			}
			if(p[i].s==80&&bb)
			{
				p[i].s=85;
				bb--;
			}
			if(p[i].s==70&&cc)
			{
				p[i].s=75;
				cc--;
			}
			if(p[i].s==60&&dd)
			{
				p[i].s=65;
				dd--;
			}
		}
		sort(p,p+n,cmp1);
		for(int i=0;i<n;i++){
			cout<<p[i].s<<"\n";
		}
		puts("");
	}
}
```
### Magical Bamboos
Description:
In a magical forest, there exists N bamboos that don't quite get cut down the way you would expect.

Originally, the height of the ith bamboo is equal to hi. In one move, you can push down a bamboo and decrease its height by one, but this move magically causes all the other bamboos to increase in height by one.

If you can do as many moves as you like, is it possible to make all the bamboos have the same height?

Input
>The first line of input is T – the number of test cases.
The first line of each test case contains an integer N (1 ≤ N ≤ 105) - the number of bamboos.
The second line contains N space-separated integers hi (1 ≤ hi ≤ 105) - the original heights of the bamboos.

Output
>For each test case, output on a single line "yes” (without quotes), if you can make all the bamboos have the same height, and "no" otherwise.

Example
>Input
2
3
2 4 2
2
1 2

>Output
yes
no

Problem solving:
Sorted this array fist.If the difference of two adjacent numbers have odd,output 'no',otherwise,output 'yes'.
Code:
```
#include<cstdio>
#include<algorithm>
using namespace std;
const int maxn=1e5+7;
int a[maxn];
int main()
{
	int n;
	scanf("%d",&n);
	while(n--)
	{
		int m,flag=0;
		scanf("%d",&m);
		for(int i=0;i<m;i++)
		{
			scanf("%d",&a[i]);
		}
		for(int i=0;i<m-1;i++)
		{
			if((a[i+1]-a[i])%2!=0)
			{
				flag=1;
				break;
			}
		}
		if(flag)	puts("no");
		else	puts("yes");
	}
	return 0;
}
```
### Bear and Three Balls
Description:
Limak is a little polar bear. He has n balls, the i-th ball has size ti.

Limak wants to give one ball to each of his three friends. Giving gifts isn't easy — there are two rules Limak must obey to make friends happy:

No two friends can get balls of the same size.
No two friends can get balls of sizes that differ by more than 2.
For example, Limak can choose balls with sizes 4, 5 and 3, or balls with sizes 90, 91 and 92. But he can't choose balls with sizes 5, 5 and 6 (two friends would get balls of the same size), and he can't choose balls with sizes 30, 31 and 33 (because sizes 30 and 33 differ by more than 2).

Your task is to check whether Limak can choose three balls that satisfy conditions above.

Input
>The first line of the input contains one integer n (3 ≤ n ≤ 50) — the number of balls Limak has.
The second line contains n integers t1, t2, ..., tn (1 ≤ ti ≤ 1000) where ti denotes the size of the i-th ball.

Output
>Print "YES" (without quotes) if Limak can choose three balls of distinct sizes, such that any two of them differ by no more than 2. Otherwise, print "NO" (without quotes).

Examples
>Input
4
18 55 16 17

>Output
YES

Input
>6
40 41 43 44 44 44

Output
>NO

Input
>8
5 972 3 4 1 4 970 971

Output
>YES

Note
>In the first sample, there are 4 balls and Limak is able to choose three of them to satisfy the rules. He must must choose balls with sizes 18, 16 and 17.
In the second sample, there is no way to give gifts to three friends without breaking the rules.
In the third sample, there is even more than one way to choose balls:
1. Choose balls with sizes 3, 4 and 5.
2. Choose balls with sizes 972, 970, 971.

Problem solving:
If there have three numbers which are adjacent,output 'yes',otherwise ouput'no'.
Code:
```
#include<cstdio>
#include<algorithm>
using namespace std;
int a[100];
int main()
{
	int n,flag=0;
	scanf("%d",&n);
	for(int i=0;i<n;i++)
	{
		scanf("%d",&a[i]);
	}	
	sort(a,a+n);
	for(int i=0;i<n;i++)	
	{
		if(binary_search(a,a+n,a[i]+1)&&binary_search(a,a+n,a[i]+2))
		{
			flag=1;
			break;
		}
	}
	if(flag)	puts("YES");
	else	puts("NO");
}
```
### 今年暑假不AC
Description:
“今年暑假不AC？” 
“是的。” 
“那你干什么呢？” 
“看世界杯呀，笨蛋！” 
“@#\$%^&\*%...” 

确实如此，世界杯来了，球迷的节日也来了，估计很多ACMer也会抛开电脑，奔向电视了。 
作为球迷，一定想看尽量多的完整的比赛，当然，作为新时代的好青年，你一定还会看一些其它的节目，比如新闻联播（永远不要忘记关心国家大事）、非常6+7、超级女生，以及王小丫的《开心辞典》等等，假设你已经知道了所有你喜欢看的电视节目的转播时间表，你会合理安排吗？（目标是能看尽量多的完整节目） 
Input
>输入数据包含多个测试实例，每个测试实例的第一行只有一个整数n(n<=100)，表示你喜欢看的节目的总数，然后是n行数据，每行包括两个数据Ti_s,Ti_e (1<=i<=n)，分别表示第i个节目的开始和结束时间，为了简化问题，每个时间都用一个正整数表示。n=0表示输入结束，不做处理。 

Output
>对于每个测试实例，输出能完整看到的电视节目的个数，每个测试实例的输出占一行。

Sample Input
>12
1 3
3 4
0 7
3 8
15 19
15 20
10 15
8 18
6 12
5 10
4 14
2 9
0

Sample Output
>5

Problem solving:
Greedy,sort by the end time,and then start counting.
Code:
```
#include<bits/stdc++.h>
using namespace std;
const int maxn = 105;
struct node{
	int b,s;
}x[maxn];
bool cmp(node q,node w)
{
	return q.s<w.s;
}
int main()
{
	int n;
	while(scanf("%d",&n)&&n)
	{
		for(int i=0;i<n;i++)
		{
			cin>>x[i].b>>x[i].s;
		}
		sort(x,x+n,cmp);
		int o=x[0].s,ans=1;
		for(int i=0;i<n;i++)
		{
			if(x[i].b>=o)
			{
				ans++;
				o=x[i].s;
			}
		}
		cout<<ans<<endl;
	}
	return 0;
}
```
### The sum problem
Description:
Given a sequence 1,2,3,......N, your job is to calculate all the possible sub-sequences that the sum of the sub-sequence is M.
Input
>Input contains multiple test cases. each case contains two integers N, M( 1 <= N, M <= 1000000000).input ends with N = M = 0. 

Output
>For each test case, print all the possible sub-sequence that its sum is M.The format is show in the sample below.print a blank line after each test case. 

Sample Input
>20 10
50 30
0 0

Sample Output
>[1,4]
[10,10]
[4,8]
[6,9]
[9,11]
[30,30]

Problem solving:
Sum Formula of Equal Difference Sequences.
![](https://i.loli.net/2019/07/18/5d3012d17685519697.png)
Code:
```
#include<bits/stdc++.h>
using namespace std;
int main()
{
	int n,m;
	while(scanf("%d %d",&n,&m))
	{
		if(m==0&&m==0)	break;
		for(int i=sqrt(2*m);i>=1;i--)
		{
			int a=(m-i*(i-1)/2)/i;
			if((a*i)+i*(i-1)/2==m)	
			printf("[%d,%d]\n",a,a+i-1);
		}
		puts("");
	}
return 0;
}
```
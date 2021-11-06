# Algorithm

### 排序算法（从小到大）

![Algorithm%204f40ae2da2134d09b820cf55d8acec88/Untitled.png](Algorithm%204f40ae2da2134d09b820cf55d8acec88/Untitled.png)

1. **冒泡排序（时间复杂度为O(n^2)**
    
    ```cpp
    //从小到大排序
    arr[8];
    n = arr.length;
    flag;
    	for(int i=0; i<n-1; i++)  //第一层循环——决定排序趟数 n-1次
    {
    	flag = 1；
    	for(int j=0; j<n-1-i; j++)  //第二层循环——排序个数，每次少排一个
    	{
    		if(arr[j+1] < arr[j])
    		{
    			flag = 0;
    			temp = arr[j];
    			arr[j] = arr[j+1];
    			arr[j+1] = temp;
    		}
    	}
    	if(flag) //如果一轮下来没有排序，说明大的都在左边，顺序已经拍好，不用再排，节省时间
    		break;
    }
    ```
    

1. **选择排序（时间复杂度为O(n^2)**
    
    ```cpp
    for (int i=0; i<n-1; i++)
    {
    	for (int j=i+1; j<n; j++)
    	{
    			if (a[i] > a[j])
    			{
    					temp = a[i];
    					a[i] = a[j];
    					a[j] = temp;
    			 }
    	}
    } 
    ```
    
2. **插入排序（时间复杂度为O（n^2）**
    
    程序有序程度越高，越高效；
    
    ```cpp
    从小到大排序
    for(int i=1; i<n; i++)  //数组从开始，以第一个arr[0]为确定元素，从1开始，依次寻找插入位置
    {
    		int inserted = arr[i];//备份待插元素
    		for(int j = i-1; j>=0 && arr[j] > arr[i]; j--)
    		{
    				arr[j+1] = arr[j];//将比待插元素大的往后移
    		}
    		arr[j+1] = inserted;//将待插元素放入正确的位置
    }
    ```
    
3. **希尔排序**
    
    ```cpp
    void ShellSort(int a[])
    {
    	int increment = a.length();
    	do{
    		increment = increment/3 + 1;   //增量序列，分割区间
    		for(int i=increment+1; i<=a.length; i++)
    		{
    			 if(a[i] < a[i-increment]) //判断两个相差一个increment的数字谁大谁小
    			{
    				a[0] = a[i];
    				for(int j=i-increment; j>0 && a[0] < a[j]; j-=increment)//循环交换
    					a[j+increment] = a[j];
    				a[j+increment] = a[0];
    			}
    		}
    	}
    	while(increment > 1)
    }
    ```
    
4. **归并排序（时间复杂度为O（nlogn）**
    
    ```cpp
    数组的范围是arr[left, right],即起始下标是left，结尾的下标是right
    void mergesort(int[] arr, int[] temp, int left, int right)
    {
    	if(left < right)//当left=right时，就是递归到只有一个元素——>终止条件
    	{
    		int center = left + (right -left)/2；//【分】比center = (left + right)/2 能避免溢出
    		mergeSort(arr, temp, left, center);//【治】将左边的数组排序（left——>center)
    		mergeSort(arr, temp, center+1, right); //【治】将右边的数组排序(center+1——>right)
    		merge(arr, temp, left, center, right);//【合】
    	}
    }
    
    void merge(int[] arr, int[] temp, int left, int center, int right)
    {
    	int i= left, j=center+1;
    	for(int k=left, k<=right; k++)
    	{
    			//以center为中心，前半段有序序列和后半段有序序列开始比较大小
    			if(i > center) temp[k] = arr[j++]; //i>center表示前半段已经全部入temp，后半段剩下的就是temp后面的，直接入temp
    			else if(j > right) temp[k] = arr[i++];//j>right表示后半段都已经入temp，前半段剩下的都比后半段的大，直接入temp
    			else if(arr[i] <= arr[j]) temp[k] = arr[i++];//常规比较，谁小谁在前
    			else temp[k] = arr[j++];
    	}
    	//拷贝
    	for(int k=left; k<= right; k++)
    	{
    		arr[k] = temp[k];
    	}
    }
    ```
    
    **非递归实现归并排序**
    
    > 非递归的迭代方法，避免了递归时深度为logn的栈空间，因此空间复杂度为O(n)，并且避免递归也在时间性能上有一定的提升
    > 
    
    ```cpp
    void merge(int[] arr, int[] temp, int left, int center, int right)
    {
    	int i= left, j=center+1;
    	for(int k=left, k<=right; k++)
    	{
    			//以center为中心，前半段有序序列和后半段有序序列开始比较大小
    			if(i > center) temp[k] = arr[j++]; //i>center表示前半段已经全部入temp，后半段剩下的就是temp后面的，直接入temp
    			else if(j > right) temp[k] = arr[i++];//j>right表示后半段都已经入temp，前半段剩下的都比后半段的大，直接入temp
    			else if(arr[i] <= arr[j]) temp[k] = arr[i++];//常规比较，谁小谁在前
    			else temp[k] = arr[j++];
    	}
    	//拷贝
    	for(int k=left; k<= right; k++)
    	{
    		arr[k] = temp[k];
    	}
    }
    
    void MergePass(int sr[],int tr[],int begin, int end)
    {
    	int i=1;
    	while(i <= end - 2*begin+1) //两两归并
    	{
    		Merge(st,tr,i,i+begin-1,i-2*begin-1);
    		i += 2*begin;  //i指向两组之后的第一组，进行下一组两两归并
    	}
    	if(i<n-s+1)
    		Merge(sr,tr,i,i+begin-1,end);
    	else
    		for(int j=i; i<=end; j++)
    			tr[i] = a[i];
    }
    void MergeSort2(int a[])
    {
    	int TR=(int*)malloc(sizeof(int)*a.length())
    	int k=1;
    	while(K<a.length())
    	{
    		MergePass(a,tr,k,a.length());
    		k *= 2;
    		MergePass(tr,a,k,a.length());
    		k *= 2;
    		//为什么要MergePass两次，因为第一次是把排序后的a赋给了tr，第二次再从tr传回a
    	}
    }
    ```
    
5. **快速排序（时间复杂度为O（nlogn） 与归并相比减少了拷贝**
    
    ```cpp
    **//分割操作，方法一，单向调整**
    int partion(int a[], int left, int right)
    {
    	int temp, pivot;//pivot存放主元
    	int i, j;
    	i = left;
    	pivot = a[right];
    	for(int j=left; j<right; j++)
    	{
    		if (a[j] > pivot)
    		{
    			temp = a[i];
    			a[i] = a[j];
    			a[j] = temp;
    			i++;
    		}
    	}
    	a[right] = a[i];
    	a[i] = pivot;
    	return i; //把主元的下标返回
    }
    void QuickSort(int a[], int left, int right)
    {
    	int center;
    	int i, j;
    	int temp;
    	if(left < right)
    	{
    		center = partion(a, left, right);
    		QuickSort(a, left, center-1);
    		QuickSort(a,center+1, right);
    	}
    }
    //方法二：双向扫描
    int partion2(int[] arr, int left, int right)
    {
    	int pivot = arr[left];
    	int i = left +1;
    	int j = right;
    	while(true)
    	{
    		//向右遍历扫描
    	∵	while(i <= j && arr[i] <= pivot) i++;
    		//向左遍历扫描
    		while(i <= j && arr[j] >= pivot) j--;
    		if (i >= j) break;
    		//交换
    		int temp = arr[i];
    		arr[i] = arr[j];
    		arr[j] = temp;
    	}
    	//把arr[j] 和主元交换
    	arr[left]  = arr[j];
    	arr[j] = pivot;
    	return j; 
    }
    ```
    
    - **快速排序的优化方法**
        
        [https://blog.csdn.net/qq_19525389/article/details/81436838?utm_source=app&app_version=4.12.0&code=app_1562916241&uLinkId=usr1mkqgl919blen](https://blog.csdn.net/qq_19525389/article/details/81436838?utm_source=app&app_version=4.12.0&code=app_1562916241&uLinkId=usr1mkqgl919blen)
        
6. **堆排序**
    
    ```cpp
    void HeapSort(int a[])
    {
    	for(int i=a.length()/2; i>0; i--)	//循环有孩子的结点，且循环顺序是从右到左，从下到上，不清楚的话画一个完全二叉树
    		HeapAdjust(a,i,a.length());
    	for(int i=a.length(); i>0; i--)
    	{
    		swap(a,1,i);					//把堆顶记录和当前未经排序子序列最后一项交换——此时最后一项已经是最大的数
    		HeapAdjust(a,1,i-1);			//将a[1,i-1]重新调整为大顶堆
    	}
    }
    
    void HeapAdjust(int a[], int l, int m);	//l表示以a[l]作为根结点的完全二叉树，m = a.length;
    {
    	int temp = a[l];
    	for(int j=2*s; j<=m; j*=2)
    	{
    		if(j<m && a[j]<a[j+1])
    			j++;
    		if(temp >= a[j])
    			break;
    		a[l] = a[j];
    		l=j;
    	}
    	a[l] = temp;
    }
    ```
    

### 如何得到整型数据的二进制

```cpp
n是需要转换的整数
void convert(int n)
{
		vector<int>two;
		long long  num=n;
		while(num)
		{
				two.push_back(num%2);    //得到其二进制末尾数 —— num>>1;
				num = num / 2;
		}
		int count=0;
		for(int i=0; i<sizeof(two); i++)
		{
				if(two[i]==1)
				{
						count++;              //统计其中为1的个数
				}
		}
		cout<<count<<endl;
}
				
```

### 进制转换

以十进制为中介进行转换，例如8进制数226转成2进制

- 先将226，转成十进制，6*8^0 + 2*8^1+2*8^2 = 150
- 再将150 转换成二进制 10010110

### 快速幂和取模运算结合

- 何为取模运算
    - (a * b) % p = (a % p * b % p) % p  快速幂原理
    两项之积的取模运算 = 每个项都取模的结果相乘再取模
- 何为快速幂
    
    ![Untitled](Algorithm%204f40ae2da2134d09b820cf55d8acec88/Untitled%201.png)
    

```cpp
以对1000取模为例
对a的每一次运算都要去模是避免数值过大发生溢出
a是底数，b是指数
typedef long long lo;
lo fastpow(lo a, lo b)
{
	lo ans=1;
	while(b>0)
	{
		if(b & 1) // 如果b是奇数，b的二进制末尾是1，&运算后非0）
		{
			ans = ans * a % 1000;
			/*为何奇数才乘，如上图解释Fastpow，3^10最后等于9*6561，而9和6561
			都是当指数为奇数的底数*/
		}
		b >>= 1; //等价于b=b>>1;  b>>1 = b/2; ,就算是奇数在取整中也相等于是-1过了
		a = a * a % 1000;
		}
	return ans;
}
```

矩阵快速幂

![Untitled](Algorithm%204f40ae2da2134d09b820cf55d8acec88/Untitled%202.png)

### 匹配问题（相关符号）

```cpp
题目导入：给定一段字符串，要求匹配好字符串中类似与'('与')'
解题思路：何为匹配的字符串，即当出现一个左符号，下一个是右符号就是与之
				 匹配，反正出现左符号就是错误，且存在着就近原则，我们就思考，
				 用栈就能很好的满足，把所有左符号都存储在栈中，一旦遇到右符号就
				 抵消栈中最后加入的元素
具体代码实现：
int find(string *str, int k)//k是指行数
{
	stack<char>st;
	for(int n=0; n<k; n++)
	{
		char *ch = str[n].data();
		int len=str[n].length();
		int i=-1;
		while(++i<len)
		{
			if(ch[i] =='(' || ch[i] == '{' || ch[i] == '[')
			{
				st.push_back(ch[i]);
			}
			else if(ch[i] == '/')
			{
				if(ch[i+1] == '*')
				{
					st.push_back('<');
				}
			}
			else if (ch[i] == ')' || ch[i] == '}' || ch[i] == ']')
            {
                char c;
                if (st.empty())
                {
                    if (ch[i] == ')')
                        return 1;
                    if (ch[i] == '}')
                        return 3;
                    if (ch[i] == ']')
                        return 5;
                }
                else
                {
                    if (ch[i] == ')')
                    {
                        if ((c = st.top()) != '(')
                        {
                            return 2;
                        }
                        st.pop();
                    }
                    if (ch[i] == '}')
                    {
                        if ((c = st.top()) != '{')
                        {
                            return 4;
                        }
                        st.pop();
                    }
                    if (ch[i] == ']')
                    {
                        if ((c = st.top()) != '[')
                        {
                            return 6;
                        }
                        st.pop();
                    }
                }
            }
            else if (ch[i] == '*')
            {
                char c1;
                if (ch[i + 1] == '/')
                {
                    if (st.empty())
                    {
                        return 7;
                    }
	                    else
	                    {
	                        if ((c1 = st.top()) != '<')
	                            return 8;
	                    }
                }
            }
            else
            {
            }
        }
    }
    if (st.empty())
    {
        return 0;
    }
    else
    {
        char rest[100];
        int m = 0;
        while (!st.empty())
        {
            rest[m] = st.top();
            st.pop();
            m++;
        }
        m--;
        if (rest[m] == '(')
            return 2;
        if (rest[m] == '{')
            return 4;
        if (rest[m] == '[')
            return 6;
        if (rest[m] == '<')
            return 8;
    }
}
```

### 全排列算法

```cpp
char data1[] = "abc";
do{
		puts(data1);
}while(next_permutation(data1, data1+4));
输出:
abc
acb
bac
bca
cab
cba
/*
next_permutation(i,j);是指重新排列范围[i, j)内的元素，
按照字典排序排列下一个较大的组合

即若给定的数组不是按照顺序来的，又需要给出所有的全排列，则
需要用sort（）函数，对原数组重新排序

next_permutaion() and sort()函数都是默认从小到大less排序，
即每一个相邻的元素都会比较，如果cmp返回结果为假，那么函数就会
将他们互换位置，如果cmp返回结果为真，就会保持原来的位置不变

*倘如需要从大到小排序
则需要重新定义compare
bool compare(char i, char j)
{
			return i > j;
}
当i>j时，返回真，位置不变
*/
char data1[] = "bac";
do{
		puts(data1);
}while(next_permutation(data1, data1+4));
输出：
bac
bca
cab
cba
char data1[] = "bac";
sort(data1, data1+4);
do{
		puts(data1);
}while(next_permutation(data1, data1+4));
输出：
abc
acb
bac
bca
cab
cba

prev_permutation() 输出所有比当前排列小的排列，排序是从大到小；
```

### 实现大写转换成小写的函数

- **tolower(a)** //A-a
- 补充字母的ASCii码：**A-Z** 65-90  |   **a-z**  97-122

### 前缀和和差分

- 一维前缀和：sum[i]表示前i项和
    - **sum[i] = sum[i-1] + a[i];**
- 二维前缀和：sum[i][j]表示以(i , j)为右下角，以（1，1）为左上角所围成的矩形的和
    - 计算方法：**sum[i][j] = sum[i-1][j] + sum[i][j-1] - sum[i-1][j-1] + a[i][j];**
    - 计算以（x1，y1）为左上角，（x2，y2）为右下角的矩形的和：
        
        **sum[x2][y2] - sum[x1-1][y2] - sum[x2][y1-1] + sum[x1-1][y1-1];**
        
        该公式基于sum数组的0行0列都是0；
        
- 差分：b[i]表示第i项与第i-1项的差，即b[i] = a[i]-a[i-1];
    - 特别的b[1] = a[1]
    - 即**a[i] = b[i] + b[i-1] + b[i-2] + ...... + b[2] + a[1];**

### 二分法

1. 二分查找法（普通版本）
    
    ```cpp
    int bsearch(int *a,int x, int y, int z)
    {
    	while(x<=y)  //考虑下x可以等于y码
    	{
    		int mid = x + (y - x) / 2;
    		if(v = a[mid]) return mid;
    		else if (v<a[mid] y = mid-1;
    		else x = mid + 1;
    	}
    	return -1;
    } 
    ```
    
2. 二分法查上界
    
    寻找a的区间[x,y) 小于等于v的最后一个数的下一个数
    
    ```cpp
    int upper_bound(int *a, int x, int y, int v)
    {
    	while(x<y)
    	{
    		int mid = x + (y-x)/2;
    		if(v >= a[mid]) x=mid+1;
    		else y =mid;
    	}
    	return x;
    }
    ```
    
3. 二分法查下界
    
    寻找a的区间[x,y)中大于v的第一个数
    
    ```cpp
    int lower_bound(int *a, int x, int y, int v)
    {
    	while(x>y)
    	{
    		int mid = x + (y-x)/2;
    		if(v > a[mid]) x = mid+1;
    		else y =mid;
    	}
    	return 0;
    }
    ```
    

### 以String存储的日期（eg20211222）的递增变化（区分闰年）

```cpp
string s;
cin >> s;
int mon[13] = {0, 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};
string s1 = s;

//str.substr(pos, longth) 返回从str的pos位置开始的长度为longth的字符串
string s_day = s1.substr(6);
string s_mon = s1.substr(4, 2);
string s_year = s1.substr(0, 4);

//如果是大月（31日）
if (mon[stoi(s_mon)] == 31)
{
		//如果是大月的最后一天
    if (stoi(s_day) == 31)
    {
	        s_day = "01";//更新为一号
				//如果这个月刚好是12月 ————进一年
        if (stoi(s_mon) == 12)
        {
            s_mon = "01";
            int n = stoi(s_year);
            s_year = to_string(++n);
        }
        else
        {
            int mon = stoi(s_mon);
            s_mon = to_string(++mon);//月份+1
            if(s_mon.size()==1) //如果是个位的月，那么要补充成两位，所以补0
            {
                s_mon.insert(0,"0");
            }
        }
    }
		//不是最后一天
    else
    {
        int day = stoi(s_day);
        s_day = to_string(++day);
        if(s_day.size() == 1)//个位要补0
        {
            s_day.insert(0,"0");
        }
    }
}
//如果是小月（30日）
else if (mon[stoi(s_mon)] == 30)
{
    if (stoi(s_day) == 30)
    {
        s_day = "01";
        int mon = stoi(s_mon);
        s_mon = to_string(++mon);
        if(s_mon.size() == 1)
        {
            s_mon.insert(0,"0");
        }
    }
    else
    {
        int day = stoi(s_day);
        s_day = to_string(++day);
        if(s_day.size() == 1)
        {
            s_day.insert(0,"0");
        }
    }
}
//二月
else
{
    if (stoi(s_day) == 28)
    {
        s_day = "01";
        s_mon = "03";
    }
    else
    {
        int day = stoi(s_day);
        s_day = to_string(++day);
        if(s_day.size() == 1)
        {
            s_day.insert(0,"0");
        }
    }
}
s1.replace(0, 4, s_year);
s1.replace(4, 2, s_mon);
s1.replace(6, 2, s_day);

```

方法2（重要）

```cpp
//闰年：能被4整除但不能被100整除,或能被400整除的
int leap_year[12] = {31, 29, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};
int nonleap_year[12] = {31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};

//该convert函数 是 int型转换成string的函数to_string()的解释
void convert(int x){
	cnt = 0;
	while(x){
		str[7-cnt++] = x % 10;
		x /= 10;
	}
}
//判断是否是闰年
bool jg_leap_year(int y){
    return y % 4 == 0 && y % 100 != 0 || y % 400 == 0;
}
//计算下一天的日期
int next_day(int x){
	int y = x / 10000;  //取前四位
	int m = x % 10000 / 100; //取最后四位的前两位
	int d = x % 100;  //取最后两位
    if(d++ == (jg_leap_year(y)? leap_year[m - 1] : nonleap_year[m - 1])){
        d = 1;
        if(m++ == 12){
            y++;
            m = 1;
        }
    }
    return y * 10000 + m * 100 + d;
}

//判断是否为回文
bool jg1(int x){
	convert(x);
	for(int i = 0; i <= 3; i++){
		if(str[i] != str[7 - i]) return false;
	}
	return true;
}
//判断是否为ABABBABA型回文
bool jg2(int x){
	//首先判断是否为回文——实际上是调用 convert
	if(jg1(x) == false) return false;
	return (str[0] != str[1] && str[0] == str[2] && str[1] == str[3]);
}
```

### 递归思想

- 一般是自上往下一层层深入，再一层层把值返回
也可以自下而上，这又一般叫做递推
- 三要素
    1. 明确函数的目的（功能）
    2. 寻找递归结束的条件（避免无限死循环地调用自己）
    3. 找出函数的等价关系（不断缩小参数的范围）
    

### 动态规划Dynamic Programming

——通过数组来存储历史记录，避免我们重复计算

- 三步骤
    1. 定义数组元素的含义，eg:dp[i]，中i是表示什么，dp[i]具体的值又表示什么
    2. 找出数组元素的关系式，自上而下，eg:dp[n] = dp[n-1] + dp[n-2]; 这就是数组元素的关系式
    3. 找出初始值，只有知道dp[1]、dp[2],才能得到的dp值

[告别动态规划，连刷 40 道题，我总结了这些套路，看不懂你打我（万字长文）](https://zhuanlan.zhihu.com/p/91582909)

### 搜索

1. 深度搜索模板
    
    ```cpp
    int dfs(int t)
    {
    	if(满足输出条件）
    	{
    		输出解；
    		return ;
    	}
    	else
    	{
    		for(int i=1; i<=尝试次数; i++)
    		{
    			if(进一步满足搜索条件，例如没有障碍)
    			{
    				为进一步搜索所需的状态打上标记；
    				search(t+1);
    				恢复到打标记前；
    			}
    		 }
    		}
      }
    ```
    

### 判断质数（素数）

> 提示：质数是只能被1和自身整除的大于1的整数
> 

```python
from math import sqrt

num = int(input("请输入一个正整数: "))
end = int(sqrt(num))
is_prime = True
for x in range(2, end+1)
	if(num % x ==0)
			is_preme = False
			break;
if(is_prime):
	print("%d is prime", % num)
else:
	print("%d is not prime" % num)

```

### 输入两个正整数，计算最大公因数和最小公倍数

> 提示：最大公因数是两个数的公共因子中最大的那个数，最小公倍数是同时能够被两个数整除的最小的数，最大公因数一定小于等于两个数的最小，最小公倍数大于两个数的最大
> 

```python
x = int(input("x = "))
y = int(input("y = "))
# 如果x > y就交换，让x最小
if x>y:
# 交换操作
	x,y=y,x
# 从两个数最小的开始循环递减
for factor in range(x,0,-1)
		if x % factor == 0 and y % factor == 0
				print("最大公因数为：%d", % factor)
				print("最小公倍数为：%d", % (x // factor * y)
				break

方法2 欧几里得算法（辗转相除法）
def gcd(a,b)
	return b == 0 ? a : gcd(b,a%b)
```

### 后缀表达式

```cpp
#include <bits/stdc++.h>
using namespace std;
int beg, en;    //在后缀表达式的处理中，beg表示运算数的第一个，en表示最后一个，起定位作用
vector<string> vc; //vc用来动态存储后缀表达式 以数组的方式访问后缀表达式
stack<int> st;     //后缀表达式运算的栈
stack<char> stt;   //将中缀表达式转换成后缀表达式时用来存符号的栈
//后缀表达式的运算函数
void Postfix()
{
    int count = vc.size();
    for (int i = 0; i < count; i++)
    {
        if (vc[i] == "-" || vc[i] == "+" || vc[i] == "*" || vc[i] == "/")
        {
            int m, n, sum;
            m = st.top();
            st.pop();
            n = st.top();
            st.pop();
            if (vc[i] == "-")
                sum = n - m;
            else if (vc[i] == "+")
                sum = m + n;
            else if (vc[i] == "*")
                sum = m * n;
            else
            {
                if (m == 0)
                {
                    cout << "ILLEGAL";
                    return;
                }
                else
                    sum = n / m;
            }
            st.push(sum);
        }
        else
            st.push(stoi(vc[i]));
    }
    cout << st.top();
}

int main()
{
    //s是中缀表达式（我们运算的那种），s1是后缀表达式（给计算机运算的
    string s, s1;

    cin >> s;
    //遍历中缀表达式的每个元素
    for (int i = 0; i < s.length(); i++)
    {
        //如果是符号,
        if (s[i] < '0' || s[i] > '9') //简化后，不用把所有符号都写一遍
        {
            /*因为参加四则运算的不都是个位数，所以需要在每一个运算数后加一个'.'以示区分，
            每一个运算符之前一般都是运算数，但也有括号的情况,所以需要排除*/
            if (s[i] == '(' || s[i - 1] == ')')
            {
            }
            else
                s1.insert(s1.size(), ".");

            //如果是‘+’or‘-’
            if (s[i] == '-' || s[i] == '+')
            {
                //先判断此时栈顶的符号优先级是否更高，‘+’ ‘/’，如果是，则先把此时栈内的符号全部弹出在入栈
                //当然还有栈内为空的时候也可以入栈
                if (stt.empty() || stt.top() != '*' || stt.top() != '/')
                    stt.push(s[i]);
                else
                {
                    while (!stt.empty())    //判断栈空
                    {
                        //将此时栈顶的符号转换成string，加在s1后缀表达式后
                        char ch = stt.top();
                        string ss(1, ch);
                        s1.insert(s1.size(), ss);
                        stt.pop();
                    }
                }
            }
            //如果是')'，把两个括号之间的符号弹出
            else if (s[i] == ')')
            {
                char ch;
                ch = stt.top();
                while (ch != '(')
                {
                    string ss(1, ch);
                    s1.insert(s1.size(), ss);
                    stt.pop();
                    ch = stt.top();
                }
                stt.pop();
            }
            //如果是‘*’ ‘/’直接入栈
            else
                stt.push(s[i]);
        }

        //是数字
        else
        {
            string s2(1, s[i]);
            s1.insert(s1.size(), s2);
        }
    }
    //某些式子以‘）’结尾，那么最后的数字就没有'.'来分割 所以在最后还要在判断下此时后缀表达式的最后是不是数字
    if (s1[s1.length() - 1] >= '0' && s1[s1.length() - 1] <= '9')
        s1.insert(s1.size(), ".");
    //把栈内剩余的符号全部弹出
    while (!stt.empty())
    {
        char ch = stt.top();
        string ss(1, ch);
        s1.insert(s1.size(), ss);
        stt.pop();
    }
    //后缀表达式的处理加工，运算符、符号都依次存入vector中
    for (int i = 0; i < s1.length(); i++)
    {
        //当遍历到'.'时，表示在从beg到i-1（i是点）是一个运算数
        if (s1[i] == '.')
        {
            en = i;
            vc.push_back(s1.substr(beg, en - beg));
            beg = en + 1;//beg自动更新到下一位
        }
        if (s1[i] == '-' || s1[i] == '+' || s1[i] == '*' || s1[i] == '/')
        {
            string s3(1, s1[i]);
            vc.push_back(s3);
            beg = i + 1;    //beg自动更新到下一位
        }
        if (s1[i] == '@')
            break;
    }
    Postfix();
    return 0;
}
```

### 最大子段和

`2，-4，3，-1，2，-4，3`  求该数组的最大和——Answer`3，-1，2（4）`

**Method：**

1. 第一个数为一个有效序列
2. 如果后一个数加在前一个有效序列上，sum变大，则该数也并入该有效序列
3. 如果后一个数加在前一个有效序列上，sum变小，则该数成为一个新的有效序列
4. 比较各个有效序列，最后输出最大值

**Solution：**

2作为第一个有效序列`2`

来到第二个数-4，与2相加，得-2，相较于-4变大，所以-4要是最优序列内的，那么一定会有2

第三个数3，加上前面的序列`2，4`，得1，相较于3变小，所以3要是在最优序列内，那么一定不会有前面的2和-4

第四个数-1，如果加上前面的3，得2，相较于-1变大，所以-1要是在最优序列内，那么一定有3

第五个数2，加上前面的`3，-1` ，得4，变大了，所以要是2在最优序列，那么前面的序列一定有

第六个数-4，加上前面的`3，-1，2` ，得0，变大了，所以要是-4在最优序列，那么前面序列也会在

第七个数3，加上前面的`3，-1，2，-4` ，得3，没有变化，所以即可加入，也可成为新的有效序列

> 综上可以得知，sum和最大的是4，有效序列`3，-1，2` 为最优有效序列
> 

**Code：**

```cpp
#include <bits/stdc++.h>
using namespace std;
#define maxn 200005
int ans=-1e7;   //默认初始值为最小的数，因为不知道所给的数组是不是都是负数，在负数中选最小
int a[maxn],b[maxn];    //a数组存储数字，b[i]表示当存在a[i]时的有效序列

int main()
{
    int n;
    cin>>n;
    for(int i=1; i<=n; i++)
    {
        cin>>a[i];
        if(i==1)
            b[i] = a[i];    //第一个数就是一个最优子序列
        else
            b[i] = max(a[i],b[i-1]+a[i]);   //判断此时+a[i]后，会不会变大，变大了就加入上一个有效序列，否则自成一个新序列
        ans = max(ans,b[i]);    //实时更新最大的序列
    }

    cout<<ans;
    return 0;
}
```

### 线段树的lazytag法

- 适用于不断的区间加k，区间乘k，区间求和
- lazy－tag思想，记录每一个线段树节点的变化值，当这部分线段的一致性被破坏我们就将这个变化值传递给子区间，大大增加了线段树的效率。
在此通俗的解释我理解的Lazy意思：
现在需要对[a,b]区间值进行加c操作，那么就从根节点[1,n]开始调用update函数进行更新操作；如果刚好执行到一个rt节点，而且tree[rt].l == a && tree[rt].r == b，这时我们就应该一步更新此时rt节点的sum[rt]的值（sum[rt]+=c* (tree[rt].r - tree[rt].l + 1)）。
关键来了，如果此时按照常规的线段树的update操作，这时候还应该更新rt子节点的sum[]值，而Lazy思想恰恰是暂时不更新rt子节点的sum[]值，而是在这里打一个tag，直接return。直到下次需要用到rt子节点的值的时候才去更新，这样避免许多可能无用的操作，从而节省时间 。
- 数列数组的长度为L，那么其segment_tree结构体需要4L长度

```cpp
/*
线段树的Lazytag法，极大减少时间，适用于不断的区间加乘 和区间求和
*/
#include <bits/stdc++.h>
using namespace std;
int p;               //模数
long long a[100007]; //暂存数列的数组
//线段树结构体
struct Node
{
    long long v, mul, add;
    //v表示该节点的值，mul表示该节点的乘法lazytag，add表示为该节点的加法lazytag
} st[400007];

void buildtree(int root, int l, int r)
{
    //初始化lazytag
    st[root].add = 0;
    st[root].mul = 1;
    if (l == r)
        st[root].v = a[l];
    else
    {
        int m = (l + r) / 2;
        buildtree(root * 2, l, m);
        buildtree(root * 2 + 1, m + 1, r);
        st[root].v = st[root * 2].v + st[root * 2 + 1].v;
    }
    st[root].v %= p;
    return;
}

void pushdown(int root, int l, int r)
{
    int m = (l + r) / 2;
    //规定好的优先度，乘法优先
    st[root * 2].v = (st[root * 2].v * st[root].mul + st[root].add * (m - l + 1)) % p;
    st[root * 2 + 1].v = (st[root * 2 + 1].v * st[root].mul + st[root].add * (r - m)) % p;
    //继续维护其儿子的lazytag
    st[root * 2].mul = (st[root * 2].mul * st[root].mul) % p;
    st[root * 2 + 1].mul = (st[root * 2 + 1].mul * st[root].mul) % p;
    st[root * 2].add = (st[root * 2].add * st[root].mul + st[root].add) % p;
    st[root * 2 + 1].add = (st[root * 2 + 1].add * st[root].mul + st[root].add) % p;
    //把父节点的lazytag还原
    st[root].add = 0;
    st[root].mul = 1;
}
//乘法
void update1(int root, int stdl, int stdr, int l, int r, long long k)
{
    //假如本区间和所给区间没有交集
    if (r < stdl || l > stdr)
        return;
    //假如给出的区间包含本区间
    if (l <= stdl && stdr <= r)
    {
        st[root].v = (st[root].v * k) % p;
        st[root].mul = (st[root].mul * k) % p;
        st[root].add = (st[root].add * k) % p;
        return;
    }
    //假如给出的区间和本区间有交集，也有不交叉的地方
    //先维护lazytag——因为要往下探索，所以之前欠着的操作要完成
    pushdown(root, stdl, stdr);
    int m = (stdl + stdr) / 2;
    update1(root * 2, stdl, m, l, r, k);
    update1(root * 2 + 1, m + 1, stdr, l, r, k);
    st[root].v = (st[root * 2].v + st[root * 2 + 1].v) % p;
    return;
}
//加法
void update2(int root, int stdl, int stdr, int l, int r, long long k)
{
    //假如本区间和所给区间没有交集
    if (r < stdl || l > stdr)
        return;
    //假如给出的区间包含本区间
    if (l <= stdl && stdr <= r)
    {
        st[root].add = (st[root].add + k) % p;
        st[root].v = (st[root].v + k * (stdr - stdl + 1)) % p;
        return;
    }
    //假如给出的区间和本区间有交集，也有不交叉的地方
    //先维护lazytag——因为要往下探索，所以之前欠着的操作要完成
    pushdown(root, stdl, stdr);
    int m = (stdl + stdr) / 2;
    update2(root * 2, stdl, m, l, r, k);
    update2(root * 2 + 1, m + 1, stdr, l, r, k);
    st[root].v = (st[root * 2].v + st[root * 2 + 1].v) % p;
    return;
}
//求和
long long query(int root, int stdl, int stdr, int l, int r)
{
    if (r < stdl || l > stdr)
    {
        return 0;
    }
    if (l <= stdl && stdr <= r)
        return st[root].v;
    pushdown(root, stdl, stdr);
    int m = (stdr + stdl) / 2;
    return (query(root * 2, stdl, m, l, r) + query(root * 2 + 1, m + 1, stdr, l, r)) % p;
}
int main()
{
    int n, m;
    scanf("%d%d%d", &n, &m, &p);
    for (int i = 1; i <= n; i++)
    {
        scanf("%lld", &a[i]);
    }
    buildtree(1, 1, n);
    while (m--)
    {
        int chk;
        scanf("%d", &chk);
        int x, y;
        long long k;
        if (chk == 1)
        {
            scanf("%d%d%lld", &x, &y, &k);
            update1(1, 1, n, x, y, k);
        }
        else if (chk == 2)
        {
            scanf("%d%d%lld", &x, &y, &k);
            update2(1, 1, n, x, y, k);
        }
        else
        {
            scanf("%d%d", &x, &y);
            printf("%lld\n", query(1, 1, n, x, y));
        }
    }
    return 0;
}
```

**关于乘法优先的解释**

比如现在有3个数1,2,31,2,3

```cpp
            1~3(1)
           /     \
      1~2(2)      3(3)
     /      \
  1(4)      2(5)

```

**我们先给1~3加上2**,画个小小小小的图，**节点后面的括号代表节点下标**

所以

t[1].add+=2;*t*[1].*add*+=2;

t[1].sum+=((3-1)+1)*2;*t*[1].*sum*+=((3−1)+1)∗2;

**我们再给1~3乘上3**

所以

t[1].mu*=3;*t*[1].*mu*∗=3;

**我们再给1~3加上4，那是不是先加再乘**

t[1].add+=4;*t*[1].*add*+=4;

obviously我们发现不能先加：

```cpp
操作2之后的式子是:
sum=(a[1]+2)*3+(a[2]+2)*3+(a[3]+2)*3;

```

如果直接加:

```cpp
式子是:
sum=(a[1]+2+4)*3+(a[2]+2+4)*3+(a[3]+2+4)*3;
   =(a[1]+2)*3+4*3+(a[2]+2)*3+4*3+(a[3]+2)*3+4*3;

```

我们发现这和

```cpp
sum=(a[1]+2)*3+4+(a[2]+2)*3+4+(a[3]+2)*3+4;

```

并不等价

而要等价必须这样

```cpp
sum=(a[1]+2+4/3)*3+(a[2]+2+4/3)*3+(a[3]+2+4/3)*3;

```

**我们发现这样就成了实数运算了,还有可能除成无限小数**

而先乘后加:

```cpp
sum=(a[1]*3+2*3+4)+(a[2]*3+2*3+4)+(a[3]*3+2*3+4);
```

### 约瑟夫环问题——两种题型

大家都知道约瑟夫环吧？现在这里有 *n* 个数围成的环，从第一个人开始喊 1 每个喊到 *n*−1的人要出去，下一个人要从 1开始喊。

现在我想知道第一个出去的人的编号是多少。

第一行一个数 n 表示有n个人 (1<=n<=1e100)

```cpp
/*
约瑟夫环的两种题型
1. 人数极限大（unsigned long long 也装不下），找出第一个（n-1）出去的人
2. 人数可以用Long long 装下，数到m按照顺序全部出列
*/
#include <bits/stdc++.h>
using namespace std;
int num[100]; //最大数据为1e100，即最长有100位

int main()
{
    string s;
    cin >> s; //数据过大，只能用string来装（数组）

    //最特殊的情况，只有一个人，只能他出去
    if (s.size() == 1 && s[0] == '1')
    {
        cout << 1;
        return 0;
    }

    //字符到数值的转换
    for (int i = 0; i < s.size(); i++)
        num[i] = s[i] - '0';

    //第n-1个人出队，就是对n-1，输出这个数，但是这个数无法进行减法运算
    //直接模拟减法运算：后一个数减一，如果小于0，就往前一位借1，加10
    num[s.size() - 1]--; //个位减一
    //判断借位 函数
    for (int i = s.size() - 1; i >= 1; i--) //第一位不能在往前借，所以停在>=1
    {
        if (num[i] < 0)
        {
            num[i] += 10;
            num[i - 1] -= 1;
        }
        else
            break;
    }

    if (num[0] != 0)
        cout << num[0];
    for (int i = 1; i < s.size(); i++)
    {
        cout << num[i];
    }

    return 0;
}
```

n 个人围成一圈，从第一个人开始报数,数到 mm 的人出列，再由下一个人重新从 11 开始报数，数到 mm 的人再出圈，依次类推，直到所有的人都出圈，请输出依次出圈人的编号

```cpp
#include <bits/stdc++.h>
using namespace std;

typedef struct Node
{
    int num;
    struct Node *next;
} Node, *Linklist;

// //头插法——不适合做循环链的初始化
// void initial(Linklist *L, int n)
// {
//     (*L) = (Linklist)malloc(sizeof(Node));
//     (*L)->next=nullptr;
//     for (int i = n; i >= 1; i--)
//     {
//         Linklist s = (Linklist)malloc(sizeof(Node));
//         s->num = i;
//         s->next = (*L)->next;
//         (*L)->next = s;
//     }
// }

//尾插法
void initial(Linklist *L, int n)
{
    Linklist p, r;//尾插法，需要一个新结点p，和指向尾结点的r
    //链表L的初始化（建立头指针）
    (*L) = (Linklist)malloc(sizeof(Node));
    (*L)->next = nullptr;
    r = (*L);
    for (int i = 1; i <= n; i++)
    {
        p = (Linklist)malloc(sizeof(Node));
        p->num = i;
        r->next = p;    //插在尾结点后
        r = p;  //尾结点更新
    }
    (*L) = (*L)->next; //删除头结点，头指针直接指向第一结点，方便尾指针
    r->next = (*L); //尾结点的next指向第一结点，构成循环链表
}

void del(Linklist *L, int pos)
{
    Linklist s, r;
    s = (*L);
    while (s->next->num != pos)
        s = s->next;
    r = s->next;
    cout << r->num << " ";
    if(r->num == (*L)->num)
    {
        (*L)= (*L)->next;
    }
    s->next = r->next;
    free(r);
}
int main()
{
    Linklist l;
    int n, m;
    cin >> n >> m;
    //链表的初始化
    initial(&l, n);
    //在对链表进行变更操作（update，delete.etc)时，要在设置一个指针，一开始指向头指针
    //变更中也进行移动变化
    Linklist e;
    e = l;
    while (n)
    {

        for (int i = 1; i <= m - 2; i++)
            e = e->next;
        del(&l, e->next->num);
        //
        e = e->next;
        n--;
    }
    return 0;
}
```

关于while循环哪里的解释

![836FF64CB8F1F3B2A9FB7FA9E70A189D.png](Algorithm%204f40ae2da2134d09b820cf55d8acec88/836FF64CB8F1F3B2A9FB7FA9E70A189D.png)

### 完全二叉树/满二叉树的建树、更新问题

```cpp
//满二叉树、完全二叉树的建立用数组更合适方便，空间利用率高
int a[maxn], tree[maxn][2];    //tree[i][0]左子树、tree[i][1]右子树
int num, n;
//已知最后的叶子结点数据，一层层往上更新，这里的更新是让结点的值等于其左右儿子的最大值
void update()
{
    for (int i = num - 1; i > 0; i--)
    {
        tree[i][0] = a[i * 2];
        tree[i][1] = a[i * 2 + 1];
        a[i] = max(tree[i][0], tree[i][1]);
    }
}
```

### 树的前中后序问题

1. 树的结点是以整数给出（不是一位数的那种——只能用数组来解决的
    
    > 题目：给定一棵二叉树的后序遍历和中序遍历，请你输出其层序遍历的序列。这里假设键值都是互不相等的正整数
    > 
    
    ```cpp
    #include <bits/stdc++.h>
    using namespace std;
    const int MAX = 2e5 + 5;
    
    struct Node {
    	int val,l,r;
    } node[MAX];
    int tot;
    int c[MAX],b[MAX]; 
    
    int dfs(int len,int b[],int c[]) {//中序，后序 
    	if(len <= 0) return -1;
    	if(len == 1) {
    		node[++tot].val = b[1];
    		node[tot].l=node[tot].r = -1;
    		return tot;
    	}
    	node[++tot].val = c[len];
    	int res = tot;
    	int l;
    	for(l = 1; l<=len; l++) {
    		if(b[l] == c[len]) break;
    	}
    	node[res].l = dfs(l-1,b,c);
    	//node[res].r = dfs(len-l,b+l-1,c+l);
    	node[res].r = dfs(len-l,b+l,c+l-1); //传递指针，b+l表示传递b数组的第l+1个开始
    	return res;
    } 
    void bfs() {
    	queue<int> q;
    	q.push(1);
    	while(q.size()) {
    		int cur = q.front();q.pop();
    		if(cur != 1) printf(" ");
    		printf("%d",node[cur].val);
    		if(node[cur].l != -1) q.push(node[cur].l);
    		if(node[cur].r != -1) q.push(node[cur].r);
    	}
    }
    int main()
    {
    	int n;
    	cin>>n;
    	for(int i = 1; i<=n; i++) scanf("%d",c+i);
    	for(int i = 1; i<=n; i++) scanf("%d",b+i);
    	dfs(n,b,c);
    	//printf("%d",node[1].val);
    	bfs();
    	return 0 ;
    }
    ```
    
2. 树的结点是单个数字或字母（可以用string来解决
    
    > 题目：给出一棵二叉树的中序与后序排列。求出它的先序排列。（约定树结点用不同的大写字母表示，长度\le 8≤8）
    > 
    
    ```cpp
    #include <bits/stdc++.h>
    using namespace std;
    
    void get_pre(string in, string aft)
    {
        if (aft.empty())
            return;
        int num = aft.size();
        char root = aft[num - 1];
        aft.erase(num - 1);
        int k = in.find(root);
    
        string leftin = in.substr(0, k);
        string rightin = in.substr(k + 1);
        string leftaft = aft.substr(0, k);
        string rightaft = aft.substr(k);
    
        cout << root;
        get_pre(leftin, leftaft);
        get_pre(rightin, rightaft);
    }
    int main()
    {
        string inor, neor;
        cin >> inor >> neor;
        get_pre(inor, neor);
    
        return 0;
    }
    ```
    
    1. 已知后序（前序）+中序求层序
    
    > 算法：根据已知的后序和中序建立一颗二叉树，再把该二叉树bfs遍历输出
    > 
    
    ```cpp
    #include <bits/stdc++.h>
    using namespace std;
    const int MAX = 2e5 + 5;
    
    struct Node {
    	int val,l,r;
    } node[MAX];
    int tot;
    int c[MAX],b[MAX]; 
    
    int dfs(int len,int b[],int c[]) {//中序，后序 
    	if(len <= 0) return -1;
    	if(len == 1) {
    		node[++tot].val = b[1];
    		node[tot].l=node[tot].r = -1;
    		return tot;
    	}
    	node[++tot].val = c[len];
    	int res = tot;
    	int l;
    	for(l = 1; l<=len; l++) {
    		if(b[l] == c[len]) break;
    	}
    	node[res].l = dfs(l-1,b,c);
    	//node[res].r = dfs(len-l,b+l-1,c+l);
    	node[res].r = dfs(len-l,b+l,c+l-1); //传递指针，b+l表示传递b数组的第l+1个开始
    	return res;
    } 
    void bfs() {
    	queue<int> q;
    	q.push(1);
    	while(q.size()) {
    		int cur = q.front();q.pop();
    		if(cur != 1) printf(" ");
    		printf("%d",node[cur].val);
    		if(node[cur].l != -1) q.push(node[cur].l);
    		if(node[cur].r != -1) q.push(node[cur].r);
    	}
    }
    int main()
    {
    	int n;
    	cin>>n;
    	for(int i = 1; i<=n; i++) scanf("%d",c+i);
    	for(int i = 1; i<=n; i++) scanf("%d",b+i);
    	dfs(n,b,c);
    	//printf("%d",node[1].val);
    	bfs();
    	return 0 ;
    }
    ```
    

### 最长公共子序列

Longest Commom Sequence

**Definition：**如果一个序列S，分别是两个或多个序列的子序列，且是所有符合次条件序列中最长的，则S称为这两个或多个已知序列的最长公共子序列

**Related Definitions**

- **字符子串：**指字符串中连续的n个字符，如abcdefg中的ab，de等
- **字符子序列：**指字符串中不一定连续但先后顺序一致的n个字符，例如abcdef中的acd、cef等，dae就不是，因为它们与字符串的顺序不一致
- 公共子序列：如果序列C是序列A的子序列，还是序列B的子序列，那么序列C就可以称为序列A和序列B的公共子序列，那么最长公共子序列，就是序列A和序列B的所有公共子序列中最长的那个，公共子序列不唯一，LCS也不唯一

**LCS长度求法：**

我们用Ax表示序列A的连续前x项构成的子序列，即Ax= a1,a2,……ax, By= b1,b2,……by, 我们用LCS(x, y)表示它们的最长公共子序列长度，那原问题等价于求LCS(m,n)。为了方便我们用L(x, y)表示Ax和By的一个最长公共子序列。让我们来看看如何求LCS(x, y)。我们令x表示子序列考虑的最后一项，考虑能不能把最后一项元素t加公共子序列上，y同理

（1） Ax ＝ By

```
那么它们L(Ax, By)的最后一项一定是这个元素！
   
为什么呢？为了方便，我们令t = Ax = By, 我们用反证法：假设L(x,y)最后一项不是t，则要么L(x,y)为空序列（别忘了这个），要么L(x,y)的最后一项是Aa＝Bb ≠ t, 且显然有a < x, b < y。无论是哪种情况我们都可以把t接到这个L(x,y)后面,从而得到一个更长的公共子序列。矛盾！
   如果我们从序列Ax中删掉最后一项ax得到Ax-1,从序列By中也删掉最后一项by得到By-1，(多说一句角标为0时，认为子序列是空序列)，则我们从L(x,y)也删掉最后一项t得到的序列是L(x – 1, y - 1)。为什么呢？和上面的道理相同，如果得到的序列不是L(x - 1, y - 1)，则它一定比L(x - 1, y - 1)短（注意L（，）是个集合！），那么它后面接上元素t得到的子序列L(x,y)也比L(x - 1, y - 1)接上元素t得到的子序列短，这与L(x, y)是最长公共子序列矛盾。因此L(x, y) = L(x - 1, y - 1) 最后接上元素t，LCS(Ax, By) = LCS(x - 1, y - 1) + 1。

```

（2）  Ax ≠ By

```
    仍然设t = L(Ax, By), 或者L(Ax, By)是空序列（这时t是未定义值不等于任何值）。则t  ≠ Ax和t  ≠ By至少有一个成立，因为t不能同时等于两个不同的值嘛！

```

（2.1）如果t  ≠ Ax，则有L(x, y)= L(x - 1, y)，因为根本没Ax的事嘛。

```
        LCS(x,y) = LCS(x – 1, y)

```

（2.2）如果t  ≠ By,l类似L(x, y)= L(x , y - 1)

```
        LCS(x,y) = LCS(x, y – 1)
   可是，我们事先并不知道t，由定义，我们取最大的一个，因此这种情况下,有LCS(x,y) = max(LCS(x – 1, y) , LCS(x, y – 1))。看看目前我们已经得到了什么结论：

```

<aside>
💡 LCS(x,y) =
(1) LCS(x - 1,y - 1) + 1      （Ax ＝ By）
(2) max(LCS(x – 1, y) , LCS(x, y – 1))    （Ax ≠ By）

</aside>

这时一个显然的递推式，光有递推可不行，初值是什么呢？显然，一个空序列和任何序列的最长公共子序列都是空序列！所以我们有:

<aside>
💡 LCS(x,y) =
(1) LCS(x - 1,y - 1) + 1 如果Ax ＝ By
(2) max(LCS(x – 1, y) , LCS(x, y – 1)) 如果Ax ≠ By
(3) 0 如果x = 0或者y = 0

</aside>

## 强连通图

### 定义

图1不是， 图2是

> 强连通图：
> 

[https://bkimg.cdn.bcebos.com/pic/8d5494eef01f3a29a0571f389325bc315d607cad?x-bce-process=image/watermark,image_d2F0ZXIvYmFpa2UxNTA=,g_7,xp_5,yp_5/format,f_auto](https://bkimg.cdn.bcebos.com/pic/8d5494eef01f3a29a0571f389325bc315d607cad?x-bce-process=image/watermark,image_d2F0ZXIvYmFpa2UxNTA=,g_7,xp_5,yp_5/format,f_auto)

## 查找

### 查找概论

- 查找表：被查数据所在的集合 || 由同一类型的数据元素（记录）构成的集合
- 关键字：数据元素中的某个数据项（结构体中的数据类型，eg学生结构体的string 学号num）
    - Primary Key（主关键字）：唯一标识项，不同的记录不同的主关键字
    - Secondary Key（次关键字）：对同一条数据元素（记录）除了主关键字外的其他数据项
        
        ![QQ图片20211025195203.png](Algorithm%204f40ae2da2134d09b820cf55d8acec88/QQ%E5%9B%BE%E7%89%8720211025195203.png)
        
- Static Search Table（静态查找表）：只做查找
- Dynamic Search Table（动态查找表）：在查找的同时做插入删除操作

### 顺序表的查找

> 以数组的形式（非链式），有序or无序都算
> 

```cpp
哨兵查找
int Sequence_Search(int a[], int n, int key){
		int i= n; //从最后的一位元素开始往前查
		a[0] = key;//a数组就是查找表，查找元素在[1,n]的范围，a[0] 就是哨兵
		while(a[i] != key)
			i--;
		return i; //return 0 means fail to find
}
compare一般的查找——就是从头比到尾（for循环）
每一次比较节省了判断i是否出界(i<=n)
在数据量较大时能节省较多时间
```

- 通常对于无序表的查找情况，只能采取顺序查找，即从头到尾依次遍历，判断关键字是否和给定值相等，这种线性查找算法的时间复杂度为O(n)

### 有序表查找

- 折半查找（二分查找） O(logn)

> 每次取中间记录作为查找
> 

```cpp
int Binary_search(int *a,int key)
{
	int l,r;
	l = 1;
	r = n;
	while(l <= r)
	{
		int mid = (l + r) / 2; //mid = l + 1/2(r - l)
		if(a[mid] == key)
			return mid;
		else if(a[mid] > key)
		{
			r = mid - 1;
			continue;
		}
		else if(a[mid] < key)
		{
			l = mid + 1;
			continue;
		}
	}
	return 0;
}
//递归算法
int Binary_search(int *a, int l, int r, int key)
{
	if(l == r)
	{
		if(a[l] = key;
			return l;
		else
			return 0;
	}
	
	int mid = (r+l) / 2;
	if(a[mid] == key)
		return mid;
	else if(a[mid] > key)
		return Binary_search(a,l,mid-1,key);
	else if(a[mid] < key)
		return Binary_search(a,mid+1, r, key);
}
```

- **插值查找 O(logn)**
    - ——对于折半查找每次都从中间查找的进一步优化（当有序表内的数据并不均匀分布时，例如`a[] = {0,1,9999,10000,10001.....};`折半查找的效率就会大打折扣
    而插值查找只需修改折半查找得到mid的方程：上面的折半查找的mid方程，下面是插值查找的mid方程

$$mid = \frac{r+l}{2}=l+\frac{1}{2}(r-l)$$

$$mid=l+\frac{key-a[l]}{a[r]-a[l]}(r-l)$$

把 $\frac{1}{2}$ 转换成 $\frac{key-a[l]}{a[r]-a[l]}$是根据关键字key与查找表中最大最小记录的关键字进行比较后的查找方法，对于分布不规律的能显著提高查找效率

- **斐波那契查找——利用黄金分割理论 O(logn)**

      详细说明见《大话数据结构》p256

### 线性索引查找

> 索引就是把一个关键字与它对应的记录相关联的过程
索引按照结构可以分成：线性索引、树形索引和多级索引
> 

线性索引——将索引项集合组织为线性结构，即索引表

- **稠密索引**
    
    是指在线性索引中，将数据集的每个记录都对应一个索引项，且对于稠密索引这个索引表来说，索引项一定是按照关键码有序排列的
    
    不足：因为稠密索引是每一个数据元素都对应一个索引，当数据元素特别大时，对应的稠密索引表也会特别大，在空间和访问时间效率上都不够好
    
- **分块索引——图书馆分区管理**
    
    把数据集的记录分成若干块，并且这些块需要满足两个条件：块内无序，块间有序
    
    对于分块有序的数据集，每一个块都对应一个索引，而此时该索引项结构为：
    
    - 最大关键码：它存储每一块中的最大关键字，以保证下一块的所有数据元素的关键字都比上一块大
    - 块中记录的个数：方便查找
    - 块首指针：方便对块的遍历
    
    鉴于分块索引的块之间是有序的，所以在查找的时候也可以用折半、插值查找进一步节省时间
    
- **倒排索引——基础搜索技术**
    
    根据相同类型的数据元素，我们提取出所有元素的属性，并制成索引表，例如两句英文，我们把这两句英文中出现的所有单词按照顺序排列出一张单词表，并且单词表后都有相对应的编号，标识该单词出现在该编号的句子里，**这种倒过来通过属性来定位元素的索引方法就是倒排索引**
    

### HashTable

<aside>
💡 散列技术是在记录的存储位置和它的关键字之间建立一个确定的对应关系f，使得每个关键字key对应一个存储位置$f(key)$,这里我们把对应关系成为散列函数（哈希函数），采用这种思想建立的表就是散列表（哈希表）

</aside>

散列技术既是一种存储技术，也是一种查找技术，散列表与线性表、树和图等数据结构相比，元素之间没有逻辑联系，数据元素只与关键字有关——因此散列表主要是面向查找的数据结构

在理想情况下的哈希表，每个关键字对应的地址都是不同的，但是现实中常常遇见两个关键字不等$key1 ≠ key2$,但是$f(key1)=f(key2)$ ,这种现象我们称为冲突，而对于评判一个哈希表的好与坏，就是从两个纬度来判断：**选择什么哈希函数能避免更多的冲突？在遇到不可避免的confilt时怎么更好的处理confilt？**

- **Hash function的构造方法**
    
    follow principle：计算简单，散列地址分布均匀
    
    - 直接定址法：对于连续分布且量小的关键字的情况下，适合选用线性函数来解决地址
    $f(key) = a * key + b$
    - 数字分析法：对于一些位数比较多且统一的但没有分布规律的数字，如电话号码，我们可以利用其数字信息，前三位是运营商，中间四位是地区，后四位才是用户号，所以对于大量号码，前七位很有可能一致，所以我们可以采取后四位作为$f(key)$,还可以对后四位进行进一步处理，如反转，前两数和后两数相加等处理方法，进一步避开冲突
    - 平方取中法：对于位数不是很多也不知道分布规律的数字，可以对其平方，再取中间3位的数作为$f(key)$
    - 折叠法：对于位数比较多且不统一，也不知道分布规律的数字，可以对其从左到右分割成位数相等的几部分（最后不够的时候可以短一点），将这几部分叠加求和，并按哈希表表长取后几位作为哈希地址，eg: 9876543210 ——> 987 | 654 | 321| 0 , 求和$987+654+321+0=1962$，取后三位962作为$f(key)$
    - 除留余数法：对于绝大部分情况都适用，也是最常见的哈希函数，对于哈希表表长为m的哈希函数为：$f(key) = key\mod p(p \leq m)$
    - 随机数法：$f(key) = random(key)$，在查找的时候使用与存储时同一个随机种子
- **处理Confilt的方法**
    - 开放地址法：最常见的处理冲突方法，经常与除留余数法连用，具体是一旦发生了冲突，就去寻找下一个空的散列地址，只要散列表足够大，空的散列地址总能找到，并将记录存下
    $f(key) = (f(key) + 1) \mod m$
    - 再散列函数：准备多个散列函数，当一个发生冲突时换另外一个函数试，但这就会造成空间利用的不确定性
    - 链地址法：不去考虑有冲突就去换地方，对于$f(key1) = f(key2)$，就把key1和key2存储在一条单链表上
    - 公共溢出区法：为所有冲突的关键字建立一个公共的溢出区来存放

**HashTable代码**

```cpp
#include <iostream>
#include <cstdio> 
using namespace std;
#define SUCCESS 1
#define UNSUCCESS 0
#define maxn 20
#define NULLKEY -32768

//create the structrue of hashtable
typedef struct
{
	int *elem;
	int count;
}HashTable;

int m = 0;

//initialize the hashtable
bool InitHashTable(HashTable *h)
{
	m = maxn;
	h->elem = (int*)malloc(m * sizeof(int));
	for(int i=0; i<m; i++)
		h->elem[i] = NULLKEY;
	return 1;
}

//Hash function(varieties/diversty,choose the best base on the fact)
int Hash(int key)
{
	return key % m;
}

//Insert the key into HashTable
void InsertHash(HashTable *h, int key)
{
	int addr = Hash(key);
	//开放地址的线性探索 
	while(h->elem[addr] != NULLKEY)
	{
		addr = (addr + 1) % m;
	}
	h->elem[addr] = key;
}

bool SearchHash(HashTable h, int key, int *addr)
{
	*addr = Hash(key);
	while(h.elem[(*addr)] != key)
	{
		*addr = ((*addr) + 1) % m;
		if(h.elem[*addr] == NULLKEY || (*addr) == Hash(key))
			return UNSUCCESS;
	}
	return SUCCESS;
 } 
 
int main()
{
	HashTable H;
	int a[] = {12,67,56,16,25,37,22,29,15,47,48,34};
	InitHashTable(&H);
	for(int i=0; i<12; i++)
		InsertHash(&H,a[i]);
	for(int i=0; i<12; i++)
	{
		int addr;
		bool flag;
		flag = SearchHash(H,a[i],&addr); 
		if(flag == true)
			printf("hash[%d] = %d\n", addr, H.elem[addr]);
		else
			printf("Not find\n");	
	}
	return 0;
}
```

## Tarjan算法

### 遍历过程

例子1：

例子2：

### 算法过程分析

> i : 记录上述遍历的访问顺序，时间戳 （对应代码中的 dn[]）j : 本身所能达到的最低时间戳 (对应代码中的is[n])
> 

例子1：

> 输入数据：5 5
1 2
2 3
3 4
4 5
5 2
> 

例子2：

> 输入数据：7 9
1 2
2 3
3 4
4 2
3 5
4 5
1 6
6 7
7 1
> 

### 代码

```cpp
#include<bits/stdc++.h>

using namespace std;

int a[10][10]; //记录有无边
int n, m;

stack<int >st;
int low[10], dn[10];    
int tim;
bool is[10];

void DFS(int x)
{
	dn[x] = low[x] = ++tim;
	st.push(x);
	is[x] = true;
	for(int y=1; y<=n; y++){
		//能够到达的点
		if(a[x][y] == 1){
			if(dn[y] == 0){
			//y点没有被访问
			  DFS(y);
			  low[x] = min(low[x], low[y]);
			} else if(is[y]){
				//判断有没有组成强连通分量
				low[x] = min(low[x], low[y]);
			}
		}
	}
	if(dn[x] == low[x]){
		while(!st.empty() ){
			int top = st.top();
			cout << top << " ";
			st.pop();
			is[top] = false;
		    if(top == x) break;
		}
	    cout << endl;
	}
}

int main()
{
	cin >> n >> m;

	for(int i=1; i<=m; i++){
		int x, y;
		cin >> x >> y;
		a[x][y] = 1;
	}
	for(int i=1; i<=n; i++){
		if(!dn[i]) DFS(i);
	}

	return 0;
}

```
# training
#力扣算法第1题



int* twoSum(int* nums, int numsSize, int target, int* returnSize)
{
	for (int i = 0; i < numsSize; i++)
	{
		for (int j = i + 1; j < numsSize; j++)
		{
			if (target == nums[i] + nums[j])
			{
				//返回字符串的方式
				/*char* str = NULL;
				str = (char*)malloc(5 * sizeof(char));
				strcpy(str, "[i,j]");
				return str;*/
				//难点，不知如何定义数组
				*returnSize = 2;//空间为2
				int* ans = (int*)malloc(2 * sizeof(int));
				ans[0] = i, ans[1] = j;
				return ans;//返回[i,j]，既返回数组
			}
		}
	}
	*returnSize = 0;
	return NULL;//忘记考虑不存在情况
}

二刷
int* twoSum(int* nums, int numsSize, int target, int* returnSize)
{
	*returnSize = 2;
	int* arr = (int*)malloc(2 * sizeof(int));
	int i, j;
	for (i = 0; i < numsSize; i++)
//若写为i<j，在初始化时，j 的值还没有被赋予（处于上一个循环的值），会导致未定义。
	{
		for (j = i + 1; j < numsSize; j++)
//需要将初始化 j 的操作移动到循环体内（for循环第一个式子一定为j=...）
		{
			if (target == nums[i] + nums[j])
			{
				arr[0] = i;
				arr[1] = j;
				return arr;
			}
		}
	}
	//为空则要释放arr的内存，并返回空
	free(arr);
	return NULL;
}
三刷
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target)
    {
        unordered_map<int,int>map;
        vector<int>res;
        for(int i=0;i<nums.size();i++)
        {
            auto iter=map.find(target-nums[i]);//找下标,iter蕴含两个下标（二维数组）
            if(iter!=map.end())
            {
                res.push_back(iter->second);
                res.push_back(i);//vector多用push_back
                return res;
            }
            else
            {
                map.insert(pair<int,int>(nums[i],i));//必须先注明pair才能插入
            }
        }
        return res;
    }
};

#力扣算法第2题

#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include<stdlib.h>
#include<string.h>
#define SIZE 1000000000
//#define TSIZE 45

//struct film
//{
//	char title[TSIZE];
//	int rating;
//	struct film* next;//指向链表的下一个结构
//};
////s_gets(char* st, int n);
//int main()
//{
//
//	getchar();
//	getchar();
//	return 0;
//}
bool isPalindrome(int x)
{
	if (x < 0)
	{
		return false;
	}
	//x有几位
	int k = 0;
	int arr[100];
	int a = x;//移花接木，避免对x造成影响
	while (a)
	{
		a /= 10;//若是取模，则会进入死循环
		k++;
	}
	//问题是x的初始值已被改变,目前不会解决
	printf("%d", x);
	//x存入动态数组
	for (int m = 0; m < k; m++)
	{
		arr[m] = x % 10;
		x = (x - arr[m]) / 10;
	}
	//首末比较，不同的返回false
	int i, j;
	for (i = 0, j = k - 1; i < j; i++, j--)
	{
		if (arr[i] != arr[j])
		{
			return false;
		}
	}
	return true;

	////方法二
	//char* a = (char*)malloc(100 * sizeof(char));//搞算法时少用这个malloc，慢
	////100是字符串的长度

	////方法三
	////char[100]a;//更快

	//sprintf(a, "%d", x);//把整数x转化为字符串存入a中。
	//int len_l = 0,len_r = 0;//有趣的赋值格式
	//len_r = strlen(a) - 1;//右边的下标值
	//for (len_l, len_r; len_l < len_r; len_l++, len_r--)
	//{
	//	if (a[len_l] != a[len_r])
	//	{
	//		return false;
	//	}
	//}
	//return true;
}
int main()
{
	if (isPalindrome(1869449681))
	{
		printf("对");
	}
	else
	{
		printf("错");
	}
	return 0;
}

//罗马数字换算

int romanToInt(char* s)
{
	
	int sum = 0;//求和
	int j= strlen(s);
	//思路：把字符数组转换成数字数组
	int n[16];
	for (int i = 0; i < j; i++)
	{
		//列情况
		switch (s[i])
		{
		case 'I':
			n[i] = 1;
			break;
		case 'V':
			n[i] = 5;
			break;
		case 'X':
			n[i] = 10;
			break;
		case 'L':
			n[i] = 50;
			break;
		case 'C':
			n[i] = 100;
			break;
		case 'D':
			n[i] = 500;
			break;
		case 'M':
			n[i] = 1000;
			break;
		default:
			break;
		}
	}
	for (int k = 0; k < j ; k++)
	{
		if (n[k] >= n[k + 1])
		{
			sum += n[k];
		}
		else
		{
			sum -= n[k];
		}
	}
	return sum;
}

int main()
{
	char s[8] = {"III"};

	printf("%d", romanToInt(s));
	return 0;
}

//27题
 int removeDuplicates(int* nums, int numsSize)
 {
	 int number = numsSize;
	 for (int i = 0; i < numsSize-1; i++)
	 {
		 if (nums[i] == nums[i + 1])
		 {
			 nums[i + 1] = NULL;
			 number -= 1;
		 }
	 }//计算number的数值
	 int newnum[30000];
	 int* p = &nums[0];
	 int* q = &newnum[0];//创立新数组
	 for (p,q; p < &nums[0] +numsSize; )
	 {
		 if (*p != NULL)
		 {
			*q = *p;
			p++;
			q++;
		 }	 
		 else
		 {
			 p++;
		 }
	 }
	 
	 for (int k = 0; k < number; k++)
	 {
		 printf("%d  ", newnum[k]);
	 }
	 printf("----------------------------------\n");
	 return number;
 }

 int main()
 {
	 int arr[5] = { 1,3,4,4 };
	 printf("%d", removeDuplicates(arr, 5));
	 return 0;
 }

 //第27题
  int removeElement(int* nums, int numsSize, int val)
 {
	 int* p = &nums[0];//别忘写&取地址
	 int number = 0;
	 for (int i = 0; i < numsSize; i++)
	 {
		 if (nums[i] == val)
		 {

		 }
		 else
		 {
			 *p = nums[i];
			 p++;
			 number++;
		 }
	 }
	 return number;
 }


 int main()
 {
	 int arr[4] = { 4,4,4,4 };
	 printf("%d", removeElement(arr, 4, 4));
	 return 0;
 }

 //35题
 int searchInsert(int* nums, int numsSize, int target)
 {
	 for (int i = 0; i < numsSize; i++)
	 {
		 if (nums[i] == target)
		 {
			 return i;
		 }
	 }
	 //不存在时
	 if (target < nums[0])
		 return 0;
	 for (int j = 0; j < numsSize-1; j++)
	 {
		 if (nums[j] <= target && target < nums[j + 1])
		 {
			 return j + 1;
		 }
	 }
	 return numsSize;
 }


 int main()
 {
	 int arr[4] = { 1,3,5,6 };
	 printf("%d", searchInsert(arr, 4, 0));
	 return 0;
 }

//88题
void merge(int* nums1, int nums1Size, int m, int* nums2, int nums2Size, int n)
{
	int* end1 = &nums1[0] + m - 1;
	int* end2 = &nums2[0] + n - 1;
	int* end = &nums1[0] + m + n - 1;//一开始end与end1不同
	while (end1 >= &nums1[0] && end2 >= &nums2[0])
	{
		if (*end1 >= *end2)
		{
			*end = *end1;
			end--;
			end1--;//仅最后会重叠
		}
		else 
		{
			*end = *end2;
			end--;
			end2--;
		}
	}
	while (end2 >= &nums2[0])
	{
		*end = *end2;
		end--;
		end2--;
	}
}

int main()//测试的代码
{
	int nums1[6] = { 1,2,8,0,0,0 };
	int nums2[3] = { 2,5,6 };
	merge(nums1, 6, 3, nums2, 3, 3);
	for (int i = 0; i < 6; i++)
	{
		printf("%d  ", nums1[i]);
	}
	return 0;
}


//94题
struct TreeNode
{
	int val;
	struct TreeNode* left,*right;
};

void preorder(struct TreeNode* root, int* res, int* resSize)
{
	//resSize作为指针，便于更改resSize所对应的值
	//res是数组
	if (root == NULL)return;
	preorder(root->left, res, resSize);
	res[*(resSize)] = root->val;//挨个赋值
	(*resSize)++;//
	preorder(root->right, res, resSize);
}

int* inorderTraversal(struct TreeNode*root,int*returnSize)
{	
	int* res = (int*)malloc(2000 * sizeof(int));
	*returnSize = 0;
	preorder(root, res, returnSize);//初值为零，为数组第一个元素
	return res;
}


//回溯算法
//77题
//1.定义全局变量，一个存放结果，一个存放存结果的数组
//1.两个整型变为全局是便于迭代。
int* path;
int pathTop;
int** ans;
int ansTop;

void backtracking(int n, int k, int startIndex)
{
	//加上终止条件,深度为k时，把结果存入数组
	if (pathTop == k)
	{
		//因为直接将path数组的地址放入二维数组ans中
		// 会使path数组中的值随着回溯而变化
		//所以要创建新的数组存储path的值
		int* temp = (int*)malloc(k * sizeof(int));
		//能存k个int值，是一维数组
		int i;
		for (i = 0; i < k; i++)
		{
			temp[i] = path[i];//每项依次赋值
		}
		ans[ansTop] = temp;//ans[0]={1,2,3,4,...,k};
		ansTop++;//变为ans[1];
		return;//退出第k层迭代（------------！！！！-----------）
	}
	int j;
	for (j = startIndex; j <= n; j++)//递归

		//也可以改成for(j=startIndex;j<n-k+pathtop+1;j++)//值可以凑，更快
	{
		//把当前节点放入path数组
		path[pathTop] = j;
		pathTop++;
		backtracking(n, k, j + 1);
		//上一层刚return回来，就要进行回溯
		pathTop--;//进行回溯，将数组最上层节点弹出
	}
}

int** combine(int n, int k, int* returnSize, int** returnColumnSizes)
{
	path = (int*)malloc(k*sizeof(int));//path的存储标准与temp相同
	//k*sizeof(...)说明存储量为k个
	ans = (int**)malloc(10000 * sizeof(int*));//存指针的数组
	pathTop = ansTop = 0;//确定初值

	backtracking(n, k, 1);
	//返回ans数组
	*returnSize = ansTop;//ansTop要动态变化
	*returnColumnSizes = (int*)malloc((*returnSize) * sizeof(int));
	//存储一列的容量
	int i;
	for (i = 0; i < *returnSize; i++)
	{
		(*returnColumnSizes)[i] = k;
	}
	return ans;
}

//移动窗口
//209题

int minSubArrayLen(int target, int* nums, int numsSize)
{
	int minSize = numsSize+1;//注意
	int len = 0;
	int i = 0;
	int sum = 0;
	//考虑终止条件
	int sumTest = 0;
	for (int k = 0; k < numsSize; k++)
	{
		sumTest += nums[k];
	}
	if (sumTest < target)
	{
		return 0;
	}
	for (int j = 0; j < numsSize; j++)
	{
		sum += nums[j];//只加一项
		//求出j不动时，i的最大值
		while (sum >= target)
		{	
			len = j - i + 1	;
			if (minSize >= len)
			{
				minSize = len;
			}
			sum -= nums[i];
			i++;
		}
		
		//希望小于目标值就会被舍弃
	}
	return minSize;
}

//移动窗口
//3题
int lengthOfLongestSubstring(char*s)
{
	int left, right = 0;
	int cnt, result = 0;//记录当前值和结果值
	int temp[128] = { 0 };
	int slen = strlen(s);//128位数组存储子串中任意字符
	while (right<slen)
	{
		if (temp[s[right]] == 0)
		{
			temp[s[right]] = 1;
			right++;
			cnt++;
			result = cnt > result ? cnt : result;//比较
		}
		else
		{
			temp[s[left]] = 0;//因为在循环之初，左指针与右指针对应的值相等
			left++;
			cnt--;//最初肯定是一，删成0之后还会加成一
		}
	}
	return result;
}

//59题（螺旋矩阵）
int** generateMatrix(int n, int* returnSize, int** returnColumnSizes)
{
	*returnSize = n;
	*returnColumnSizes = (int*)malloc(n * sizeof(int));
	int** arr = (int**)malloc(400 * sizeof(int*));
	for (int i = 0; i < n; i++)
	{
		arr[i] = (int*)malloc(n * sizeof(int));
		(*returnColumnSizes)[i] = n;
	}
	//标定循环次数(一轮循环消去两行)!!!
	int times = 0;
	//发现起始横纵坐标很重要
	int x = 0;
	int y = 0;
	//发现边界频繁出现，所以必须设置参数
	int xmax = n - 1;
	int ymax = n - 1;
	//要遵循左闭右开的要求来达成循环
	if (n % 2 == 0)
	{
		int num = 1;
		while ((times < n / 2)&&(num<n*n+1))//记住一轮循环哪些值发生了变化
		{
			for (x=times,y=times; x < xmax; x++)//x<n-1是为了留头去尾
			{
				arr[x][y] = num;
				num++;
			}
			for (x=xmax,y; y < ymax; y++)
			{
				arr[x][y] = num;
				num++;
			}
			for (y=ymax,x; times<x ; x--)
			{
				arr[x][y] = num;
				num++;
			}
			for (x=times,y; times<y; y--)
			{
				arr[x][y] = num;
				num++;
			}
			xmax--;
			ymax--;
			times++;
		}

		return arr;
	}
	else
	{
		int num = 1;
		while ((times < n / 2) && (num < n * n + 1))
		{
			for (x = times, y = times; x < xmax; x++)//x<n-1是为了留头去尾
			{
				arr[x][y] = num;
				num++;
			}
			for (x = xmax, y; y < ymax; y++)
			{
				arr[x][y] = num;
				num++;
			}
			
			for (y = ymax, x; times < x; x--)
			{
				arr[x][y] = num;
				num++;
			}
			
			for (x = times, y; times < y; y--)
			{
				arr[x][y] = num;
				num++;
			}
			xmax--;
			ymax--;
			times++;
		}	
		//最后一项单独赋值
		arr[(n - 1) / 2][(n - 1) / 2] = n * n;
		return arr;
	}
}


#力扣算法第203题
struct ListNode
{
	int val;
	struct ListNode* next;
};
struct ListNode* removeElements(struct ListNode* head, int val)
{
	struct ListNode* temp;
	/*if (head == NULL)
	{
		return head;
	}*/
	//只是处理头结点的数据，处理完并未结束
	while (head&&head->val == val)
		//逻辑判断顺序，1不过2不看,在这里无影响
	{
		temp = head;
		head = head->next;//head已经改变，所以需要提前存储之前的,用temp
		free(temp);

	}
	//注意，这是单项链表,无 pro
	struct ListNode* current=head;
	while (current&&(temp=current->next))
//while (head->next&&head) 和 while (head&&head->next) 是有区别的
//前者先判断 head->next 是否为非空，再判断 head 是否为非空。
//后者先判断 head 是否为非空，再判断 head->next 是否为非空。
		//head->next->next为空也没事
		//current无论选择if/else都一直在迭代更新
	{
		if (temp->val == val)
		{
			current->next = current->next->next;
			//head->next已经改变，所以需要提前存储之前的,用current
			free(temp);
		}
		//因为还要循环，但不能改变head的值（还要返回他）
		else
		{
			current = current->next;//current变化，head没变
		}	
	}
	return head;
}

方法二，虚拟头结点法
struct ListNode
{
	int val;
	struct ListNode* next;
};

struct ListNode*removeElements(struct ListNode*head,int val)
{
	//创建虚拟头结点
	struct ListNode* dummyhead = (struct ListNode*)malloc(sizeof(struct ListNode));
	dummyhead->next = head;
	//遍历需要(而且删掉current对head有影响)
	struct ListNode* current = dummyhead;
	while (current->next)
	{
		if (current && current->next->val == val)
		{
			//替罪羊
			struct ListNode* temp = current->next;
			current->next = current->next->next;
			free(temp);
		}
		//通盘考虑后
		else
		{
			current = current->next;
		}
	}
	return dummyhead->next;
}

#力扣算法第206题
struct ListNode
{
	int val;
	struct ListNode* next;
};

//双指针法
struct ListNode* reverseList(struct ListNode* head)
{
	//先在头结点变化
	struct ListNode* post = (struct ListNode*)malloc(sizeof(struct ListNode));
	struct ListNode* current = (struct ListNode*)malloc(sizeof(struct ListNode));
	post = NULL;
	current = head;
	//生成替罪羊temp
	struct ListNode* temp = (struct ListNode*)malloc(sizeof(struct ListNode));
	//temp = current->next;//不知cuurrent有无下一个的值
	//画图发现current就是修改后的头结点
	while (current)
	{
		temp = current->next;
		current->next = post;
		post = current;
		current = temp;
	}
	//若current->next==NULL，又因current=current->next，NULL不能做头结点
	return post;
}

//递归法
struct ListNode* reverse(struct ListNode* post, struct ListNode* current)
{
	if (!current)
	{
		return post;
	}
	else
	{
		//生成替罪羊temp
	/*	struct ListNode* temp = (struct ListNode*)malloc(sizeof(struct ListNode));*/
		struct ListNode* temp = current->next;
		current->next = post;
		/*post = current;*/
		/*current = temp;*/
		return reverse(current,temp);
	}
}
struct ListNode* reverseList(struct ListNode* head)
{
	return reverse(NULL, head);
}

#-----动态规划--------------------------------------------------------------
#力扣算法第509题
int fib(int n)
{
	//确定dp数组含义，dp[i]是第i个项，dp[i]为第i个数组值,
	int dp[32];
	dp[0] = 0;
	dp[1] = 1;

	//终止条件
	if (n == 0)return 0;
	else if (n == 1)return 1;

	//递推公式 dp[n]=dp[n-1]+dp[n-2];
	else
	{
		//遍历顺序，由后向前
		//dp数组初始化
		for (int i = 2; i < n+1; i++)
		{
			dp[i] = dp[i - 1] + dp[i - 2];
		}
	}
	return dp[n];
	//打印数组检验
}

#力扣算法第70题
int climbStairs(int n)
{
	//确定dp数组含义，dp[i]表示到第i级台阶能用的不同方法
	int dp[47];
	dp[1] = 1;
	dp[2] = 2;
	if (n == 1)return 1;
	else if (n == 2)return 2;
	else
	{
		//递推公式:dp[i]=dp[i-1]+dp[i-2];
		for (int i = 3; i < n+1; i++)
		{
			dp[i] = dp[i - 1] + dp[i - 2];
		}
	}
	return dp[n];
}

#力扣算法第746题

一刷
int minCostClimbingStairs(int* cost, int costSize)
{
	//定价格
	int totalCost = 0;
	int dp[1002];

	//dp数组含义:dp[i]指到第i层的花费
	//递归
	/*dp[0] = 0;
	dp[1] = 0;*/
	//初值,不用for循环（不用算每一层的值）
	//for (int i = 2; i < costSize+2; i++)
	//{
	//	dp[i] = dp[i - 2] + cost[i - 2] > dp[i - 1] + cost[i - 1] ? dp[i - 2] + cost[i - 2] : dp[i - 1] + cost[i - 1];
	//}

	//从第0层出发和从第1层出发
	int dp0 = 0;
	int dp1 = 0;
	for (int i = 2; i < costSize+1; i++)
	{
		int dpi = dp0 + cost[i - 2] > dp1 + cost[i - 1] ? dp1 + cost[i - 1] : dp0 + cost[i - 2];
		dp0 = dp1;
		dp1 = dpi;
	}
	return dp1;
}

#力扣算法第62题
int uniquePaths(int m, int n)
{
	if (m == 1 && n == 1)
	{
		return 1;
	}
	//dp数组含义,dp[i][j],到（i，j）的不同路数
	int dp[102][102];
	//递归方式
	//初始值
	dp[0][0] = 0;
	
	//特殊：要给一列，一行全补上初始值
	
	//注意：延每一列、行只有一种走法（勿忘dp数组的含义）
	for (int j = 1; j < m; j++)
	{
		dp[0][j] = 1;
	}
	for (int i = 1; i < n; i++)
	{
		dp[i][0] = 1;
	}

	//问题：排列边界不等长，要用不同边界判断标准
	/*for (int i = 1, j = 1; (i < n)&& (j < m); i++, j++)
	{
		dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
	}*/

	int i = 1;
	int j = 1;
	
		//遍历顺序 重点：二维数组的遍历
	for (i=1; i < n; i++)
	{
		//不重置j的值，每次i循环j就不会变了
		for (j=1; j < m; j++)
		{
			dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
		}
	}
	return dp[n - 1][m - 1];
}

int main()
{
	//打印结果
	printf("%d", uniquePaths(7,3 ));
	return 0;
}


-------------------------------------------------------哈希表----------------------------------
#力扣算法第1478题
int sumOfUnique(int* nums, int numsSize)
{
	//哈希表精髓：hash[arr[i]]意为存储arr[i]这个值出现的次数
	int hash[102];
	memset(hash, 0, sizeof(hash));//把哈希表所有位变为0（sizeof(hash)不可改为numsSize）
	for (int i = 0; i < numsSize; i++)
	{
		hash[nums[i]]++;
		printf("hash[nums[%d]]=%d\n", i, hash[nums[i]]);
	}
	//求和
	int sum = 0;
	//j的范围是nums数组项的最大值
	for (int j = 0; j < 101; j++)
	{
		if (hash[j] == 1)
		{
			sum += j;
		}
	}
	return sum;
}

#力扣算法第242题
bool isAnagram(char* s, char* t)
{
	char hashs[26];
	char hasht[26];
	memset(hashs, 0, sizeof(hashs));
	memset(hasht, 0, sizeof(hasht));
	for (int i = 0; i < strlen(s); i++)
	{
		//压缩大小
		hashs[s[i]-'a']++;
	}
	for (int i = 0; i < strlen(t); i++)
	{
		hasht[t[i]-'a']++;
	}
	//哈希数组的大小
	for (char j = 0; j < 26; j++)
	{
		if (hashs[j] != hasht[j])
		{
			return false;
		}
	}
	return true;
}

#力扣算法第1题
class Solution
{
public:
	vector<int>twoSum(vector<int>& nums, int target)
	{
		std::unordered_map<int, int>map;
		for (int i = 0; i < nums.size(); i++)
		{
			//遍历当前元素，并在map中寻找是否有匹配的k
			//auto:根据后面的值判断变量的类型（目的：简化变量初始化过程）
			//eg.	auto x1=5
			auto iter = map.find(target - nums[i]);
			//如果iter的值在map中有相等的项
	//map.end() 返回一个特殊的迭代器，指向映射的结尾位置的下一个位置。
			//它并不指向有效的元素，主要用于表示不存在的情况。
			if (iter != map.end())
			{
				//因为题目中说只有一个符合条件
			//i是被判断元素的下标，iter->second是因为数组第i项下标为i-1
				return { i,iter->second };
			}
			//向map里插入项，便于之后找到合适的
			map.insert(pair<int, int>(nums[i], i));
		}
		return {};
	}
};

#力扣算法第15题
class Solution
{
public:
	vector<vector<int>> threeSum(vector<int>&nums)
	{
		int begin, left, right;
		vector<vector<int>>res;
		//先排好序(从小到大)，事半功倍
		for (int i = 0; i < nums.size()-1; i++)
		{
			for (int j = i + 1; j < nums.size(); j++)
			{
				if (nums[i] >= nums[j])
				{
					int temp = nums[i];
					nums[i] = nums[j];
					nums[j] = temp;
				}
			}
		}

		for (int i = 0; i < nums.size(); i++)
		{
			//排序后第一个元素>0，那么直接返回空
			if (nums[i] > 0)return res;
			//
			if (i > 0 && nums[i] == nums[i - 1])continue;
			
			if (nums[begin] > 0)
			{
				return res;
			}
			left = i+1;
			right = nums.size() - 1;
			while (right > left)
			{
				if (nums[i] + nums[left] + nums[right] > 0)
				{
					right--;
				}
				else if (nums[i] + nums[left] + nums[right] < 0)
				{
					left++;
				}
				else
				{
					res.push_back(vector<int>{nums[i], nums[left], nums[right]});
					//去重
					while (right > left && nums[right] == nums[right - 1])right--;
					while (right > left && nums[left] == nums[left + 1])left--;

					right--;
					left++;
				}
			}
		}
		return res;
	}
};

int main()
{
	vector<int>nums = { -1,0,1,2,-1,-4 };
	Solution solution; // 创建 Solution 对象
	vector<vector<int>> result = solution.threeSum(nums); // 调用成员函数获取结果
	for (int i = 0; i < 3; i++)
	{
		printf("%d  ",result[i]);
	}
	;
}

#力扣算法第541题
class Solution
{
public:
	string reverseStr(string s, int k)
	{
		for (int i = 0; i < s.size(); i += 2 * k)
		{
		/*	int* num;
			*num = k;
			char* cur = (char*)malloc((*num) * sizeof(char));
			for (i; i < k+i; i++)
			{
				cur[i] = s[i];
			}*/
			//尾部不超出
			if (i + k <= s.size())
			{
				/*swap(k个);的高级用法*/
				reverse(s.begin()+i,s.begin()+i+k);
			//continue终止本次循环，进行接下来的循环（所以i+=2不能放下面）
				continue;
			}
			//尾部超出（只取剩余部分的）
			//!!!
			reverse(s.begin() + i, s.end());
		}
		return s;
	}
};


----------------------------------------------------栈  ------------------------------------------------------------
#力扣算法第20题
class Solution
{
public:
	bool isValid(string s)
	{
		//设置栈
		stack<char>buffer;
		
		//对进栈的每一个数据进行条件判断
		for (int i = 0; i < s.size(); i++)
		{
			
			if (buffer.empty())
			{
				buffer.push(s[i]);
				//完成后立即不执行接下来的语句
				continue;
			}

			//这行代码在栈 buffer 是空的时候就会造成错误。当栈为空时调用 top() 函数将导致未定义行为。
			// 因此，在访问栈顶元素之前，应该先检查栈是否为空。
			// 
			//这在内部定义，保证每一次循环都取buffer的新top
			char top = buffer.top();
			//配对后就出栈
			if (s[i] == ')' && top == '(' 
				|| s[i] == ']' && top == '[' 
				|| s[i] == '}' && top == '{')
			{
				buffer.pop();
				continue;
			}

			//s[i]=='{','[','('
			else
			{
				buffer.push(s[i]);
				
				//top++;//不需要，因为push会直接把新的s[i]
			}
			
		}
		return buffer.empty();
	}
};

#力扣算法第1047题
class Solution
{
public:
	string removeDuplicates(string s)
	{
		stack<char>tar;
		//times用来计数，算出栈的初始容量
		int times = 0;
		for (int i = 0; i < s.size(); i++)
		{
			if (tar.empty())
			{
				tar.push(s[i]);
				times++;
				continue;
			}
			char top = tar.top();
			if (top == s[i])
			{
				tar.pop();
				times--;
				continue;
			}
			tar.push(s[i]);
			times++;
		}
		//栈转字符串
		string res;
		if (tar.empty())
		{
			return res;
		}
		for (int i = 0; i < times; i++)
		{
			//取出栈的顶部值
			res.push_back(tar.top());
			tar.pop();
		}
		reverse(res.begin(),res.end());
		return res;
	}
};

#力扣算法第3题
class Solution
{
public:
	int lengthOfLongestSubstring(string s)
	{
		unordered_set<char>vec;
		int left = 0;
		int right = 0;
		int res = 0;//取max
		if (s.empty())return 0;
		/*vec.insert(s[0]);难点：不能多插入*/
		while (right<s.size())
		{
			//不存在
			if (vec.find(s[right]) == vec.end())
			{
				vec.insert(s[right++]);
				res = max(res, right - left);
			}
			else
			{
				//key
				vec.erase(s[left++]);
			
			}
		}
		return max(res, right - left);
	}
};

-----------------------------------------------------------二叉树--------------------------------------------------
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
						迭代法
class Solution {
public:
    vector<int> preorderTraversal(TreeNode* root) {
        stack<TreeNode*> st;
        vector<int> result;
        if (root == NULL) return result;
        st.push(root);
   //每一次循环，都会把该节点的左右结点压入栈，而压入栈的栈顶又会充当树的中间结点
        while (!st.empty()) {
            TreeNode* node = st.top();// 中
								//弹出尾结点
            st.pop();
            result.push_back(node->val);
            if (node->right) st.push(node->right);           // 右（空节点不入栈）
            if (node->left) st.push(node->left);             // 左（空节点不入栈）
        }
        return result;
    }

};

#力扣算法第102题
 struct TreeNode {
      int val;
      TreeNode *left;
      TreeNode *right;
      TreeNode() : val(0), left(nullptr), right(nullptr) {}
      TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
      TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 };
 
class Solution {
public:
	vector<vector<int>> levelOrder(TreeNode* root) {
        //构建队列
        queue<TreeNode*>que;
        //树为空，返回空
        if (root != NULL)que.push(root);
        //返回的数组为二维数组，每一行的元素数量不同，取决于循环的轮数
        vector<vector<int>>res;
        while (!que.empty())
        {
            vector<int>vec;
            //!!!要会使用迭代，因为每一层数组存储的数目不同
            //!!!这里一定要用固定大小的size，因为que.size()不断变化的。
            int size = que.size();
            for (int i = 0; i < size; i++)
            {
                //!!!每次都会取动态的顶部
                TreeNode* node = que.front();
                vec.push_back(node->val);
                //弹出顶部的值
                que.pop();
                //!!!前提是含有这个值
                if(node->left)que.push(node->left);
                if (node->right)que.push(node->right);
            }
            res.push_back(vec);
        }
        return res;
	}
};

#力扣算法第226题
class Solution {
public:
    TreeNode* invertTree(TreeNode* root)
    {
        //存储
        queue<TreeNode*>que;
        if (root == NULL)return NULL; 
        //!!!不需要的操作，因为root的指向可以通过cur
       /* TreeNode* res = root;*/
        
        que.push(root);
        /*while (cur)*/
        while (!que.empty())
        {
            int size = que.size();
            for (int i = 0; i < size; i++)
            {
                //!!!便于que顶部弹出后操作
                TreeNode* cur = que.front();
                que.pop();
                //!!!可以改变指针的值
                swap(cur->left, cur->right);
                if (cur->left)
                {
                    //!!!上下结合来看，两个操作是平行的，会使cur的值发生cur->left->right的改变
                    /*cur = cur->left;*/
                    que.push(cur->left);
                }
                if (cur->right)
                {
                    //!!!上下结合来看，两个操作是平行的，会使cur的值发生cur->left->right的改变
                    /*cur = cur->right;*/
                    que.push(cur->right);
                }
            }
        }
        return root;
    }
};

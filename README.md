# training
力扣算法第一题



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

#力扣算法第二题

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

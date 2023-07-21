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

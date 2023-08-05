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

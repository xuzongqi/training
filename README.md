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

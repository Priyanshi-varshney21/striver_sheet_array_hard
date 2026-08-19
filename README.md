# striver_sheet_array_hard
#PASCAL'S TRIANGLE
def pascalTriangleI(self, r, c):
        n=r-1
        k=c-1
        result=1
        for i in range(k):
            result=result*(n-i)//(i+1)
        return result

#MAJORITY ELEMENT 1
def majorityElement(self, nums: List[int]) -> int:
        n=len(nums)
        freq=0
        ans=0
        for i in range(n):
            if(freq==0):
                ans=nums[i]
            if (ans==nums[i]):
                freq+=1
            else:
                freq-=1
        return ans

#MAJORITY ELEMENT 2'
def majorityElement(nums):
    n = len(nums)
    count1 = 0
    count2 = 0
    candidate1 = None
    candidate2 = None
    for num in nums:
        if num == candidate1:
            count1 += 1
        elif num == candidate2:
            count2 += 1
        elif count1 == 0:
            candidate1 = num
            count1 = 1
        elif count2 == 0:
            candidate2 = num
            count2 = 1
        else:
            count1 -= 1
            count2 -= 1
    # Verify candidates
    result = []
    for candidate in [candidate1, candidate2]:
        if nums.count(candidate) > n // 3:
            result.append(candidate)
    return result

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

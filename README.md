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

#THREE SUM
def threeSum(nums):
    nums.sort()
    ans = []
    for i in range(len(nums) - 2):
        if i > 0 and nums[i] == nums[i - 1]:
            continue
        left = i + 1
        right = len(nums) - 1
        while left < right:
            total = nums[i] + nums[left] + nums[right]
            if total == 0:
                ans.append([nums[i], nums[left], nums[right]])
                left += 1
                right -= 1
                while left < right and nums[left] == nums[left - 1]:
                    left += 1
                while left < right and nums[right] == nums[right + 1]:
                    right -= 1
            elif total < 0:
                left += 1
            else:
                right -= 1
    return ans

#4 SUM
def fourSum(self, nums, target):
        nums.sort()
        ans=[]
        for i in range(len(nums)-3):
            for j in range(i+1,len(nums)-2):
                left=j+1
                right=len(nums)-1
                while left<right:
                    total=nums[i]+nums[j]+nums[left]+nums[right]
                    if total==target:
                        ans.append([
                            nums[i],
                            nums[j],
                            nums[left],
                            nums[right]
                            ])
                        left+=1
                        right-=1
                    elif total<target:
                        left+=1
                    else:
                        right-=1
        return ans

#LONGEST SUBARRAY WITH SUM 0
def maxLen(self, arr):
        freq={}
        ans=0
        sum_=0
        for i in range(len(arr)):
            sum_+=arr[i]
            if sum_==0:
                ans=i+1
            if sum_ in freq:
                ans=max(i,i-freq[sum_])
            else:
                freq[sum_]=i
        return ans

#COUNT SUBARRAYS WITH GIVEN XOR K
def subarraysWithXorK(self, nums, k):
        xor=0
        count=0
        freq={0:1}
        for num in nums:
            xor^=num
            if xor^k in freq:
                count+=freq[xor^k]
            freq[xor]=freq.get(xor,0)+1
        return count

#ERASE OVER LAP INTERVAL 
def` eraseOverlapIntervals(self, nums: List[List[int]]) -> int:
        nums.sort(key=lambda x:x[1])
        count=0
        end=float('-inf')
        for start,finish in nums:
            if start>=end:
                end=finish
            else:
                count+=1
        return count

#MERGE OVERLAPPING SUBINTERVALS
def mergeOverlap(self, intervals):
        # Your code goes here
        intervals.sort()
        ans=[]
        current_start=intervals[0][0]
        current_end=intervals[0][1]
        for i in range(1,len(intervals)):
            start=intervals[i][0]
            end=intervals[i][1]
            if start<=current_end: #overlapping
                current_end=max(end,current_end)
            else:#NO overlapping
                 ans.append([current_start,current_end])
                 current_start=start
                 current_end=end
        ans.append([current_start,current_end])
        return ans


#MERGE TWO SORTED ARRAYS WITHOUT USING AN EXTRA SPACE
nums1 = [-5, -2, 4, 5]
nums2 = [-3, 1, 8]
n = len(nums1)
m = len(nums2)
gap = (n + m + 1) // 2
while gap > 0:
    i = 0
    j = gap
    while j < n + m:
        if i < n and j < n:
            if nums1[i] > nums1[j]:
                nums1[i], nums1[j] = nums1[j], nums1[i]
        # i in nums1, j in nums2
        elif i < n and j >= n:
            if nums1[i] > nums2[j - n]:
                nums1[i], nums2[j - n] = nums2[j - n], nums1[i]
        # Both elements are in nums2
        else:
            if nums2[i - n] > nums2[j - n]:
                nums2[i - n], nums2[j - n] = nums2[j - n], nums2[i - n]
        i += 1
        j += 1
    if gap == 1:
        break
    gap = (gap + 1) // 2
print(nums1)
print(nums2)

# FIND THE REPEATING AND MISSING NUMBERS 
def findMissingRepeatingNumbers(self, nums):
        freq={}
        ans=[]
        for n in nums:
            if n in freq:
                freq[n]+=1
            else:
                freq[n]=1
        for i in range(1, len(nums) + 1):
            if i in freq and freq[i] > 1:
                ans.append(i)
        for i in range(1, len(nums) + 1):
            if i not in freq:
                ans.append(i)
        return ans

#COUNT INVERSIONS
def countInversions(arr):
    def merge_sort(low, high):
        if low >= high:
            return 0
        mid = (low + high) // 2
        count = merge_sort(low, mid)
        count += merge_sort(mid + 1, high)
        i = low
        j = mid + 1
        temp = []
        while i <= mid and j <= high:
            if arr[i] <= arr[j]:
                temp.append(arr[i])
                i += 1
            else:
                temp.append(arr[j])
                # Count inversions
                count += mid - i + 1
                j += 1
        while i <= mid:
            temp.append(arr[i])
            i += 1
        while j <= high:
            temp.append(arr[j])
            j += 1
        for k in range(len(temp)):
            arr[low + k] = temp[k]
        return count
    return merge_sort(0, len(arr) - 1)

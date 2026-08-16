# striver_sheet_array_hard
#PASCAL'S TRIANGLE
def pascalTriangleI(self, r, c):
        n=r-1
        k=c-1
        result=1
        for i in range(k):
            result=result*(n-i)//(i+1)
        return result

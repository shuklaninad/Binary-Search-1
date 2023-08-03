# Binary-Search-1


## Problem1 
## Search a 2D Matrix(https://leetcode.com/problems/search-a-2d-matrix/)
## For a matrix with 'm' rows and 'n' columns, TC = O(log(m*n)), SC = O(1)
class Solution:
    def searchMatrix(self, matrix: List[List[int]], target: int) -> bool:
        if matrix == None or len(matrix) == 0:
            return False
        
        m = len(matrix)
        n = len(matrix[0])
        low = 0
        high = m * n - 1

        while low <= high:
            mid = low + (high-low)//2; #to prevent integer overflow
            row = mid // n
            col = mid % n
            if target == matrix[row][col]:
                return True
            elif target > matrix[row][col]:
                low = mid + 1
            else:
                high = mid - 1
        return False

## Problem2 
## Search in a Rotated Sorted Array (https://leetcode.com/problems/search-in-rotated-sorted-array/)
## TC = O(log n), SC = O(1)

class Solution:
    def search(self, nums: List[int], target: int) -> int:
        if nums == None or len(nums) == 0:
            return -1
        
        n = len(nums)
        low = 0
        high = n - 1

        while low <= high:
            mid = low + (high - low) // 2
            if nums[mid] == target:
                return mid
            if nums[low] <= nums[mid]:
                if target >= nums[low] and target < nums[mid]:
                    high = mid - 1
                else:
                    low = mid + 1
            else:
                if target > nums[mid] and target <= nums[high]:
                    low = mid + 1
                else:
                    high = mid - 1
        
        return -1



## Problem3
## Search in Infinite sorted array: (https://leetcode.com/problems/search-in-a-sorted-array-of-unknown-size/)
## TC = O(log n), SC = O(1)
class Solution:
    def search(self, reader: 'ArrayReader', target: int) -> int:
        low = 0
        high = 1

        while target > reader.get(high):
            low = high
            high = 2 * high

        return self.binarySearch(reader, target, low, high)

    def binarySearch(self, reader: 'ArrayReader', target: int, low: int, high: int) -> int:
        while low <= high:
            mid = low + (high - low) // 2
            value = reader.get(mid)
            if value == target:
                return mid
            elif target > value:
                low = mid + 1
            else:
                high = mid - 1
        return -1  


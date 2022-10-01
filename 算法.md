

LeetCode算法



# Day01二分查找

## 704.二分查找

https://leetcode.cn/problems/binary-search/


```java
class Solution {
    public int search(int[] nums, int target) {
        int left = 0;
        int right = nums.length - 1;
        while(left <= right){
            int mid = left + (right - left) / 2;
            if(target == nums[mid]){
                return mid;
            }else if(target < nums[mid]){
                right = mid - 1;
            }else{
                left = mid + 1;
            }
        }
        return -1;
    }
}
```

```java
class Solution {
    public int search(int[] nums, int target) {
        int left = 0;
        int right = nums.length;
        while(left < right){
            int mid = left + (right - left) / 2;
            if(target == nums[mid]){
                return mid;
            }else if(nums[mid] < target){
                left = mid + 1;
            }else{
                right = mid;
            }
        }

        return -1;
    }
}
```

两种解法，注意区间。



## 278.第一个错误的版本

https://leetcode.cn/problems/first-bad-version/


```java
public class Solution extends VersionControl {
    public int firstBadVersion(int n) {
        int left = 0;
        int right = n;
        while(left < right){
            int mid = left + (right - left) / 2;
            if(isBadVersion(mid) == false){
                left = mid + 1;
            }else{
                right = mid;
            }
        }

        return left; //其实这里写left 、right 都可以
    }
}
```













## 35.搜索插入位置

https://leetcode.cn/problems/search-insert-position/


```java
class Solution {
    public int searchInsert(int[] nums, int target) {
        int left = 0;
        int right = nums.length - 1;
        while(left <= right){
            int mid = left + (right - left) / 2;
            if(target == nums[mid]){
                return mid;
            }else if(nums[mid] < target){
                left = mid + 1;
            }else{
                right = mid - 1;
            }
        }
        // 分别处理如下四种情况
        // 目标值在数组所有元素之前  [0, -1]
        // 目标值等于数组中某一个元素  return middle;
        // 目标值插入数组中的位置 [left, right]，return  right + 1
        // 目标值在数组所有元素之后的情况 [left, right]，这是右闭区间，所以  return right + 1
        return right + 1;
    }
}
```





# Day02双指针

## 977.有序数组的平方

https://leetcode.cn/problems/squares-of-a-sorted-array/



```java
class Solution {
    public int[] sortedSquares(int[] nums) {
        int l = 0;
        int r = nums.length - 1;
        int[] res = new int[nums.length];
        int j = nums.length - 1;
        while(l <= r){
            if(nums[l] * nums[l] > nums[r] * nums[r]){
                res[j--] = nums[l] * nums[l++];
            }else{
                res[j--] = nums[r] * nums[r--];
            }
        }
        return res;
    }
}
```





## 189.轮转数组

https://leetcode.cn/problems/rotate-array/


```java
class Solution {
    public void rotate(int[] nums, int k) {
        if(nums.length < 2){
            return;
        }
        k = k % nums.length;

        reverse(nums, 0, nums.length - 1);
        reverse(nums, 0, k - 1);
        reverse(nums, k, nums.length - 1);

    }


    public void reverse(int[] nums, int begin, int end){
        int temp;
        while(begin < end){
            temp = nums[begin];
            nums[begin] = nums[end];
            nums[end] = temp;
            begin++;
            end--;
        }
    }
}
```


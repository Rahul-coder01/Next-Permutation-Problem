# Next-Permutation-Problem

Implement next permutation, which rearranges numbers into the lexicographically next greater permutation of numbers.

If such an arrangement is not possible, it must rearrange it as the lowest possible order (i.e., sorted in ascending order).

The replacement must be in place and use only constant extra memory.

 

Example 1:

Input: nums = [1,2,3]
Output: [1,3,2]
Example 2:

Input: nums = [3,2,1]
Output: [1,2,3]
Example 3:

Input: nums = [1,1,5]
Output: [1,5,1]
Example 4:

Input: nums = [1]
Output: [1]
 

Constraints:

1 <= nums.length <= 100
0 <= nums[i] <= 100

Code Solution: (In Java)

class Solution {
    public void nextPermutation(int[] nums) {
        // Length of the array
        int n = nums.length;
        // Index of the first element that is smaller than
        // the element to its right.
        int index = -1;
        // Loop from right to left
        for (int i = n - 1; i > 0; i--) {
            if (nums[i] > nums[i - 1]) {
                index = i - 1;
                break;
            }
        }
        // Base condition
        if (index == -1) {
            reverse(nums, 0, n - 1);
            return;
        }
        int j = n - 1;
        // Again swap from right to left to find first element
        // that is greater than the above find element
        for (int i = n - 1; i >= index + 1; i--) {
            if (nums[i] > nums[index]) {
                j = i;
                break;
            }
        }
        // Swap the elements
        swap(nums, index, j);
        // Reverse the elements from index + 1 to the nums.length
        reverse(nums, index + 1, n - 1);
    }

    private static void reverse(int[] nums, int i, int j) {
        while (i < j) {
            swap(nums, i, j);
            i++;
            j--;
        }
    }

    private static void swap(int[] nums, int i, int index) {
        int temp = nums[index];
        nums[index] = nums[i];
        nums[i] = temp;
        
    }
}

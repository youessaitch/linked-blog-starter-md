### 1. Sorting Algorithms
- <!--⚠️Imgur upload failed, check dev console-->
![[Pasted image 20240725101025.png

#### 1. Merge Sort
- Divide and conquer
- Keep dividing in half then sort and merge
- ![[Pasted image 20240725101537.png]]
- Then use 2-pointer to get the final sorted array
	- ![[Pasted image 20240725103042.png]]
- ```cpp
	class Solution {
public:
    int n;
    
    void merge(vector<int>& nums, int l, int mid, int r) {
        // Divide into two
        int n1 = mid - l + 1;
        int n2 = r - mid;

        vector<int> a(n1); // Two arrays to store the left and right array
        vector<int> b(n2);

        for (int i = 0; i < n1; i++) a[i] = nums[l + i];
        for (int i = 0; i < n2; i++) b[i] = nums[mid + 1 + i];

        int i = 0, j = 0, k = l; // k->traverse main array nums
        while (i < n1 && j < n2) {
            if (a[i] < b[j]) {
                nums[k] = a[i];
                i++;
            } else {
                nums[k] = b[j];
                j++;
            }
            k++;
        }

        while (i < n1) {
            nums[k] = a[i];
            i++;
            k++;
        }

        while (j < n2) {
            nums[k] = b[j];
            j++;
            k++;
        }
    }

    // Divide and conquer
    void mergeSort(vector<int>& nums, int l, int r) {
        if (l < r) {
            int mid = l + (r - l) / 2; // Prevent overflow
            mergeSort(nums, l, mid);
            mergeSort(nums, mid + 1, r);
            merge(nums, l, mid, r);
        }
    }

    vector<int> sortArray(vector<int>& nums) {
        n = nums.size();
        mergeSort(nums, 0, n - 1);
        return nums;
    }
};


- TC : O(nlogn) {Best,worst,average All nlogn}
- SC : O(n)
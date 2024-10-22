# 1. Merge Sort
- ![](https://i.imgur.com/GhGYsak.jpeg)
- In merge part : Jo v chota ho L[i], R[j] me usko daldo array me using pointer k
- ```cpp
	class Solution
{
    public:
    void merge(int arr[], int l, int m, int r) {
        int n1 = m - l + 1;
        int n2 = r - m;

        // Create temporary arrays to store the two halves
        int L[n1], R[n2];

        int k = l;
        // Copy data to temporary arrays L[] and R[]
        for (int i = 0; i < n1; i++)
            L[i] = arr[k++];
        for (int j = 0; j < n2; j++)
            R[j] = arr[k++];

        // Merge the temporary arrays back into arr[l..r]
        int i = 0; // Initial index of first subarray
        int j = 0; // Initial index of second subarray
        k = l; // Initial index of merged subarray

        while (i < n1 && j < n2) {
            if (L[i] <= R[j]) {
                arr[k] = L[i];
                i++;
            } else {
                arr[k] = R[j];
                j++;
            }
            k++;
        }

        // Copy the remaining elements of L[], if there are any
        while (i < n1) {
            arr[k] = L[i];
            i++;
            k++;
        }

        // Copy the remaining elements of R[], if there are any
        while (j < n2) {
            arr[k] = R[j];
            j++;
            k++;
        }
    }
    
    public:
    void mergeSort(int arr[], int l, int r) {
        
        if(l >= r) {
            return;
        }
        
        int mid = l + (r-l)/2;
        
        mergeSort(arr, l, mid);
        mergeSort(arr, mid+1, r);
        
        merge(arr, l, mid ,r);
        
    }
};

## Questions on Merge Sort:
1. [493. Reverse Pairs](https://leetcode.com/problems/reverse-pairs/) 
- ```cpp
	class Solution {
public:
    int cnt = 0;  //cnt of pairs

    void merge(vector<int> &arr, int l, int m, int r) {
        int n1 = m - l + 1;
        int n2 = r - m;
        vector<int> L(n1), R(n2);
        for (int i = 0; i < n1; i++) L[i] = arr[l + i];
        for (int j = 0; j < n2; j++) R[j] = arr[m + 1 + j];
        int i = 0, j = 0, k = l;
        while (i < n1 && j < n2) {
            if (L[i] <= R[j]) {
                arr[k] = L[i];
                i++;
            } else {
                arr[k] = R[j];
                j++;
            }
            k++;
        }
        while (i < n1) {
            arr[k] = L[i];
            i++;
            k++;
        }
        while (j < n2) {
            arr[k] = R[j];
            j++;
            k++;
        }
    }
    
	//****MAIN PART OF THE CODE****
    // Function to count reverse pairs in the array
    void countPairs(vector<int> &nums, int l, int mid, int r) {
        int j = mid + 1; //checking in the R array
        for (int i = l; i <= mid; i++) {
            while (j <= r && nums[i] > 2LL * nums[j]) {
                j++;
            }
            cnt += (j - (mid + 1));  // Increment the global count
        }
    }

    // Merge sort function
    void mergeSort(vector<int> &arr, int l, int r) {
        if (l >= r) {
            return;
        }

        int mid = l + (r - l) / 2;

        // Sort both halves
        mergeSort(arr, l, mid);
        mergeSort(arr, mid + 1, r);
        
		//****MERGE KRNE SE PEHLE CNT KRLO KI REQUIRED PAIR MIL RHE YA NHI***
        // Count reverse pairs
        countPairs(arr, l, mid, r);

        // Merge the two sorted halves
        merge(arr, l, mid, r);
    }

    // Main function to return the number of reverse pairs
    int reversePairs(vector<int>& nums) {
        int n = nums.size();
        mergeSort(nums, 0, n - 1);
        return cnt;
    }
};

TC - 2 4 3 5 1
L = 2 3 4
R = 1 5

2. https://www.naukri.com/code360/problems/count-inversions_615?leftPanelTabValue=PROBLEM 
- Same to same code except while(j<=r && arr[i]>arr[j]) j++;


# KMP Algorithm
- USED FOR PATTERN MATCHING IN STRINGS in O(n+m) time
- Prepare a temporary array, called LPS (longest proper prefix which is also a suffix)
- ```cpp
	class Solution
{
    public:
        // Function to compute the LPS (Longest Proper Prefix which is also Suffix) array
        void computeLPS(string pattern, vector<int>& lps) {
            int M = pattern.length();
            int len = 0; // Length of the previous longest prefix & suffix
        
            lps[0] = 0; // Because there is no proper suffix and prefix of pattern[0..0]
        
            int i = 1;
            while (i < M) {
                if (pattern[i] == pattern[len]) {
                    len++;
                    lps[i] = len;
                    i++;
                } else {
                    if (len != 0) {
                        len = lps[len - 1]; //You can also write, len = len-1;
                    } else {
                        lps[i] = 0;
                        i++;
                    }
                }
            }
        }
        
        vector <int> search(string pat, string txt) {
            int N = txt.length();
            int M = pat.length();
            vector<int> result;
            
            // Create an LPS array to store the longest proper prefix which is also a suffix
            //lps[i] = the longest proper prefix of pat[0..i] which is also a suffix of pat[0..i]. 
            vector<int> lps(M, 0);
            computeLPS(pat, lps);
        
            int i = 0; // Index for text
            int j = 0; // Index for pattern
        
            while (i < N) {
                if (pat[j] == txt[i]) {
                    i++;
                    j++;
                }
        
                if (j == M) {
                    result.push_back(i-j+1); //Pattern found at index i-j+1 (If you have to return 1 Based indexing, that's why added + 1)
                    j = lps[j - 1];
                } else if (i < N && pat[j] != txt[i]) {
                    if (j != 0) {
                        j = lps[j - 1];
                    } else {
                        i++;
                    }
                }
            }
            
            return result;
        }
     };



# Line Sweep Algorithm
- Used in interval based problems
- Example: [2406. Divide Intervals Into Minimum Number of Groups](https://leetcode.com/problems/divide-intervals-into-minimum-number-of-groups/)
- A video on this: https://www.youtube.com/watch?v=YnIxejYW7cE
- Explanation:
	- ![](https://i.imgur.com/BUqo8YC.jpeg)

- Code:
	- ```cpp
		class Solution {
		public:
		    // Line Sweep Algorithm
		    // No of groups required == Maximum number of overlapping intervals
		    int minGroups(vector<vector<int>>& intervals) {
		        int n = intervals.size();
		
		        vector<pair<int, int>> v;
		
		        // Create events
		        for (auto it : intervals) {
		            v.push_back({it[0], 1});       // start time: +1
		            v.push_back({it[1] + 1, -1});  // end time: -1 (after the end of the interval)
		        }
		
		        // Sort the events by time, and if times are equal, the end event (-1) should come before the start event (+1)
		        sort(v.begin(), v.end());
		
		        int cnt = 0;  // count of current overlapping intervals
		        int maxi = 0; // maximum number of overlapping intervals
		
		        // Sweep through the events
		        for (auto it : v) {
		            cnt += it.second;  // increment or decrement based on event type
		            maxi = max(maxi, cnt);  // update the maximum number of overlaps
		        }
		
		        return maxi;
		    }
		};


# Check if intervals are overlapping
- Given two points (a1,b1), (a2,b2), if
	- ### ==max(a1,a2) < min(b1,b2)==
- Then its overlapping
- Overlapped Interval:
	- ### {max(a1,a2), min(b1,b2)}

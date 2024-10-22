1. https://leetcode.com/discuss/interview-question/5619722/Amazon-or-Online-Assessment-or-2024
	- ```cpp
		#include <bits/stdc++.h>
		using namespace std;
		
		int getMaxConsecutiveON(string &s, int k) {
		    int n = s.size();
		    int sol = 0;      // Variable to store the maximum length of consecutive 1s
		    int currK = 0;    // Counter for the number of 0s flipped
		    int i = 0;        // Start index of the sliding window
		
		    // Iterate with j as the end index of the sliding window
		    for (int j = 0; j < n; j++) {
		        // If the current character is '0', increase the count of flipped 0s
		        if (s[j] == '0') {
		            currK++;
		        }
		
		        // If the number of flipped 0s exceeds k, shrink the window from the left
		        while (currK > k)
				{
					if (s[i++] == '0'){
					while (i < n && s[i] == '0'){
						i++;
					}
					currK--;
					}
				}
		
		        // Update the maximum length of consecutive 1s
		        sol = max(sol, j - i + 1);
		    }
		
		    return sol;
		}
		
		int main() {
		    int t;
		    cin >> t;
		    while (t--) {
		        string s;
		        int k;
		        cin >> s >> k;
		        int ans = getMaxConsecutiveON(s, k);
		        cout << ans << endl;
		    }
		
		    return 0;
		}

2. 
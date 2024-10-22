- #### Divisors
	- Divisors come in pair, for example -> 36 ka divisor {2,18}, {3, 12} aisa. So to find all divisors just go till sqrt(n) from j = 1, and if(num%j == 0) store j and num/j as divisors. Make sure if j == num/j then it has only one divisor so dont store twice
	- ```cpp
		for (int i = 0; i < n; i++) {
	    int num = nums[i];
	    for (int j = 1; j * j <= num; j++) {
	        // Divisors come in pairs, so only go up to sqrt(num), i.e., j * j <= num
	        if (num % j == 0) {
	            int div1 = j;
	            int div2 = num / j;
	
	            cntDivisors[div1]++;
	            if (div1 != div2) {
	                cntDivisors[div2]++;
	            }
	        }
	    }
	}

- #### LIS Using Binary Search
	- ```cpp
		vector<int> res;
		int currW = envelopes[0][0];
		int currH = envelopes[0][1];
		res.push_back(currH);
		
		for (int i = 1; i < n; i++) {
		    if (envelopes[i][1] > res[res.size() - 1]) {
		        res.push_back(envelopes[i][1]);
		    } else {
		        // Find index of the first element that is >= envelopes[i][1]
		        //Find index of just bada element in res
		        auto idx = lower_bound(res.begin(), res.end(), envelopes[i][1]) - res.begin();
		        res[idx] = envelopes[i][1];
		    }
		}

	- If the element is greater than the last then put it in ans vector since its still increasing, if not then find the index which is just greater than equal to the required one in ans vector ans replace it there, this way scope of increasing sequence increases;
	- Refer to this problem test cases for more info : [354. Russian Doll Envelopes](https://leetcode.com/problems/russian-doll-envelopes/)
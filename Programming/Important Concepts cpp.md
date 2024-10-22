- stringstream st(s) -> trims the string
	- ![](https://i.imgur.com/iSYlczF.png)
- a&(1<<i) gives a power of 2 so use bool to find if set or not

### More on Stringstream:
- ![](https://i.imgur.com/yTkivfB.png)
	- ```cpp
			bool isValid(string str){
		        for(auto it: str){
		            if(!isdigit(it) || it=='9') return false;
		        }
		        return true;
		    }
		  
		    long long ExtractNumber(string sentence) {
		
		        // code here
		        stringstream ss(sentence);
		        string word;
		        long long ans = -1;
		        
		        while(ss >> word){
		            if(isValid(word)){
		                long long num = stol(word);
		                ans = (long long)max(ans,num);
		            }
		        }
		        return ans;
		    }
			```
- Explaination:
	- **Logic**:
	- Create a `stringstream` object `ss` initialized with the input `sentence`. A `stringstream` allows you to treat a string like a stream, similar to reading from standard input.
	- Declare a `string` variable `word` to hold each word extracted from the stream.
	- Initialize `ans` to `-1` to keep track of the largest valid number found.
	- ![](https://i.imgur.com/30w3Zeo.png)

1. OS - semaphore mutex deadlock scheduling raid virtual memory cache
2. Merge 3 sorted arrays
3. Inorder iterator for a binary tree 🌲 🌲 🌲 
4. Vertical sum in a given binary tree
5. Asteroid collision 
6. Clone a linked list with random pointers
7. Median of the data stream
8. Implement heal data structure
9. Swap code without using temporary variables
10. Project : difficulty and how to face the difficulty 
11. ==Sorting algorithms==
12. Stacks, trees 
13. ==Amazon leadership principles are crucial==
14. Explain complexity for most optimized solution
15. ==Discuss tc and sc beforehand==
16. Prepare insightful questions
17. BST, BFS
18. ==Create BST from string==
19. 2 sum in BST
20. Rotten oranges
21. Print all anagrams of a given string 
22. Two sum (sorted and unsorted array)
23. Three sum 
24. Blind 75
25. ==How hashing is done==
26. Wildcard matching
27. Normalisation in dbms
28. Binary search, find k closest elements given value

## prepare questions for them
1. In which team are you working and how is your experience regarding work-life balance and how is 6-month intern different from 2 month intern.


if(str[i]!='(' && str[i]!=')'){
                string s="";
                while(str[i]>='0' && str[i]<='9'){
                    s+=str[i];
                    i++;
                }
                int num = stoi(s);
                st.push(new Node(num));
            }else if(str[i] == '('){
                if(p1->left == nullptr) l = true;
                else l = false;
                
                if(!st.empty()){
                    if(l){
                        p1->left = st.top();
                        p1 = p1->left;
                        st.pop();
                    }else{
                        p1->right = st.top();
                        p1 = p1->right;
                        st.pop();
                    }
                }
            }else if(str[i]==')'){
               if(!st.empty()){
                    if(l){
                        p1->left = st.top();
                        p1 = p1->left;
                        st.pop();
                    }else{
                        p1->right = st.top();
                        p1 = p1->right;
                        st.pop();
                    }
                }
                
                
            }
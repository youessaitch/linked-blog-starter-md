1. Burn a Tree ( Use of node and its parent, use map) -> very easy method but important to remember
	- ```cpp
		/**
		 * Definition for binary tree
		 * struct TreeNode {
		 *     int val;
		 *     TreeNode *left;
		 *     TreeNode *right;
		 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
		 * };
		 */
		int Solution::solve(TreeNode* A, int B) {
		    // Map to store the parent of each node
		    map<TreeNode*, TreeNode*> par;
		    queue<TreeNode*> q;
		    TreeNode* src = A; // The target node
		    q.push(A);
		    
		    // BFS to find the target node and create the parent mapping
		    while (!q.empty()) {
		        auto node = q.front();
		        q.pop();
		        
		        if (node->val == B) {
		            src = node;
		        }
		        
		        if (node->left) {
		            q.push(node->left);
		            par[node->left] = node;
		        }
		        
		        if (node->right) {
		            q.push(node->right);
		            par[node->right] = node;
		        }
		    }
		    
		    int t = 0;
		    queue<TreeNode*> q1;
		    map<TreeNode*, int> vis; // Map to track visited nodes
		    q1.push(src);
		    
		    // BFS to calculate the time taken
		    while (!q1.empty()) {
		        int size = q1.size();
		        bool ch = false;
		        
		        while (size--) {
		            auto node = q1.front();
		            q1.pop();
		            
		            if (node->left && !vis[node->left]) {
		                vis[node->left] = 1;
		                q1.push(node->left);
		                ch = true;
		            }
		            
		            if (node->right && !vis[node->right]) {
		                vis[node->right] = 1;
		                q1.push(node->right);
		                ch = true;
		            }
		            
		            if (par.find(node) != par.end() && !vis[par[node]]) {
		                vis[par[node]] = 1;
		                q1.push(par[node]);
		                ch = true;
		            }
		        }
		        
		        if (ch) {
		            t++;
		        }
		    }
		    
		    return t;
		}

2. 
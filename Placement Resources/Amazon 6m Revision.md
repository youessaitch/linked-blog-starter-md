1. Reverse a Linked List in Groups
- ```cpp
	struct node *reverseIt(struct node *head, int k) {
        // Complete this method
        node* prev = NULL;
        node* curr = head;
        node* p1;
        int cnt = 0;
        
        while(curr!=NULL && cnt<k){
            p1 = curr->next;
            curr->next = prev;
            prev = curr;
            curr = p1;
            cnt++;
        }
        
        if(p1!=NULL){
            head->next = reverseIt(p1,k);
        }
        return prev;
    }

2. Tree and Subtree Same
- ```cpp
	class Solution {
	public:
	    bool solve(TreeNode* a, TreeNode* b) {
	        if (a == nullptr && b == nullptr) return true;
	        if (a == nullptr || b == nullptr) return false;
	
	        if (a->val != b->val) return false;
	
	        return solve(a->left, b->left) && solve(a->right, b->right);
	    }
	
	    bool isSubtree(TreeNode* root, TreeNode* subRoot) {
	        if (!subRoot) return true;
	        if (!root) return false;
	
	        if (solve(root, subRoot)) return true;
	
	        return isSubtree(root->left, subRoot) || isSubtree(root->right, subRoot);
	    }
	};


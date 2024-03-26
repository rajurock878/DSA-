
Q1.Level Order Traversal
class Solution
{
    public:
    //Function to return the level order traversal of a tree.
    vector<int> levelOrder(Node* root)
    {
      //Your code here
      queue<Node*>q;
      q.push(root);
      vector<int>ans;
      Node*temp;
      while(!q.empty())
      {
          temp= q.front();
          q.pop();
          
          ans.push_back(temp->data);
          //left
          if(temp->left)
          q.push(temp->left);
          //right
          if(temp->right)
          q.push(temp->right);
          
      }
      
      return ans;
    }
};

Q2.size of binary tree
class Solution {
  public:
  void Total(Node*root,int &count)
  {
      if(root==NULL)
      return ;
      
      count++;
      Total(root->left,count);
      Total(root->right,count);
      
  }
    int getSize(Node* root) {
        
        // code here
        int count=0;
        Total(root,count);
        return count;
    }
};
#second method 
class Solution {
  public:
    int getSize(Node* root) {
        // code here
        if(!root)
        return 0;
        
        return (1+getSize(root->left)+getSize(root->right));
    }
};
# Q3.sum of binary tree
first method
void Total(Node*root,long int &sum)
{
    if(root==NULL)
    return;
    
    sum+=root->key;
    Total(root->left,sum);
    Total(root->right,sum);
}
long int sumBT(Node* root)
{
    // Code here
    long int sum=0;
    Total(root,sum);
    return sum;
    
}
#second method
long int sumBT(Node* root)
{
    // Base case: If the tree is empty, return 0
    if (!root)
        return 0;

    // Recursively compute the sum of nodes in the left and right subtrees
    long int leftSum = sumBT(root->left);
    long int rightSum = sumBT(root->right);

    // Return the sum of the current node's key and the sums of its left and right subtrees
    return root->key + leftSum + rightSum;
}
#Q4 COUNT Leaves in binary tree
void countleaf(Node*root,int&count)
 {
     if(!root)
     return;
     
     if(!root->left && !root->right)
     {
         count++;
         return ;
         
     }
     countleaf(root->left,count);
     countleaf(root->right,count);
 }
int countLeaves(Node* root)
{
  // Your code here
  int count=0;
  countleaf(root,count);
  return count;
}
#second method
int countLeaves(Node* root)
{
  // Your code here
  if(!root)
  return 0;
  if(!root->left && !root->right)
  return 1;
  
  //non leaf
  return (countLeaves(root->leaf)+countLeaves(root->right));
}
#Q5.COUNT nonleaf Nodes
class Solution {
public:
    int countNonLeafNodes(Node* root) {
        if (!root || (!root->left && !root->right))
            return 0;

        return 1 + countNonLeafNodes(root->left) + countNonLeafNodes(root->right);
    }
};
#Q6.height of binary tree
class Solution{
    public:
    //Function to find the height of a binary tree.
    int height(struct Node* root){
        // code here 
        if(root==NULL)
        return 0;
        return 1+max(height(root->left),height(root->right));
    }
};
#Q7.largest value of each level
#include <vector>
#include <queue>
#include <climits> // for INT_MIN
#include <algorithm> // for std::max

using namespace std;

// Definition for a binary tree node.
struct Node {
    int data;
    Node *left;
    Node *right;
    Node(int val) : data(val), left(nullptr), right(nullptr) {}
};

class Solution {
public:
    vector<int> largestValues(Node* root) {
        vector<int> res;
        if (!root) 
            return res;
        queue<Node*> q;
        q.push(root);
        while (!q.empty()) {
            int n = q.size();
            int maxVal = INT_MIN;
            for (int i = 0; i < n; i++) {
                Node* node = q.front();
                q.pop();
                maxVal = max(maxVal, node->data);
                if (node->left) 
                    q.push(node->left);
                if (node->right) 
                    q.push(node->right);
            }
            res.push_back(maxVal);
        }
        return res;
    }
};

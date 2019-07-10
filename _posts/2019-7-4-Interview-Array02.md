---
layout: post
title:  "Leetcode Arrays 02"
categories: Interview
---
## 581. Shortest Unsorted Continuous Subarray
First solution is just sort, O(nlogn)
```
public:
    // longest increasing sequence
    int findUnsortedSubarray(vector<int>& nums) {
        vector<int> tmp(nums);
        sort(tmp.begin(),tmp.end());
        int cnt = 0 ;
        int n = nums.size();
        int left = -1;
        int right = -1;
        for(int i=0;i<n;i++){
            if(nums[i] != tmp[i]){
                left = i;
                break;
            }
            
        }
        for(int i=n-1;i>=0;i--){
            if(nums[i] != tmp[i]){
                right = i;
                break;
            }
        }
        if(left == -1 or right == -1){
            return 0l;
        }
        return right-left+1;
    }
};
```

Stack Solution, kind of tricky.
```
class Solution {
public:
    int findUnsortedSubarray(vector<int>& nums) {
        stack<int> myStack;
        int l=nums.size(),r=0;
        for(int i=0 ; i<nums.size() ; i ++){
            while(!myStack.empty() && nums[myStack.top()] > nums[i]){
                l = min(myStack.top(),l);
                myStack.pop();
            }
            myStack.push(i);
        }
        stack<int> tmp;
        swap(tmp,myStack);
        for(int j=nums.size()-1;j>=0;j--){
            while(!myStack.empty() && nums[j] > nums[myStack.top()]){
                r = max(r,myStack.top());
                myStack.pop();
            }
            myStack.push(j);
        }
        return max(r-l+1, 0);
    }
};
```
<hr>
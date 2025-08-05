# [3477. Fruits Into Baskets II](https://leetcode.com/problems/fruits-into-baskets-ii/)

### Description

> You are given two arrays of integers, `fruits` and `baskets`, each of length `n`, where `fruits[i]` represents the **quantity** of the `ith` type of fruit, and `baskets[j]` represents the **capacity** of the `jth` basket.
>
> From left to right, place the fruits according to these rules:
>
> - Each fruit type must be placed in the **leftmost available basket** with a capacity **greater than or equal** to the quantity of that fruit type.
> - Each basket can hold **only one** type of fruit.
> - If a fruit type **cannot be placed** in any basket, it remains **unplaced**.
>
> Return the number of fruit types that remain unplaced after all possible allocations are made.



### Code

```c++
/* O(n^2) , faster but need to modify baskets */
class Solution {
    public:
        int numOfUnplacedFruits(vector<int>& fruits, vector<int>& baskets){
            const int size = baskets.size();
            int ans = size;
            for(int i=0;i<size;i++){
                for(int j=0;j<size;j++){
                    if(fruits[i]<=baskets[j]){
                        ans--;
                        baskets[j]=0;
                        break;
                    }
                }
            }
            return ans;
        }
};
```



### Possible Optimization

> Use Segment tree. 

  






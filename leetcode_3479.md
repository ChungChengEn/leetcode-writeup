# [3479. Fruits Into Baskets III](https://leetcode.com/problems/fruits-into-baskets-iii/)

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

### Constraints

> - `n == fruits.length == baskets.length`
> - `1 <= n <= 10^5`
> - `1 <= fruits[i], baskets[i] <= 10^9`
>
> The data is much larger than that of leetcode 3477, so I have to do the optimization using Segment Tree; otherwise I will get an TLE.



### Code

```c++
class Solution {
public:
    int n;
    vector<int> seg;

    void Update(int p){
        seg[p] = max(seg[p << 1], seg[p << 1|1]);
    }

    void Build(int p, int l, int r, vector<int>& baskets){
        if(l==r){
            seg[p]=baskets[l];
            return;
        }
        int mid = (l + r) >> 1;
        Build(p << 1, l, mid, baskets);
        Build(p << 1 | 1, mid+1, r, baskets);
        Update(p);
    }

    void Assign(int pos, int val, int p, int l, int r){
        if(pos < l || pos > r)  return;
        if(l==r){
            seg[p] = val;
            return;
        }
        int mid = (l + r) >> 1;
        Assign(pos, val, p<<1, l, mid);
        Assign(pos, val, p<<1|1, mid+1, r);
        Update(p);
    }

    int FirstQualify(int val, int p, int l, int r){
        if(seg[p] < val)    return r+1;
        if(l==r)    return l;
        int mid = (l + r) >> 1;
        int ind = FirstQualify(val, p<<1, l, mid);
        if(ind<=mid)    return ind;
        return FirstQualify(val, p<<1|1, mid+1,r);
    }

    int numOfUnplacedFruits(vector<int>& fruits, vector<int>& baskets) {
        // Need to learn segment tree
        n = baskets.size();
        seg.assign(4*n+1, 0);
        Build(1,0,n-1,baskets);
        int res = 0;
        for(int fruit:fruits){
            int pos = FirstQualify(fruit,1,0,n-1);
            if(pos==n)  res++;
            else    Assign(pos,0,1,0,n-1);
        }
        return res;
    }
};
```


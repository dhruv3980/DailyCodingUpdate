# 🚀 Day 9 – Greedy Algorithm Problems (C++)

## This document contains solutions to several Greedy Algorithm problems implemented in C++.

📌 Problems Covered

**Activity Selection Problem**

**Fractional Knapsack Problem**

**Minimum Coin Change**

**Job Sequencing Problem**

**Maximum Length Chain of Pairs**

**Minimum Absolute Difference of Two Arrays**

**Sorting Pairs with Custom Comparator**

---

## 1️⃣ Activity Selection Problem

**Select the maximum number of activities that don’t overlap.**
```
#include<iostream>
#include<vector>
using namespace std;

int maxActivitySelect(vector<int>&start, vector<int>&end){
    int ans = 1;
    int endtime = end[0];
    cout<<"Activity A0 select"<<endl;

    for(int i =0; i<start.size(); i++){
        if(start[i]>=endtime){
            endtime = end[i];
            cout<<"Activity A"<<i<<" Select"<<endl;
            ans++;
        }
    }
    return ans;
}

int main(){
    vector<int>start = {1,3,0,5,8,5};
    vector<int>end = {2,4,6,7,9,9};
    cout<<maxActivitySelect(start,end);
}
```
 # 2️⃣ Fractional Knapsack Problem

**Maximize the total value that fits into the bag.**
```
#include<iostream>
#include<vector>
#include<algorithm>
using namespace std;

bool compare(pair<double, int>p1, pair<double, int>p2){
    return p1.first>p2.first;
}

int getFractionalKnapsack(vector<int> &value, vector<int>&weight , int W){
    vector<pair<double, int>> ratio;

    for(int i =0; i<value.size(); i++){
        double r = value[i]/(double)weight[i];
        ratio.push_back(make_pair(r, i));
    }

    sort(ratio.begin(), ratio.end(), compare);

    int ans =0;

    for(int i =0; i<value.size(); i++){
        int w = weight[i];
        if(w<W){
            ans+=value[i];
            W-=w;
        }
        else{
            ans+=(int)ratio[i].first*W;
            break;
        }
    }

    cout<<"total item value is "<<ans<<endl;
    return ans;
}

int main(){
    vector<int> value = {60,100,120};
    vector<int> weight = {10,20,30};
    int W = 50;
    cout<<getFractionalKnapsack(value, weight, W);
}


```
---
## 3️⃣ Minimum Coin Change

**Find the minimum number of coins required to make a given value.**
```

#include<iostream>
#include<vector>
using namespace std;

int getminchange(vector<int>&coins, int V){
    int ans=0;
    for(int i = coins.size()-1; i>=0 && V>0 ; i--){
        if(coins[i]<=V){
            ans+=V/coins[i];
            V=V%coins[i];
        }
    }
    cout<<"min coin that can we used to make the val  "<<ans;
    return ans;
}

int main(){
    vector<int> coins{1,2,5,10,20,50,100,500,2000};
    int V = 590;
    getminchange(coins,V);
}
```
---

## 4️⃣ Job Sequencing Problem

**Schedule jobs to maximize profit.**
```
#include<iostream>
#include<vector>
#include<algorithm>
using namespace std;

class job{
    public:
    int idx;
    int profit;
    int deadline;
    job(int idx, int profit, int deadline){
        this->idx =idx;
        this->deadline=deadline;
        this->profit=profit;
    }
};

int maxProfit(vector<pair<int,  int>> & pairs){
    vector<job>Jobs;
    for(int i=0; i<pairs.size(); i++){
        Jobs.emplace_back(i, pairs[i].second, pairs[i].first);
    }

    sort(Jobs.begin(), Jobs.end(), [](job &a , job &b){
        return a.profit > b.profit;
    });

    int Profit =Jobs[0].profit;
    int jobdeadline = Jobs[0].deadline;
    
    for(int i=1; i<Jobs.size(); i++){
        if(Jobs[i].deadline>jobdeadline){
            jobdeadline++;
            Profit+=Jobs[i].profit;
        }
    }

    cout<<"max profit from jobs "<<Profit<<endl;
    return Profit;
};

int main(){
    vector<pair<int, int>> jobs;
    jobs.push_back(make_pair(1,20));
    jobs.push_back(make_pair(1,10));
    jobs.push_back(make_pair(4,40));
    jobs.push_back(make_pair(1,30));
    maxProfit(jobs);
}
```
---

## 5️⃣ Maximum Length Chain of Pairs

**Form the longest chain where one pair’s second element is smaller than the next pair’s first element.**

```
#include<iostream>
#include<vector>
#include<algorithm>
using namespace std;

bool compare(pair<int, int>p1, pair<int, int>p2){
    return p1.second<p2.second;
}

int maxchainlength(vector<pair<int, int>>pairs){
    sort(pairs.begin(), pairs.end(), compare);

    int ans =1;
    int endTime = pairs[0].second;
    for(int i=1; i<pairs.size(); i++){
        if(pairs[i].first>=endTime){
            ans++;
            endTime=pairs[i].second;
        }
    }
    cout<<"max-chain-length "<<ans;
    return ans;
}

int main(){
    int n=5;
    vector<pair<int, int>>pairs(n);
    pairs[0] = make_pair(5,24);
    pairs[1] = make_pair(39,60);
    pairs[2] = make_pair(5,28);
    pairs[3] = make_pair(27,40);
    pairs[4] = make_pair(50,90);
    maxchainlength(pairs);
}
```
---

## 6️⃣ Minimum Absolute Difference of Two Arrays
```
#include<iostream>
#include<vector>
#include<algorithm>
using namespace std;

int main(){
    vector<int>p1 = {4,1,8,7};
    vector<int>p2={2,3,6,5};

    sort(p1.begin(), p1.end());
    sort(p2.begin(), p2.end());

    int ans =0;
    for(int i=0; i<p1.size(); i++){
        ans+=abs(p1[i]-p2[i]);
    }

    cout<<"min abs difference "<<ans;
}

```
---
## 7️⃣ Sorting Pairs with Custom Comparator
```
#include<iostream>
#include<vector>
#include<algorithm>
using namespace std;

bool compare(pair<int, int>p1, pair<int, int>p2){
    return p1.second<p2.second;
}

int main(){
    vector<int>p1 = {1,3,5,7,4,9,8};
    vector<int>p2 = {7,1,2,6,7,4,6};

    vector<pair<int, int>> q;
    for(int i=0; i<p1.size(); i++){
        q.push_back(make_pair(p1[i], p2[i]));
    }

    cout<<" printing pair"<<endl;
    for(int i=0; i<q.size(); i++){
        cout<<q[i].first<<"-"<<q[i].second<<endl;
    }

    sort(q.begin(), q.end(), compare);

    cout<<" sorted pair"<<endl;
    for(int i=0; i<q.size(); i++){
        cout<<q[i].first<<"-"<<q[i].second<<endl;
    }
}

```
✅ Summary
---
**Learned Greedy Algorithm concepts with real coding problems.**

---
**Solved Activity Selection, Knapsack, Coin Change, Job Sequencing, Chain of Pairs, Min Abs Difference, Sorting with Comparator.**


---

**All codes implemented in C++ with STL.**
---
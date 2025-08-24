# 🚀 Day 7 of DSA Progress

Today I focused on **sliding window maximum, queues, stacks, and deque implementations** in C++.

---

## ✅ Problems Solved

### 1. Sliding Window Maximum (LeetCode 239)
---


**Concept**: Find maximum in every sliding window of size `k`. 

**Approach**: Use a **deque** to maintain indices of useful elements in decreasing order.  

**Time Complexity**: `O(n)`  

```cpp
class Solution {
public:
    vector<int> maxSlidingWindow(vector<int>& nums, int k) {
        vector<int> res;
        int n = nums.size();
        deque<int> q;

        for(int i=0; i<k; i++){
            while(!q.empty() && nums[q.back()] <= nums[i]){
                q.pop_back();
            }
            q.push_back(i);
        }

        for(int i=k; i<n; i++){
            res.push_back(nums[q.front()]);

            while(!q.empty() && q.front() <= i-k){
                q.pop_front();
            }

            while(!q.empty() && nums[q.back()] <= nums[i]){
                q.pop_back();
            }

            q.push_back(i);
        }

        res.push_back(nums[q.front()]);
        return res;
    }
};
```
---
# 2. Interleaving Queue

**Concept**: Split the queue into two halves and interleave elements.

**Learning**: Showed how to manipulate queues using a helper queue.

```
#include<iostream>
#include<queue>
using namespace std;

void interleave(queue<int>& q) {
    queue<int> p;
    int n = q.size();

    for(int i=0; i<n/2; i++) {
        p.push(q.front());
        q.pop();
    }

    for(int i=0; i<n/2; i++) {
        q.push(p.front());
        p.pop();

        q.push(q.front());
        q.pop();
    }
}

int main() {
    queue<int> q;
    for(int i=0; i<10; i++) q.push(i);

    interleave(q);

    while(!q.empty()) {
        cout << q.front() << " ";
        q.pop();
    }

}
```
---
# 3. Queue Implementation using Deque

**Concept**: Built a custom queue class using std::deque.

**Operations**: push, pop, front, empty.

```
#include<iostream>
#include<deque>
using namespace std;

class Queue {
    deque<int> q;

public:
    void push(int d) { q.push_back(d); }
    void pop() { q.pop_front(); }
    int front() { return q.front(); }
    bool empty() { return q.empty(); }
};

int main() {
    Queue q;
    q.push(1);
    q.push(2);
    q.push(3);
    q.push(4);

    while(!q.empty()) {
        cout << q.front() << " ";
        q.pop();
    }
}
```
---
# 4. Stack Implementation using Deque

**Concept**: Built a custom stack class using std::deque.

**Operations**: push, pop, top, isEmpty.

```
#include<iostream>
#include<deque>
using namespace std;

class Stack {
    deque<int> q;
public:
    void push(int data) { q.push_back(data); }
    void pop() { q.pop_back(); }
    int top() { return q.back(); }
    bool isEmpty() { return q.empty(); }
};

int main() {
    Stack s;
    s.push(1);
    s.push(2);
    s.push(3);
    s.push(4);

    while(!s.isEmpty()) {
        cout << s.top() << " ";
        s.pop();
    }
}
```
---
# 5. Queue Reversal (GFG – Function Template)

**Concept**: Reverse a queue using a stack.

**Learning**: Practical implementation combining stack and queue.

```

class Solution {
public:
    void reverse(queue<int>& q) {
        stack<int> s;
        while(!q.empty()) {
            s.push(q.front());
            q.pop();
        }
        while(!s.empty()) {
            q.push(s.top());
            s.pop();
        }
    }

    queue<int> reverseQueue(queue<int>& q) {
        reverse(q);
        return q;
    }
};
```
---
🔑 Key Takeaways

## deque is extremely versatile: can mimic both stack and queue.


## Sliding window problems become efficient with O(n) solutions using deques.

## Stacks and queues often complement each other beautifully.

## 💡 Today’s practice boosted my confidence with STL containers and their role in solving algorithmic challenges.

## #DSA #C++ #Queue #Stack #Deque #LeetCode #ProblemSolving
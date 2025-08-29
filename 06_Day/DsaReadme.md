# 🚀 Day 6 – DSA Progress  





# 📌 LeetCode 387: First Unique Character in a String

### Problem
Given a string `s`, find the first non-repeating character in it and return its index. If it does not exist, return -1.

### Approach
- Maintain a frequency array `arr[26]` for characters.
- Use a **queue** to store indices of characters as they appear.
- Remove indices from the queue if the character frequency is greater than 1.
- At the end, the **front of the queue** is our answer.

### Code
```cpp
class Solution {
public:
    int firstUniqChar(string s) {
        vector<int> arr(26, 0);
        queue<int> q;

        for (int i = 0; i < s.size(); i++) {
            arr[s[i] - 'a']++;
            q.push(i);

            while (!q.empty() && arr[s[q.front()] - 'a'] > 1) {
                q.pop();
            }
        }

        return q.empty() ? -1 : q.front();
    }
};
```
---
✅ Time Complexity: O(n)
✅ Space Complexity: O(1)
---

# 📌 Queue Implementation using Linked List
Concept
Each node stores a value and a pointer to the next node.

head points to the front of the queue, tail points to the rear.

Push → Add node at the end.

Pop → Remove node from the front.

```
#include<iostream>
using namespace std;

class Node {
public:
    int data;
    Node* next;

    Node(int data) {
        this->data = data;
        this->next = NULL;
    }
};

class queue {
    Node* head;
    Node* tail;

public:
    queue() {
        head = NULL;
        tail = NULL;
    }

    void push(int data) {
        Node* newNode = new Node(data);
        if (head == NULL) {
            head = newNode;
            tail = newNode;
        } else {
            tail->next = newNode;
            tail = newNode;
        }
    }

    void pop() {
        if (isEmpty()) {
            cout << "queue is empty";
            return;
        }
        Node* temp = head;
        head = head->next;
        delete temp;
    }

    int getfront() {
        return (head == NULL) ? -1 : head->data;
    }

    bool isEmpty() {
        return head == NULL;
    }
};

int main() {
    queue q;
    q.push(1);
    q.push(2);
    q.push(3);

    while (!q.isEmpty()) {
        cout << q.getfront() << " ";
        q.pop();
    }
}
```
---
# 📌 Circular Queue Implementation using Array
Concept
Queue implemented with fixed capacity using array.

rear and front wrap around using modulo operator (% capacity).

Efficient O(1) push and pop.



```
#include<iostream>
using namespace std;

class circularqueue {
    int rear;
    int front;
    int* arr;
    int capacity;
    int actualsize;

public:
    circularqueue(int capacity) {
        arr = new int[capacity];
        front = 0;
        rear = -1;
        this->capacity = capacity;
        this->actualsize = 0;
    }

    void push(int data) {
        if (actualsize == capacity) {
            cout << "queue is full \n";
            return;
        }
        rear = (rear + 1) % capacity;
        arr[rear] = data;
        actualsize++;
    }

    void pop() {
        if (isEmpty()) {
            cout << "queue is empty";
            return;
        }
        front = (front + 1) % capacity;
        actualsize--;
    }

    int fronttop() {
        return isEmpty() ? -1 : arr[front];
    }

    bool isEmpty() {
        return actualsize == 0;
    }

    int printrear() {
        return isEmpty() ? -1 : arr[rear];
    }
};

int main() {
    circularqueue q(4);
    q.push(1);
    q.push(2);
    q.push(3);
    q.push(4);
    q.push(5); // will print "queue is full"
    
    cout << q.fronttop() << endl;
    q.pop();
    cout << q.fronttop() << endl;
    q.push(5);
    cout << q.fronttop() << endl;
    cout << q.printrear() << endl;
}
---
```
# 📌 Queue Implementation using Two Stacks
Concept
s1 is the main stack.

For push: Move all elements from s1 → s2, push new element in s1, then move elements back from s2 → s1.

For pop: Just pop from s1.


```
#include<iostream>
#include<stack>
using namespace std;

class queue {
    stack<int> s1, s2;

public:
    void push(int data) {
        while (!s1.empty()) {
            s2.push(s1.top());
            s1.pop();
        }
        s1.push(data);
        while (!s2.empty()) {
            s1.push(s2.top());
            s2.pop();
        }
    }

    void pop() {
        if (isEmpty()) {
            cout << "Queue is empty";
            return;
        }
        s1.pop();
    }

    int top() {
        return isEmpty() ? -1 : s1.top();
    }

    bool isEmpty() {
        return s1.empty();
    }
};

int main() {
    queue q;
    q.push(1);
    q.push(2);
    q.push(3);

    while (!q.isEmpty()) {
        cout << q.top() << " ";
        q.pop();
    }
}
```
---
# 📌 Stack Implementation using Two Queues
Concept
q1 is the main queue.

For push: Move all elements from q1 → q2, push new element in q1, then move back elements from q2.

For pop: Just pop from q1.

```
#include<iostream>
#include<queue>
using namespace std;

class stack {
    queue<int> q1, q2;

public:
    void push(int data) {
        while (!q1.empty()) {
            q2.push(q1.front());
            q1.pop();
        }
        q1.push(data);
        while (!q2.empty()) {
            q1.push(q2.front());
            q2.pop();
        }
    }

    void pop() {
        if (q1.empty()) {
            cout << "stack is empty";
            return;
        }
        q1.pop();
    }

    int front() {
        return q1.empty() ? -1 : q1.front();
    }

    bool isEmpty() {
        return q1.empty();
    }
};

int main() {
    stack s;
    s.push(1);
    s.push(2);
    s.push(3);

    while (!s.isEmpty()) {
        cout << s.front() << " ";
        s.pop();
    }
}
```
---
# 📝 Summary
In this repository, we covered:

LeetCode 387 solution using queue.

Queue using Linked List.

Circular Queue using Array.

Queue using Two Stacks.

Stack using Two Queues.

These implementations give a solid foundation in queue/stack fundamentals and demonstrate multiple ways of solving the same problem using different data structures.
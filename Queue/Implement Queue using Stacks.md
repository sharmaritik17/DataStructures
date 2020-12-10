``` cpp
https://leetcode.com/problems/implement-queue-using-stacks/

/*^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^*/amortized complexity would be O(1)-- TC/SC
class MyQueue {
public:
    int front_ele = 0;
    stack<int> in, out;
    /** Initialize your data structure here. */
    // MyQueue() {

    // }

    /** Returns whether the queue is empty. */
    bool empty() {
        return in.empty() && out.empty();
    }

    /** Push element x to the back of queue. */
    void push(int x) {
        in.push(x);
    }

    /** Removes the element from in front of queue and returns that element. */
    int pop() {
        peek();
        int save_later = out.top();
        out.pop();
        
        return save_later;
    }

    /** Get the front element. */
    int peek() {
        if (out.empty()) {
            while (!in.empty()) {
                out.push(in.top());
                in.pop();
            }
        }
        return out.top();
    }

};

/*^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^*/
class MyQueue {
public:
    int front_ele = 0;
    stack<int> s1, s2;
    /** Initialize your data structure here. */
    // MyQueue() {

    // }

    /** Returns whether the queue is empty. */
    bool empty() {
        return s1.size()==0;
    }

    /** Push element x to the back of queue. */
    void push(int x) {
        if (s1.empty()) {
            front_ele = x;
        }
        while (!s1.empty()) {
            s2.push(s1.top());
            s1.pop();
        }

        s2.push(x);

        while (!s2.empty()) {
            s1.push(s2.top());
            s2.pop();
        }
    }

    /** Removes the element from in front of queue and returns that element. */
    int pop() {
        int save_return = s1.top();
        s1.pop();

        if (!s1.empty())
            front_ele = s1.top();
        return save_return;
    }

    /** Get the front element. */
    int peek() {
        return front_ele;
    }

};

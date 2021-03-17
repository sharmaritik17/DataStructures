https://leetcode.com/problems/flatten-nested-list-iterator/


https://leetcode.com/problems/flatten-nested-list-iterator/discuss/80234/evolve-from-intuition-to-optimal-a-review-of-top-solutions


``` cpp

class NestedIterator {
public:
    NestedIterator(vector<NestedInteger> &nestedList) {
        begins.push(nestedList.begin());
        ends.push(nestedList.end());
    }

    int next() {
        hasNext();
        return (begins.top()++)->getInteger(); //++ needs to be done here so begin will meet end
    }

    bool hasNext() {
        while (begins.size()) {
            if (begins.top() == ends.top()) {
                begins.pop();
                ends.pop();
            } else {
                auto x = begins.top();
                if (x->isInteger())
                    return true;
                begins.top()++; 
                // this is for ex [1,[2,3],4]
                // to make top of begins start pointing to iterator on '4'  
                // before we proceed processing whole '[2,3]' so that at the end begins.top() == ends.top() 
                // this will meet simultaneously
                begins.push(x->getList().begin());
                ends.push(x->getList().end());
            }
        }
        return false;
    }

private:
    stack<vector<NestedInteger>::iterator> begins, ends;
};







class NestedIterator {
private:
    stack<NestedInteger*> nodes;
    
public:
    NestedIterator(vector<NestedInteger> &nestedList) {
        for(int i = nestedList.size() - 1; i >= 0; --i) {
            nodes.push(&nestedList[i]);
        }
    }
    
    int next() {
        int result = nodes.top()->getInteger();
        nodes.pop();
        return result;
    }
    
    // only flatten the Current Level until we find an integer. 
    bool hasNext() {
        while(!nodes.empty()) {
            NestedInteger* curr = nodes.top();
            // ensure the top most element is an integer not an integer list
            if (curr->isInteger()) {
                return true;
            }
            
            nodes.pop();
            
            // decouple the integer list and add the decoupled element back to stack
            vector<NestedInteger>& adjs = curr->getList();
            for(int i = adjs.size() - 1; i >= 0; --i) {
                nodes.push(&adjs[i]);
            }
        }
        
        return false;
    }
};




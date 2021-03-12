
/*^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^*/ using recursion only

``` cpp
void sort_helper(stack<int> &s,int data) {
	if (!s.size() || s.top() <= data) {
		s.push(data);
		return;
	}

	int top_element = s.top();
	s.pop();
	sort_helper(s,data);
	s.push(top_element);
}
void SortedStack :: sort()
{
	//Your code here
	if (!s.size() || s.size() == 1)
		return;

	int top_element = s.top();
	s.pop();
	sort();
	sort_helper(s,top_element);
	return;
}

/*^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^*/ using one stack
void SortedStack :: sort()
{
	//Your code here
	if (!s.size() || s.size() == 1)
		return;
      stack<int> st;
	int top_element = s.top();
	s.pop();
    while(!st.empty() && st.top()>top_element){
    	s.push(st.top());
        st.top();
    }

    st.push(top_element);

    //return st; //stack as all srted elements are in st now
}

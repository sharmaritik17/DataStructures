https://leetcode.com/problems/remove-all-adjacent-duplicates-in-string/
``` cpp
my solution----- /*^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^*/
 https://leetcode.com/problems/remove-all-adjacent-duplicates-in-string/discuss/902741/Unique-approach-easy-buzzy-faster-than-98.87-online-submissions
``` cpp
/*^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^*/
class Solution {
public:
string removeDuplicates(string s) {
	if(s.empty())
		return "";
	int n=s.length();
    int i=0;
    for(int j=0;j<n;j++,i++){
    	s[i] = s[j];

    	if(i>0 && s[i-1] == s[i]){
    		i = i-2;
    	}
    }
    return s.substr(0,i);
}
};
---------------------------------------------------------STACK------------------------------------------
class Solution {
public:
string removeDuplicates(string s) {
	if(s.empty())
		return "";
	stack<char> st;
	st.push(s[0]);
	string res = "";
	for (int i = 1; s[i] != '\0'; i++) {
		if (!st.empty() && st.top() == s[i])
			st.pop();
		else
			st.push(s[i]);
	}

	while (!st.empty()) {
		res = st.top() + res;
		st.pop();
	}
	return res;
}
---------------------------------------------------------my solution---------------------------------------------------------------------------------
class Solution {
public:
	string removeDuplicates(string s) {
		if (s.empty())
			return "";

		int n = s.length();
		int ptr = -1;
        int  i = 0;
		while (i < n) {
			if (ptr == -1 || s[ptr] != s[i]) {
				ptr++;
				s[ptr] = s[i];
				i++;
			}
			else {
				while (i < n && ptr>-1 && s[ptr] == s[i]) {
					ptr--;
					i++;
				}
			}
		}

		return s.substr(0,ptr+1);
	}
};

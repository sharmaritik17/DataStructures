https://leetcode.com/problems/html-entity-parser/

https://leetcode.com/problems/html-entity-parser/discuss/1116016/Trie-or-C%2B%2B-or-Without-Map

https://leetcode.com/problems/html-entity-parser/discuss/575416/C%2B%2B-two-pointers-O(n)-or-O(1)
``` cpp
class Solution {
  class Trie{
      public:
    Trie *children[26] = {};
    char terminal = 0;

    void insert(string &w, char ch, int p = 0) {
        if (p == w.size())
            terminal = ch;
        else {
            if (children[w[p] - 'a'] == nullptr)
                children[w[p] - 'a'] = new Trie();
            children[w[p] - 'a']->insert(w, ch, p + 1);
        }
    }

    char isValid(string &word,int st,int sz){
      if(terminal!=0 && sz==0){
        return terminal;
      }

      if(word[st]<'a' || word[st]>'z' || children[word[st]-'a']==NULL){
        return 0;
      }

      return children[word[st]-'a']->isValid(word,st+1,sz-1);
    }
  };


  vector<pair<string, char>> special = {{"gt", '>'}, {"lt", '<'},
    {"amp", '&'}, {"quot", '"'}, {"apos", '\''}, {"frasl", '/'}};


public:
  string entityParser(string s) {
    Trie root;
    //insert in trie
    for(auto &[str,ch]:special){
      root.insert(str,ch);
    }

    int st = 0,end = 0;
    for(int i=0;i<s.size();i++,end++){
      s[end] = s[i];
      if(s[end]=='&'){
        st = end;
      }
      if(s[end]==';'){
        auto ch = root.isValid(s,st+1,end-st-1);
        // if special char found then put that one
        if(ch!=0){
          end = st;
          s[end] = ch;
        }
        //pointing to next char in string now
        st = end+1;
      }
    }

    s.resize(end);
    return s;
  }
};

Word Count Engine
Implement a document scanning function wordCountEngine, which receives a string document and returns a list of all unique words in it and their number of occurrences, sorted by the number of occurrences in a descending order. If two or more words have the same count, they should be sorted according to their order in the original sentence. Assume that all letters are in english alphabet. You function should be case-insensitive, so for instance, the words “Perfect” and “perfect” should be considered the same word.

The engine should strip out punctuation (even in the middle of a word) and use whitespaces to separate words.

Analyze the time and space complexities of your solution. Try to optimize for time while keeping a polynomial space complexity.

Examples:

input:  document = "Practice makes perfect. you'll only
                    get Perfect by practice. just practice!"

output: [ ["practice", "3"], ["perfect", "2"],
          ["makes", "1"], ["youll", "1"], ["only", "1"], 
          ["get", "1"], ["by", "1"], ["just", "1"] ]
Important: please convert the occurrence integers in the output list to strings (e.g. "3" instead of 3). We ask this because in compiled languages such as C#, Java, C++, C etc., it’s not straightforward to create mixed-type arrays (as it is, for instance, in scripted languages like JavaScript, Python, Ruby etc.). The expected output will simply be an array of string arrays.

Constraints:

[time limit] 5000ms
[input] string document
[output] array.array.string

``` cpp

MINE CODE
#include <iostream>
#include <string>
#include <vector>

using namespace std;

vector<vector<string>> wordCountEngine( const string& document ) 
{
  // your code goes here
  queue<string> pendingWords;
  unordered_map<string,int> occurencesMap;
  int n = document.size();
  //extract words
  string temp="";
  for(int i=0;i<n;i++){
    if('a'>=document[i]<='z' && 'A'>=document[i]<='Z'){
      temp+=document[i];
    }
    else if(document[i]==' '){
      string afterConvert = "";
      for(int j =0;j<temp.size();j++){
        afterConvert+=tolower(temp[j]);
      }
      if(occurencesMap.find(afterConvert)==occurencesMap.end()){
        pendingWords.push(afterConvert);
      }
      occurencesMap[afterConvert]++;
      temp = "";
    }
  }
  
  vector<vector<string>> result;
  
  
  vector<vector<string>> pointOccurences(n);
  
  while(pendingWords.size()){
    
    auto frontStr = pendingWords.front();
    pendingWords.pop();
    
    int freq = occurencesMap[frontStr];
    
    pointOccurences[freq].push_back(frontStr);
  }
  
  int i=0;
  while(i<n){
    for(int j=pointOccurences[i].size()-1;j>=0;j--){
      vector<string> current;
      current.push_back(pointOccurences[j]);
      current.push_back(to_string(j));
      
      result.push_back(current);
    }
    i++;
  }
  
  
  return result;
}

CORRECT CODE

#include <iostream>
#include <string>
#include <vector>
#include <unordered_map>
#include <sstream>

using namespace std;

void parseWords(const string& str, vector<string>& words, unordered_map<string, int>& wordCount) {
  stringstream ss(str);
  string word;
  
  while (ss >> word) {
    string w = "";
    for (char c : word) {
      c = tolower(c);
      if (c >= 'a' and c <= 'z') {
        w += c;
      }
    }
    
    if (w != "") {
      wordCount[w]++;
    
      if (wordCount[w] == 1) {
        words.push_back(w);
      }
    }
  }
}

vector<vector<string>> wordCountEngine( const string& document ) 
{
  // your code goes here
  unordered_map<string, int> wordCount;
  vector<string> words;
  
  parseWords(document, words, wordCount);
  
  vector<vector<string>> sortedWords(words.size());
  
  for (string& word : words) {
    sortedWords[wordCount[word]-1].push_back(word);
  }
  reverse(sortedWords.begin(), sortedWords.end());
  vector<vector<string>> result;
  
  for (auto it = sortedWords.begin(); it != sortedWords.end(); it++) {
    for (string word : (*it)) {
      result.push_back({word, to_string(wordCount[word])});
    }
  }
  
  return result;
}

int main() {
  return 0;
}

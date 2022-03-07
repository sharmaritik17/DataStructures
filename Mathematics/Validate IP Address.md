Validate IP Address
Validate an IP address (IPv4). An address is valid if and only if it is in the form "X.X.X.X", where each X is a number from 0 to 255.

For example, "12.34.5.6", "0.23.25.0", and "255.255.255.255" are valid IP addresses, while "12.34.56.oops", "1.2.3.4.5", and "123.235.153.425" are invalid IP addresses.

Examples:

ip = '192.168.0.1'
output: true

ip = '0.0.0.0'
output: true

ip = '123.24.59.99'
output: true

ip = '192.168.123.456'
output: false
Constraints:

[time limit] 5000ms
[input] string ip
[output] boolean



``` cpp
#import <iostream>
#import <string>
#include  <cstring>

using namespace std;

bool checkIfValid(string str){
  if(str.size()==0 || (str.size()>1 && str[0]=='0')){ 
    return false;
  }
  for(int i=0;i<str.size();i++){
    if('0'> str[i] || str[i]>'9'){
      return 0;
    }
  }
  int num = stoi(str);
  if(0<=num && num<=255){
    return 1;
  }
  return 0;
}

bool validateIP(const string& ip)
{
	// your code goes here
  int n = ip.size();
  
  if(n<=3){
    return false;
  }
  
  int dotSoFar = 0;
  
  string curr = "";
  
  for(int i=0;i<=n;i++){
    if(i!=n && ip[i]!='.') curr+=ip[i];
    
    if(i!=n && ip[i]=='.'){
      dotSoFar++;
      if(dotSoFar>=4){
        return false;
      }
    }
    
    if(i==n || ip[i]=='.'){
      if(curr.size()>3 || checkIfValid(curr)==false){
        return false;
      }
      curr = "";
    }
  }
  return true;
}

int main() 
{
	return 0;
}


/*
--> 0 to 255
--> . . .

'...'

255 . . .

.121..


TC

12.34.56.1ops
....
192.168.123.456
192.168.123.255.48
.125.42.36

1.025.12
*/

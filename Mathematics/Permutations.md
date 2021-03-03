`Given a smaller string s and a bigger string b, design an algorithm to find all permutations of the shorter string within the longer one. Print the location of each permutation./ to count only'

``` cpp
//only lower case chars
int findAllpermutations(string small, string larger) {
    int freqSmall[26] = {0};
    //window size
    int n = small.length();

    //to return
    int finalAns = 0;

    for (char a : small) {
        freqSmall[a - 97]++;
    }

    int freqlarger[26]={0};
    int count = 0;
    int j = 0;

    for (int i = 0; larger[i] != '\0'; i++) {
        freqlarger[larger[i] - 97]++;
        count++;

        if (count == n) {
            count = 0;
            int i;
            for (i = 0; i < 26; i++) {
                if (freqlarger[i] != freqSmall[i]) {
                    break;
                }
            }
            if (i == 26) {
                finalAns++;
            }
            freqlarger[larger[j] - 97]--;
            j++;
        }

    }
    return finalAns;
}

int main() {
    string s, t;
    cin >> s >> t;
    cout << findAllpermutations(s, t) << endl;
    return 0;
}

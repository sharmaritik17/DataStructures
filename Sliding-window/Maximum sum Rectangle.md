https://practice.geeksforgeeks.org/problems/maximum-sum-rectangle/0#


/*^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^*/
``` cpp
#include <iostream>
#include  <bits/stdc++.h>
using namespace std;

int kadane(int rowSum[], int n) {
    int maxp = rowSum[0];
    int curr_max = rowSum[0];

    for (int i = 1; i < n; i++) {
        curr_max = max(curr_max + rowSum[i], rowSum[i]);
        maxp = max(curr_max, maxp);
    }
    return maxp;
}

int maxRectangle(int **mat, int row, int col) {
    int ans = 0;

    for (int left = 0; left < col; left++) {

        int rowSum[row] = {0};

        for (int right = left; right < col; right++) {
            for (int i = 0; i < row; i++) {
                rowSum[i] += mat[i][right];
            }

            ans = max(ans, kadane(rowSum, row));
        }

        //dynamically deleted
        //delete[] rowSum;
    }
    return ans;
}



int main() {
    int t = 0;
    cin >> t;
    while (t--) {
        int row = 0, col = 0;
        cin >> row >> col;
        int **mat = new int*[row];
        for (int i = 0; i < row; i++) {
            mat[i] = new int[col];
        }
        for (int i = 0; i < row; i++) {
            for (int j = 0; j < col; j++) {
                int x = 0;
                cin >> x;
                mat[i][j] = x;
            }
        }

        cout << maxRectangle(mat, row, col) << "\n";

        for (int i = 0; i < row; i++) {
            delete[] mat[i];
        }
        delete[] mat;
    }
    return 0;
}
```


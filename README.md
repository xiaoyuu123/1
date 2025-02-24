#include <stdio.h>
#include <stdlib.h>

#define MAX(a,b) ((a) > (b)? (a) : (b))

int maxSubArraySum(int arr[], int n) {
    int sum = 0;
    int maxSum = arr[0];
    for (int i = 0; i < n; i++) {
        sum = MAX(arr[i], sum + arr[i]);
        maxSum = MAX(maxSum, sum);
    }
    return maxSum;
}

int main() {
    int n;
    scanf("%d", &n);
    int* arr = (int*)malloc(n * sizeof(int));
    int* prefixSum = (int*)malloc((n + 1) * sizeof(int));
    prefixSum[0] = 0;
    for (int i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
        prefixSum[i + 1] = prefixSum[i] + arr[i];
    }
    int maxSum = arr[0];
    int totalSum = prefixSum[n];
    for (int i = 0; i < n; i++) {
        for (int j = i; j < n; j++) {
            int sum1 = prefixSum[i + 1];
            int sum2 = totalSum - prefixSum[j + 1];
            int curMax = sum1 + sum2;
            maxSum = MAX(maxSum, curMax);
            sum1 = prefixSum[j + 1];
            sum2 = totalSum - prefixSum[i + 1];
            curMax = sum1 + sum2;
            maxSum = MAX(maxSum, curMax);
        }
    }
    printf("%d\n", maxSum);
    free(arr);
    free(prefixSum);
    return 0;
}

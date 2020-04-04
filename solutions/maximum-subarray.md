# Version 1
```C
int maxSubArray(int* nums, int numsSize){
    int* dp = malloc(numsSize*sizeof(int));
    dp[0] = nums[0];
    int max = dp[0];
    for(int i=1; i<numsSize; i++){
        dp[i] = (dp[i-1] > 0 ? dp[i-1] : 0) + nums[i];
        if(max < dp[i]) max = dp[i];
    }
    return max;
}
```

# Version 2
```C
int maxSubArray(int* nums, int numsSize){
    int sum = nums[0];
    int max = nums[0];
    for(int i=1; i<numsSize; i++){
        if(sum < 0) sum = nums[i];
        else sum += nums[i];
        if(max < sum) max = sum;
    }
    return max;
}
```
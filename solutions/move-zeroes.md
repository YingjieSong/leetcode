# Version 1
```C
void moveZeroes(int* nums, int numsSize){
    for(int i=0; i<numsSize; i++){
        if(nums[i]==0){
            int j=i;
            while(j<numsSize && nums[j]==0){
                j++;
            }
            if(j==numsSize) return;
            for(int k=i; k<j; k++){
                if(k+j-i>=numsSize) break;
                nums[k] = nums[k+j-i];
                nums[k+j-i] = 0;
            }
        }
    }
}
```

# Version 2
```C
void moveZeroes(int* nums, int numsSize){
    int i = 0;
    for(int j = 1; j<numsSize; j++){
        if(nums[i] != 0){
            i++;
        }else if(nums[j] != 0){
            nums[i] = nums[j];
            nums[j] = 0;
            i++;
        }
    }
}
```
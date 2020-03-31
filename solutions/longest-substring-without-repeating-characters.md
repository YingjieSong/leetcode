## Version 1
```C
int lengthOfLongestSubstring(char * s){
    int len = strlen(s);
    if(len == 0) return 0;
    if(len == 1) return 1;
    int max = 1;
    int start = 0;
    int end;
    int i;
    for(end = 1; end < len; end++){
        for(i = start; i < end; i++){
            if(s[end] == s[i]){
                if(max < end - start) max = end - start;
                start = i + 1;
                break;
            }
        }
        if(max >= len - start) return max;
    }
    if(max < end - start) return end - start;
    return max;
}
```

## Version 2
```C
int lengthOfLongestSubstring(char * s){
    if(*s == NULL) return 0;
    
    bool arr[256] = {0};
    
    char* start = s;
    char* end = s + 1;
    
    arr[*start] = 1;
    int length = 1;
    int max = length;
    
    while(*end != NULL){
        if(arr[*end]){
            do{
                arr[*(start++)] = 0;
                length--;
            }while(*start != *end);
        }else{
            arr[*(end++)] = 1;
            if(max < ++length) max = length;
        }
    }
    
    return max;
}
```
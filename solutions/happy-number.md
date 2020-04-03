# [Happy Numbers](https://en.wikipedia.org/wiki/Happy_number#10-happy_numbers)
"the only cycle is the eight-number cycle"

# Version 1
```C
bool isHappy(int n){
    while(n != 4){
        n = sqsum(n);
        if(n==1) return true;
    }
    return false;
}

int sqsum(int n){
    int sum = 0;
    while(n!=0){
        sum += pow(n%10, 2);
        n = n/10;
    }
    return sum;
}
```
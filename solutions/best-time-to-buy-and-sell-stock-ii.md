# Version 1
```C
int maxProfit(int* prices, int pricesSize){
    int max = 0;
    for(int i=0; i<pricesSize-1; i++){
        if(prices[i] < prices[i+1]){
            max += prices[i+1] - prices[i];
        }
    }
    return max;
}
```
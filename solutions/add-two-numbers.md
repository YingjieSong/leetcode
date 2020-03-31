## General Definitions
```C
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */
```

## Version 1
```C
struct ListNode* addTwoNumbers(struct ListNode* l1, struct ListNode* l2){
    struct ListNode* one = malloc(sizeof(struct ListNode));
    one->val = 1;
    one->next = NULL;
    if(l1 != NULL && l2 != NULL){
        l1->val += l2->val;
        l1->next = addTwoNumbers(l1->next, l2->next);
        if(l1->val >= 10){
            l1->val %= 10;
            l1->next = addTwoNumbers(l1->next, one);
        }
        return l1;
    }else if(l1 != NULL){
        return l1;
    }else if(l2 != NULL){
        return l2;
    }return NULL;
}
```

## Version 2
```C
struct ListNode* addTwoNumbersHelper(struct ListNode* l1, struct ListNode* l2, int carry){
    if(l1 == NULL && l2 == NULL && !carry) return NULL;
    
    struct ListNode* head = (struct ListNode*)malloc(sizeof(struct ListNode));
    
    if(l1 == NULL && l2 == NULL){
        head->val = 1;
        head->next = NULL;
    }else if(l1 == NULL){
        if(carry && l2->val == 9){
            head->val = 0;
            head->next = addTwoNumbersHelper(NULL, l2->next, 1);
        }else{
            head->val = l2->val + carry;
            head->next = l2->next;
        }
    }else if(l2 == NULL){
        if(carry && l1->val == 9){
            head->val = 0;
            head->next = addTwoNumbersHelper(l1->next, NULL, 1);
        }else{
            head->val = l1->val + carry;
            head->next = l1->next;
        }
    }else{
        int sum = l1->val + l2->val + carry;
        if(sum > 9){
            head->val = sum - 10;
            head->next = addTwoNumbersHelper(l1->next, l2->next, 1);
        }else{
            head->val = sum;
            head->next = addTwoNumbersHelper(l1->next, l2->next, 0);
        }
    }
    return head;
}

struct ListNode* addTwoNumbers(struct ListNode* l1, struct ListNode* l2){
    return addTwoNumbersHelper(l1, l2, 0);
}
```

## Version 2.1
```C
struct ListNode* addTwoNumbersHelper(struct ListNode* l1, struct ListNode* l2, int carry){
    if(l1 == NULL && l2 == NULL && !carry) return NULL;
    
    struct ListNode* head = (struct ListNode*)malloc(sizeof(struct ListNode));
    
    int sum = carry;
    if(l1 != NULL){
        sum += l1->val;
        l1 = l1->next;
    }
    if(l2 != NULL){
        sum += l2->val;
        l2 = l2->next;
    }
    head->val = sum % 10;
    head->next = addTwoNumbersHelper(l1, l2, sum / 10);
    return head;
}

struct ListNode* addTwoNumbers(struct ListNode* l1, struct ListNode* l2){
    return addTwoNumbersHelper(l1, l2, 0);
}
```

## Version 3
```C
struct ListNode* addTwoNumbersHelper(struct ListNode* l1, struct ListNode* l2, int carry){
    struct ListNode* head = NULL;
    struct ListNode** node = &head;
    
    while(l1 != NULL || l2 != NULL || carry){
        int sum = carry;
        if(l1 != NULL){
            sum += l1->val;
            l1 = l1->next;
        }
        if(l2 != NULL){
            sum += l2->val;
            l2 = l2->next;
        }
        (*node) = (struct ListNode*)malloc(sizeof(struct ListNode));
        (*node)->val = sum % 10;
        carry = sum / 10;
        node = &((*node)->next);
    }
    *node = NULL;
    
    return head;
}

struct ListNode* addTwoNumbers(struct ListNode* l1, struct ListNode* l2){
    return addTwoNumbersHelper(l1, l2, 0);
}
```

## Version 3.1
```C
struct ListNode* addTwoNumbers(struct ListNode* l1, struct ListNode* l2){
    int sum = 0;
    struct ListNode* head = NULL;
    struct ListNode** node = &head;
    
    while(l1 != NULL || l2 != NULL || sum){
        if(l1 != NULL){
            sum += l1->val;
            l1 = l1->next;
        }
        if(l2 != NULL){
            sum += l2->val;
            l2 = l2->next;
        }
        *node = (struct ListNode*)malloc(sizeof(struct ListNode));
        (*node)->val = sum % 10;
        sum /= 10;
        node = &((*node)->next);
    }
    *node = NULL;
    
    return head;
}
```
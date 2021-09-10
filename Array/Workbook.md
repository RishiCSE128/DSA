# Two number sum 
Given a array, find the index of a pair of numbers that add up to a given sum. 

## Bruteforce Solution 
```
use 2 pointers p1,p2
1. p1:=0     // init p1
2. while p1 < n-1{
    3. p2:=p1+1  // set p2 as next to p1  
    4. d = t - A[p1]  // calculate difference 
    5. while p2 < n{ 
            6. if A[p2] == d then return p1, p2  // if difference exists return pointers
            7. p2++  // otherwise scan till the end of the array 
       }
    8. p1++ // if no diff found, update P1 
  } 
```



```python
def pair_sum_bf(A,target):
    for p1 in range(0,len(A)-1):
        diff = target - A[p1] 
        print(f'P1 = {p1}, A[{p1}] = {A[p1]} , diff = {diff}')
        for p2 in range(p1+1, len(A)):
            print(f'\t p2 = {p2}, A[{p2}] = {A[p2]}')
            if A[p2] == diff:
                print('\t Found!')
                return [p1,p2]
    return []
```


```python
A = [1,3,7,9,2]
target = 11
```


```python
pair_sum_bf(A,target)
```

    P1 = 0, A[0] = 1 , diff = 10
    	 p2 = 1, A[1] = 3
    	 p2 = 2, A[2] = 7
    	 p2 = 3, A[3] = 9
    	 p2 = 4, A[4] = 2
    P1 = 1, A[1] = 3 , diff = 8
    	 p2 = 2, A[2] = 7
    	 p2 = 3, A[3] = 9
    	 p2 = 4, A[4] = 2
    P1 = 2, A[2] = 7 , diff = 4
    	 p2 = 3, A[3] = 9
    	 p2 = 4, A[4] = 2
    P1 = 3, A[3] = 9 , diff = 2
    	 p2 = 4, A[4] = 2
    	 Found!
    




    [3, 4]



Now lets add the boundary conditions



```python
def pair_sum_bf(A,target):
    if len(A) == 0:    #empty array
        return []
    elif len(A) == 1: #singliton array
        return []
    else:
        for p1 in range(0,len(A)-1):
            diff = target - A[p1] 
            print(f'P1 = {p1}, A[{p1}] = {A[p1]} , diff = {diff}')
            for p2 in range(p1+1, len(A)):
                print(f'\t p2 = {p2}, A[{p2}] = {A[p2]}')
                if A[p2] == diff:
                    print('\t Found!')
                    return [p1,p2]
        return []
```


```python
pair_sum_bf(A,target)
```

    P1 = 0, A[0] = 1 , diff = 10
    	 p2 = 1, A[1] = 3
    	 p2 = 2, A[2] = 7
    	 p2 = 3, A[3] = 9
    	 p2 = 4, A[4] = 2
    P1 = 1, A[1] = 3 , diff = 8
    	 p2 = 2, A[2] = 7
    	 p2 = 3, A[3] = 9
    	 p2 = 4, A[4] = 2
    P1 = 2, A[2] = 7 , diff = 4
    	 p2 = 3, A[3] = 9
    	 p2 = 4, A[4] = 2
    P1 = 3, A[3] = 9 , diff = 2
    	 p2 = 4, A[4] = 2
    	 Found!
    




    [3, 4]



Lets test the boundary conditions 


```python
A = []
target = 11
pair_sum_bf(A,target)
```




    []




```python
A = [11]
target = 11
pair_sum_bf(A,target)
```




    []



## Optimization
* The bruteforce solution is $O(n^2)$
* Problem of repeated lookups are often solved by a Hashmap. lookingup of a hashmap is $O(1)



```python
def pair_sum_opt(A, target):
    if len(A) == 0:
        return []
    elif len(A) == 1:
        return []
    else:
        hash_map = {} # init with empty dict 
        for p in range(len(A)): # for pointer to all elem : O(n)
            print(f'p={p} , A[p]={A[p]}, \n map={hash_map}')
            diff = target - A[p] 
            if A[p] not in hash_map.keys(): # if pointed element not in map
                hash_map[diff] = p  # create {diff : p}, difference for which pointer
            else:      # if in map
                return [ p,hash_map[ A[p] ] ] # return poiner, value at map entry keyed by pointed value
        return []
```


```python
A = [1,3,7,9,2]
target = 11
pair_sum_opt(A, target)
```

    Wall time: 0 ns
    p=0 , A[p]=1, 
     map={}
    p=1 , A[p]=3, 
     map={10: 0}
    p=2 , A[p]=7, 
     map={10: 0, 8: 1}
    p=3 , A[p]=9, 
     map={10: 0, 8: 1, 4: 2}
    p=4 , A[p]=2, 
     map={10: 0, 8: 1, 4: 2, 2: 3}
    




    [4, 3]




```python
A = []
target = 11
pair_sum_opt(A, target)
```




    []




```python
A = [11]
target = 11
pair_sum_opt(A, target)
```




    []




```python

```

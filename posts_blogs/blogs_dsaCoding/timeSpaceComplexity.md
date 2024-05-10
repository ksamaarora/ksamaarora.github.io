---
layout: default
title: DSA Coding
---

> ### Time Complexity

Time complexity does not refer to the time taken by the machine to execute a particular code as different machines may take different time based on their configurations. 

**"The rate at which the time taken increases with respect to the input size is called Time Complexity."** 

Basically, the time complexity of a particular code depends on the given input size, not on the machine used to run the code. Time complexity is calculated in terms of Big-Oh Notation.

[![Screenshot-2024-05-10-at-7-00-30-PM.png](https://i.postimg.cc/J4sJs4yt/Screenshot-2024-05-10-at-7-00-30-PM.png)](https://postimg.cc/4mTnMGQT)

**Rules** for calculating Time Complexity:
  - Time complexity to be computed in terms of worst case scenario
  - Avoid constants
  - Avoid lower values 

**Best Case:** This term refers to the case where the code takes the least amount of time to get executed.
**Worst Case:** This term refers to the case where the code takes the maximum amount of time to get executed.
**Average Case:** This term is pretty self-explanatory. This is basically the case between the best and the worst.

- Notations:
[![Screenshot-2024-05-10-at-7-07-56-PM.png](https://i.postimg.cc/HLnFKhBr/Screenshot-2024-05-10-at-7-07-56-PM.png)](https://postimg.cc/sBFnGwFz)

Refer to Some Examples Here

```c++
// Example 1:
for(int i=0; i<N; i++){
    for(int j=0; j<N; j++){
        // Block of code 
    }
}
```
[![Screenshot-2024-05-10-at-7-14-46-PM.png](https://i.postimg.cc/XYrYKQdg/Screenshot-2024-05-10-at-7-14-46-PM.png)](https://postimg.cc/K1ybx79K)

```c++
// Example 2:
for(int i=0; i<N; i++){
    for(int j=0; j<i; j++){
        // Block of code 
    }
}
```
[![Screenshot-2024-05-10-at-7-15-47-PM.png](https://i.postimg.cc/pdP1b1Cf/Screenshot-2024-05-10-at-7-15-47-PM.png)](https://postimg.cc/681hCcDq)

> ### Space Complexity:

It is the memory space that your program takes. We use Big-Oh Notation.

```bash 
Auxiliary Space + Input Space = Space Complexity
// Auxiliary space refers to the space that we use additionally to solve a problem. 
// Input space refers to the space that we use to store the inputs.
```

- Example 1: int arr[N] Space complexity is O(N)
- Example 2: 
```c++
Input(a) // Input Space
Input(b) // Input Space 
c=a+b // c is Auxiliary Space
// Space Complexity is O(3)
```

NOTE: Never do anything to the input because input data should not be touched i.e. don’t do b=a+b.

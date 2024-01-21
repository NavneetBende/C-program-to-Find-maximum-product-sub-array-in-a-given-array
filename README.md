Maximum product of sub-array in C
Here, in this page we will discuss the program to find the maximum product of sub-array in C programming language. We will discuss the two different ways to find the maximum product.

maximum product of sub-array in C
While loop in C
Example
Input : arr = [ 10, -20, -30, 0, 70, -80, -20 ]
Output : Maximum product sub-array is 112000
Explanation : Sub-array [70, -80, -20] gives the maximum product 112000
Here, we will discuss the following two methods, and compare the complexity of them,

Method 1 : Naive solution
Method 2 : Efficient solution
Let’s discuss above two methods in brief.

Method 1 :
Create a variable say result, set result = arr[0], this variable hold the required maximum product.
Run a loop for range(n)
Create a variable mul = arr[i], this variable hold the product of sub-array.
Run a inner loop, set result = max(result, mul)
And, mul *= arr[j]
Update, result = max(result, mul)
Return result.
Time and Space Complexity :
Time Complexity : O(n2)
Space Complexity : O(1)
Related Pages
Counting the number of even and odd elements in an array

Find all Symmetric pairs in an array

Finding Arrays are disjoint or not

Determine Array is a subset of another array or not

Determine can all numbers of an array be made equal

Method 1 : Code in C
Run
#include<stdio.h>

int main(){
    int arr[] = { 10, -20, -30, 0, 70, -80, -20 };
    int n=sizeof(arr)/sizeof(arr[0]);
    int result = arr[0];
    
    for (int i = 0; i < n; i++)
    {
        int mul = arr[i];
        // traversing in current subarray
        for (int j = i + 1; j < n; j++) { // updating result every time // to keep an eye over the // maximum product if(mul>result)
                result = mul;
            mul *= arr[j];
        }
        if(mul>result)
                result = mul;
    }
    
    printf("Maximum Product of sub-array is %d", result);
}
Output
Maximum Product of sub-array is 1600
Method 2 :
This is the efficient solution and is also similar to Largest Sum Contiguous Subarray problem which uses Kadane’s algorithm.

Declare three variables say max_so_far, max_ending_here & min_ending_here.
For every index the maximum number ending at that index will be the maximum(arr[i], max_ending_here * arr[i], min_ending_here[i]*arr[i]).
Similarly the minimum number ending here will be the minimum of these 3.
Thus we get the final value for maximum product subarray.
Time and Space Complexity :
Time Complexity : O(n)
Space Complexity : O(1)
Method 2 : Code in C
Run
#include<stdio.h>

int max(int a, int b, int c){
    
    if(a>=b && a>=c)
        return a;
    if(b>=a && b>=a)
        return b;
    return c;
    
}

int min(int a, int b, int c){
    
    if(a<=b && a<=c)
        return a;
    if(b<=a && b<=a)
        return b;
    return c;
    
}


int main(){
    int arr[] = { 1, -2, -3, 0, 7, -8, 2};
    int n=sizeof(arr)/sizeof(arr[0]);
    int max_ending_here = arr[0];
 
    // min negative product ending
    // at the current position
    int min_ending_here = arr[0];
 
    // Initialize overall max product
    int max_so_far = arr[0];
    
    for (int i = 1; i < n; i++) { int temp = max(arr[i], arr[i] * max_ending_here, arr[i] * min_ending_here); min_ending_here = min(arr[i], arr[i] * max_ending_here, arr[i] * min_ending_here); max_ending_here = temp; //max_so_far = max(max_so_far, max_ending_here); if(max_ending_here>max_so_far)
        max_so_far = max_ending_here;
    }
    
    printf("Maximum Product of sub-array is %d", max_so_far);
}
Output
Maximum Product of sub-array is 2

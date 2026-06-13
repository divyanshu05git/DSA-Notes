

#Cycle sort

#usecase
-when the numbers are given in the range [1,n]

#key idea
swap index i until it i gets value = i+1

```java
  public static void cyclicSort(int arr[]){
        int n=arr.length;

        //numbers in the range [1,n] so arr[i]==i+1 for the sorted array

        int i=0;
        while(i<n){
            int correctIndex=arr[i]-1;
            if(arr[i]!=arr[correctIndex]){
                swap(arr,i,correctIndex);
            }
            else{
                i++;
            }
        }

  }
```
#Problems

leetcode-41

leetcode-268

leetcode-448

leetcode-287

leetcode-442

leetcode-645

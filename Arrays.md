## Array Operations

### Merge

Merge Two
```java
public class MergeArrays {
    public static void main(String[] args) {
        // Sample arrays
        int[] array1 = {1, 2, 3};
        int[] array2 = {4, 5, 6};

        // Calculate the length of the merged array
        int mergedLength = array1.length + array2.length;

        // Create the merged array
        int[] mergedArray = new int[mergedLength];

        // Copy elements from the first array
        for (int i = 0; i < array1.length; i++) {
            mergedArray[i] = array1[i];
        }

        // Copy elements from the second array
        for (int i = 0; i < array2.length; i++) {
            mergedArray[array1.length + i] = array2[i];
        }

        // Print the merged array
        for (int value: mergedArray) {
            System.out.print(value + " ");
        }
    }
}

```

Merge 2d Array
``` java 
import java.util.Arrays; // only needed for the print out 

public class MergeArrays {
    public static void main(String[] args) {
        // Sample 2D array with arrays to be merged
        int[][] inputArrays = {
                {1, 2, 3},
                {4, 5, 6},
                {7, 8, 9}
        };

        // Calculate the total length of the merged array
        int mergedLength = 0;
        for (int[] array : inputArrays) {
            mergedLength += array.length;
        }

        // Create the merged array
        int[] mergedArray = new int[mergedLength];

        // Copy elements from each array to the merged array
        int index = 0;
        for (int[] array : inputArrays) {
            for (int value : array) {
                mergedArray[index++] = value;
            }
        }

        // Print the merged array
        System.out.println("Merged Array: " + Arrays.toString(mergedArray));
    }
}

```


Merge Two sorted arrays into one sorted array
```Java
public static int[] merge(int[] arr1, int[] arr2) {  
    // TODO  
    int[] result = new int[arr1.length+arr2.length];  
    int i1 = 0;  
    int i2 = 0;  
    int ir = 0;  // index result
  
    while (ir<result.length) {  
       if (i1==arr1.length) {  
          result[ir] = arr2[i2];  
          i2++;  
       } else if (i2==arr2.length) {  
          result[ir] = arr1[i1];  
          i1++;  
       } else {  
          if (arr1[i1] < arr2[i2]) {  
             result[ir] = arr1[i1];  
             i1++;  
          } else {  
             result[ir] = arr2[i2];  
             i2++;  
          }  
       }  
           ir++;  
       }  
    return result;  
}
```



### Index

Get the index of the first occurrence of an element in the array
``` java
    // Get the index of the first occurrence of an element in the array
    public static int indexOf(int[] array, int target) {
        if (array == null) {
            System.out.println("Input array cannot be null.");
            return -1;
        }

        for (int i = 0; i < array.length; i++) {
            if (array[i] == target) {
                return i;
            }
        }

        return -1; // Element not found
    }
```

Count the number of occurrences of an element in the array
```java
    // Count the number of occurrences of an element in the array
    public static int countOccurrences(int[] array, int target) {
        if (array == null) {
            System.out.println("Input array cannot be null.");
            return 0;
        }

        int count = 0;
        for (int value : array) {
            if (value == target) {
                count++;
            }
        }

        return count;
    }

    // Check if an element exists in the array
    public static boolean contains(int[] array, int target) {
        if (array == null) {
            System.out.println("Input array cannot be null.");
            return false;
        }

        for (int value : array) {
            if (value == target) {
                return true;
            }
        }

        return false;
    }

```


### Inverse

Inverse 1d int array
``` java 
public class ArrayReverse {
    public static void reverse(int[] array) {
        if (array == null) {
            System.out.println("Input array cannot be null.");
            return;
        }

        int length = array.length;
        for (int i = 0; i < length / 2; i++) {
            int temp = array[i];
            array[i] = array[length - i - 1];
            array[length - i - 1] = temp;
        }
    }
}

```

### Array list

Init and reverse to array
```java
public static int[] linearize(int[][] a) {  

    List<Integer> result = new ArrayList<>();  
    for (int[] b:a) {  
       for (int c: b) {  
          result.add(c);  
       }  
    }  
  
  
    return result.stream().mapToInt(i -> i).toArray();  
}
```
## Sorts
#### Merge Sort
```Java
public static void mergeSort(int[] array) {  
    int length = array.length;  
    if (length <= 1) return;  
  
    int middle = length/2;  
    int[] leftArray = new int[middle];  
    int[] rightArray = new int[length-middle];  
  
    int j=0;  
  
    for (int i=0; i<length; i++) {  
        if (i<middle) {  
            leftArray[i] = array[i];  
        } else {  
            rightArray[j++] = array[i];  
        }  
    }  
    mergeSort(leftArray);  
    mergeSort(rightArray);  
    merge(leftArray, rightArray, array);  
}  
  
private static void merge(int[] leftArray, int[] rightArray, int[] array) {  
    int leftSize = array.length / 2;  
    int rightSize = array.length-leftSize;  
    int i=0, l=0, r=0;  
  
    while(l<leftSize && r<rightSize) {  
        if (leftArray[l] < rightArray[r]) {  
            array[i++] = leftArray[l++];  
        } else {  
            array[i++] = rightArray[r++];  
        }  
    }  
    while(l<leftSize) {  
        array[i++] = leftArray[l++];  
    }  
    while(r<rightSize) {  
        array[i++] = rightArray[r++];  
    }  
}
```
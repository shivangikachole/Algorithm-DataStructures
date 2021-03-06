### Selection sort

In this assignment, you implement selection sort. A basic definition of this sorting algorithm is given as:

Find the index with the smallest element.
Swap the smallest element with the element of the first index.
Repeat from index plus 1.

See: https://nl.wikipedia.org/wiki/Selection_sort
    
```java
class Solution {
  /**
   * @param elements
   *     Array of integers to be sorted.
   */
  public static void selectionSort(int[] elements) {
    if(elements.length == 0 || elements.length == 1) return;
    
    for(int i = 0; i< elements.length; i++) {
      int small = i;
      for(int j = i+1 ; j<elements.length; j++) {
        if(elements[small] > elements[j])
          small = j;
      }
      
      int temp = elements[i];
      elements[i] = elements[small];
      elements[small] = temp;
    }
  }
}
```

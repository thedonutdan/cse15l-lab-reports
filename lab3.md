# Lab 3 - Bugs and Commands
**Daniel Andrews**  

**Part 1 - Bugs**  
Example of failure-inducing input for the buggy program:  
```
	@Test 
	public void testReverseInPlaceFail() {
    int[] input1 = { 3 , 2, 1 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 1 , 2 , 3 }, input1);
	}
```
Example of non failure-inducing input for the buggy program:  
```
  @Test
  public void testReverseInPlacePass() {
    int[] input1 = { 1 };
     ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 1 }, input1);
  }
```
The result of running the tests showing what symptoms we can see:  
![image1](https://thedonutdan.github.io/cse15l-lab-reports/testresultslab3.png)  
Identifying the bug:  
```
  static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }
```
In it's current iteration this method will replace each element with the element that is equidistant and opposite from the middle index of the array, however it takes no care to preserve the original elements of the array before it overwrites them. This causes the array to be returned with only the elements of the first half mirrored on either side of the middle element.  
Fixing the bug:  
```
  static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length/2; i += 1) {
      int temp = arr[i];
      arr[i] = arr[arr.length - i - 1];
      arr[arr.length - i -1] = temp;
    }
  }
```
Here we have added two lines to the method. The first line creates a temporary variable in which we can store the ith value in the array. Then we can replace the ith element with the element opposite and equidistant from the middle index of the array. Because we have preserved the ith value in the temp variable we can then overwrite the higher indexed value properly. We also have changed the loop to iterate only over the first half of the array as we will swap each element in the first and second half of the array. Note that iterating over the full array would result in the array being reversed twice, returning the original array and causing another bug.  

**Part 2 - Researching Commands**  
For this section of the lab I will be researching the `grep` command using `man grep` and I will show four options that can be used with `grep`. The working directory we will be using is   
`-i`  
```

```

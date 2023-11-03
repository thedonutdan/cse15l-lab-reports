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


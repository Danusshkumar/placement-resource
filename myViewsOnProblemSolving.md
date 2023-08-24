## My views on Problem solving

## Common patterns on Problem solving

## Titbits on problem solving

### Duplicates on Arrays

- Commonly when we have to check duplicates on array with O(n) time complexity, there is one approach that comes to my mind. Using HashSet. By using this, I will solve most of my problems as it has time complexity of O(n) for searching an element
- Previously we used another array for storing frequency based on index or we may use arrays for finding the duplicates
- Now, it's easy to implement HashSet then doing those kinds of things as HashSet did all the work for us. This is the way tp enjoy the features of Powerful programming languages
 like Java.
- But if we wanted to check duplicates withou using extra space, then it's challenging. But we may do that if we have certain constraints. 
- If the array size is n+1 and each element in array will be in the range[1,n], then we can find duplicate elements using pointer-pointed element approach. 
- This is not a name of the approach but it's the name given by me for that approach. pointer (current element) will point to pointed element. If the current element points one element (pointed) and its already visited, then the pointer element(current element) is duplicated. We may mark the pointed element as visited using several techniques based on the constrains such as marking as -ve and adding n to the number etc.
- Explore all duplicates related problems to learn and feel this

## Questions on problem solving

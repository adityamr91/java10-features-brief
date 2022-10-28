# java10-features-brief

1. copyOf()
java.util.List, java.util.Map and java.util.Set each got a new static method copyOf(Collection).

It returns the unmodifiable copy of the given Collection:
```
@Test(expected = UnsupportedOperationException.class)
public void whenModifyCopyOfList_thenThrowsException() {
    List<Integer> copyList = List.copyOf(someIntList);
    copyList.add(4);
}
```
Any attempt to modify such a collection would result in java.lang.UnsupportedOperationExceptionruntime exception.

2. toUnmodifiable*()
java.util.stream.Collectors get additional methods to collect a Stream into unmodifiable List, Map or Set:
```
@Test(expected = UnsupportedOperationException.class)
public void whenModifyToUnmodifiableList_thenThrowsException() {
    List<Integer> evenList = someIntList.stream()
      .filter(i -> i % 2 == 0)
      .collect(Collectors.toUnmodifiableList());
    evenList.add(4);
}
```
Any attempt to modify such a collection would result in java.lang.UnsupportedOperationExceptionruntime exception.


3. Optional*.orElseThrow()
java.util.Optional, java.util.OptionalDouble, java.util.OptionalIntand java.util.OptionalLongeach got a new method orElseThrow()which doesn't take any argument and throws NoSuchElementExceptionif no value is present:
```
@Test
public void whenListContainsInteger_OrElseThrowReturnsInteger() {
    Integer firstEven = someIntList.stream()
      .filter(i -> i % 2 == 0)
      .findFirst()
      .orElseThrow();
    is(firstEven).equals(Integer.valueOf(2));
}
```
It's synonymous with and is now the preferred alternative to the existing get()method.

4. Performance Improvements
Follow the link for an in-depth article on this feature:

Java 10 Performance Improvements

5. Container Awareness
JVMs are now aware of being run in a Docker container and will extract container-specific configuration instead of querying the operating system itself – it applies to data like the number of CPUs and total memory that have been allocated to the container.

# Final Exam

### Release: 8am Wednesday June 9, 2021

### Due: 11:59pm Friday June 11, 2021

This page details a **take-home exam** that you will complete over the next few days. You can't communicate with anyone about the content of the assignment until you receive your grade. The course staff will not give debugging advice or answer questions about the problems. If you have technical trouble creating a screencast (detailed below) feel free to reach out for assistance.

You **can** make use of any course notes, online resources, Java tools, and so on to complete the exam. Feel free to use any built-in Java features and libraries to complete the tasks. Do not copy code from any non-course resources. You **can** copy code that's provided as part of the course or you used on a previous assignment for this course.

The starter code for this exam can be found in this repository

You may find some of the following resources particularly useful:

- [PA7 starter code for reading files](https://github.com/CSE11-SP21-Assignments/cse11-sp21-pa7-starter)
- [PA8 starter code for ```Point``` class with a ```distance``` method](https://github.com/CSE11-SP21-Assignments/cse11-sp21-pa8-starter)

Submission checklist:

- `[ ]` `ClosestPoints.java`
- `[ ]` `ExamplesSearch.java` containing modified `ImageQuery` interface and implementations for several methods
- `[ ]` Video screencast of tracing through a test for the `filter` method submitted to this [Google Form](https://docs.google.com/forms/d/e/1FAIpQLSePnW9JVfpgnD_78fZd7Km2lqPgiATQGiWNVv0RZXSU8l1Zvw/viewform)

## Task 1

In `ClosestPoints.java`, write a class called `ClosestPoints` with a `main` method. The `main` method should expect a single command-line  argument that is the path to a file where each line contains two integers separated by a space. The program should interpret those integers as points, with an x coordinate followed by a y coordinate. The program should print the two points that are _closest_ to one another. You can assume there will be at least two lines in the file, and there is no upper limit on the number of lines in the file. You can also assume that the file given on the command line exists and has the given format (you don't have to check for nonexistent files or badly-formatted numbers, etc).

Closeness is defined by the definition of `distance` we've used previously for `Point`s; you might find previous code from lecture that defines the `Point` class useful (but you don't have to use it). Add any additional classes and methods you need to help you complete the program.

**Example**: The file `points.txt` contains

```
1 1
5 6
1 4
-10 5
0 0
-1 3
```

Your program should behave as follows:

```
$ javac ClosestPoints.java
$ java ClosestPoints points.txt
1 1
0 0
```

The points should be printed in the order they originally appeared in the file. If there's a tie, print any pair of points with that distance.

Make sure to test your solution thoroughly. We will grade your solution automatically with our own tests.

## Task 2

```ExamplesSearch.java``` contains the starter code for image queries that we've used for past exams. This is exactly the same starter code as for previous exams.

Add the following methods to the `ImageQuery` **interface**:

```java
// Returns true if any of the ImageData match this query, false otherwise
// throw an IllegalArgumentException if ids is null
// (You can choose the message in the error)
boolean any(List<ImageData> ids);

// Returns the number of ImageData in the list that match this query
// throw an IllegalArgumentException if ids is null
// (You can choose the message in the error)
int count(List<ImageData> ids);

// Returns a new list containing just the ImageData in the list that match this query
// throw an IllegalArgumentException if ids is null
// (You can choose the message in the error)
List<ImageData> filter(List<ImageData> ids);

/**
 * Returns:
 * - A new list
 * - Containing the first n ImageData in the list:
 *    - in descending order according to the comparator
 *    - that match this query
 * - If there are fewer than n matches, returns just a list of those that match
 *   (in descending order)
 * 
 * Example: The query matches on files with extension png. The comparator
 * compares the area of images. n is 3. Consider images with these properties:
 * 
 * Extension | Width | Height
 * jpg          100     200
 * png          100     200
 * png          500     600
 * jpg         1000     300
 * png          300     200
 * png          300     400
 * 
 * The resulting list should contain the images in this order (the first row is
 * index 0).
 * 
 * Extension | Width | Height
 * png          500     600
 * png          300     400
 * png          300     200
 * 
 * throw an IllegalArgumentException if ids is null, compare is null, or n is less than 0
 * (You can choose the message in the error)
 * 
 * Note that the example above is drawn as a table to make the intended values
 * clear. The method you write should not print these tables and return a list
 * as in examples we've seen before.
*/
List<ImageData> filter(List<ImageData> ids, Comparator<ImageData> compare, int n);
```

Implement these methods for the query classes provided in the file. You should not add previous classes like ```EitherQuery``` or ```AllQuery``` from past exams. Don't make this more complicated than you have to, or write more code than you have to. What techniques do we know for avoiding code duplication across classes?

**Hint**: You will probably want to use the `sort` method that is built in to Java `List`s:

[Java sort method](https://docs.oracle.com/en/java/javase/13/docs/api/java.base/java/util/List.html#sort(java.util.Comparator))

An example of using it is here:

```
import java.util.List;
import java.util.ArrayList;
import java.util.Comparator;

class IntegerCompare implements Comparator<Integer> {
  public int compare(Integer n1, Integer n2) {
    return n1 - n2;
  }
}
class Main {
  public static void main(String[] args) {
    // Construct a new ArrayList with these elements
    List<Integer> nums = new ArrayList<>(List.of(1, 5, -3, 8, -2, 1, 7));
    nums.sort(new IntegerCompare());
    System.out.println(nums); // prints in sorted order
  }
}
```

Make sure to test these methods thoroughly yourself – we will grade them automatically based on our own tests.

### Task 3 – Video

You will record a short video of no more than 5 minutes to [this Google Form](https://docs.google.com/forms/d/e/1FAIpQLScJDNNz-yI25HjdMMPFQ5bfcBsATSsHyU4OXms7wnj93AbPOg/viewform). Include:

- Show only your face and a picture ID (your student ID is preferred) for a few seconds at the beginning. You don't have to be on camera the whole time, though it's fine if you are. Just a brief confirmation that it's you creating the video/doing the work attached to the work itself is what we want.
- Pick a test for your `filter` method that takes a **single** argument with three `ImageData` references in the list.

  Run the `ExamplesSearch` program and show the output corresponding to a method call for this example. Then, starting from the line in your code with the call to the `filter` method, indicate each line of code that runs in your program while evaluating that method call. You can scroll to and click the lines to highlight them, or otherwise indicate each one. You should indicate them in the order that **Java will evaluate them** (this might be different than the order they appear in the file).

An example of what your video should look like when doing this kind of
explanation is here:

[https://drive.google.com/open?id=1E-TcVXSg9BI4MnWoVU9_BbcRJsu8ZhCf](https://drive.google.com/open?id=1E-TcVXSg9BI4MnWoVU9_BbcRJsu8ZhCf)

PA5 has a tutorial for creating a screencast like this [https://github.com/CSE11-SP21-Assignments/cse11-sp21-pa5-starter](https://github.com/CSE11-SP21-Assignments/cse11-sp21-pa5-starter).

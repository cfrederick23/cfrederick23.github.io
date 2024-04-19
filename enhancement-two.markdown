---
layout: default
title: Enhancement Two - Algorithms and Data Structure
---

# Enhancement Two: Algorithms and Data Structure

[Download Enhancement Two](https://drive.google.com/file/d/1HaDTTC-5UzFHW5S0RK5aAPMYYCOFvfys/view?usp=sharing){:target="_blank"}

Reflecting on the progression of the Grazioso Salvare Rescue Animal Management System, this enhancement built upon the foundational software engineering and design improvements made previously, by enhancing the project in the algorithms and data structures category. The aim was to transition the system from a basic to a sophisticated application demonstrating my capabilities in optimizing data retrieval processes using advanced data structures.

## About the Enhancement

The enhancement focused on improving the efficiency of searching for an animal by name within the Grazioso Salvare application. By integrating a hash map, I significantly optimized the search process, reducing the time complexity from O(n) to O(1) for the best-case scenarios.

To demonstrate the improvement, I populated the system with a large number of Dog and Monkey objects using for loops. These objects were added to both an ArrayList and a HashMap for comparison:

```java
// Populating the system with Dog objects
for (int i = 1; i <= 5000000; i++) {
    createDog("Dog" + i, "Great Dane", "male", "5", "20.0", 
              "01/01/2020", "USA", "intake", false, "USA");
}
```

The above loop simulates the addition of millions of Dog objects, each with a unique identifier.

```java
for (int i = 1; i <= 5000000; i++) {
    createMonkey("Monkey" + i, 10.0, 50.0, "Species", "female", 5, 
    20.0, "01/01/2020", "United States", "Fully Trained", false, 
    "United States");
}
```

Similarly, this loop adds a significant number of Monkey objects, ensuring a comprehensive dataset for my search optimization tests.

The original search method used an ArrayList, which required iterating through all elements to find a match:

```java
public static RescueAnimal searchAnimalByNameArrayList(String name) {
    for (RescueAnimal animal : animalArrayList) {
        if (name.equalsIgnoreCase(animal.getName())) {
            return animal;
        }
    }
    return null;
}
```

While functional, the above method is inefficient for large datasets as it performs a linear search.

The new search method leverages a HashMap, providing immediate access to the objects by their names:

```java
public static RescueAnimal searchAnimalByNameHashMap(String name) {
    return animalHashMap.get(name.toLowerCase());
}
```
## Performance Comparison

When it comes to searching through data, the choice of data structure can make a drastic difference in performance. To illustrate this, I compared the search times between using a hash map and an array list.

The search duration for both the hash map and the array list methods was calculated by recording the time immediately before and after each method call, and then determining the difference between these two timestamps.

```java
// Timing search in a hash map
long startTimeHashMap = System.currentTimeMillis();
RescueAnimal foundAnimalHashMap = RescueAnimalFactory
    .searchAnimalByNameHashMap(searchName);
long endTimeHashMap = System.currentTimeMillis();

// Timing search in an array list
long startTimeArrayList = System.currentTimeMillis();
RescueAnimalFactory.searchAnimalByNameArrayList(searchName);
long endTimeArrayList = System.currentTimeMillis();

// Calculate the durations
long durationHashMap = endTimeHashMap - startTimeHashMap;
long durationArrayList = endTimeArrayList - startTimeArrayList;
```

### Results

![Search Performance Result 1](images/Result 1.png "Result 1")

The hash map executed the search instantly, taking 0 milliseconds, whereas the array list took 241 milliseconds for the same operation.

Even when the target animal doesn't exist, the hash map maintains its swift performance:

![Search Performance Result 2](images/Result 2.png "Result 2")

Once again, the hash map search was immediate, showing 0 milliseconds, while the array list search slowed down to 195 milliseconds.

## Additional Enhancements and Outcomes
Further enhancements included updating animal attributes, deleting records, and canceling reservations, which increased the system's administrative versatility. The introduction of specific validation methods like 'validateAge' and 'validateWeight' ensured the accuracy and integrity of the data entered into the system. The change to 'Date' from 'String' for acquisition dates and the revamping of the user interface enhanced navigability and aesthetic appeal.

These enhancements not only improved the system's organization and maintainability but also demonstrated a commitment to best practices in software development. The incorporation of a help/about menu option and the diligent closure of system resources upon application termination highlighted attention to detail and security-minded practices.

Through these enhancements, I directly addressed and fulfilled key program outcomes, notably in designing and evaluating computing solutions with algorithmic principles and developing a security mindset that anticipates adversarial exploits in software architecture.

[Return to Home](/)
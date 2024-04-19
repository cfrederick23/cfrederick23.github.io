---
layout: default
title: Enhancement Two - Algorithms and Data Structure
---

# Enhancement Two: Algorithms and Data Structure

[Download Enhancement Two](https://drive.google.com/file/d/1HaDTTC-5UzFHW5S0RK5aAPMYYCOFvfys/view?usp=sharing){:target="_blank"}

Reflecting on the progression of the Grazioso Salvare Rescue Animal Management System, this enhancement built upon the foundational software engineering and design improvements made previously, by enhancing the project in the algorithms and data structures category. The aim was to transition the system from a basic to a sophisticated application demonstrating my capabilities in optimizing data retrieval processes using advanced data structures.

## About the Enhancement

The most notable improvement in this milestone was the integration of a hash map to optimize the search functionality. This significant adjustment reduced the time complexity of finding an animal from O(n) to O(1) in best-case scenarios, thus making data retrieval more efficient.

To demonstrate the difference in time complexities between a search using a hash map and a search using an array list, the 'initializeAnimals' method within the 'RescueAnimalFactory' class was utilized. Here, for loops were employed to create Dog and Monkey objects, which were then added to both the hash map and the array list. Methods providing search-by-name functionality were then implemented for each list.

Images illustrating the for loops and search implementations:

![For Loop Implementation for Dog](images/For Loop - Dog.png "For Loop - Dog")
![For Loop Implementation for Monkey](images/For Loop - Monkey.png "For Loop - Monkey")
![Array List Search Method](images/ArrayList Search.png "ArrayList Search")
![Hash Map Search Method](images/HashMap Search.png "HashMap Search")

In the 'Driver' class, the 'searchAnimalByName' method calls both the 'searchAnimalByNameHashMap' and 'searchAnimalByNameArrayList' methods from the 'RescueAnimalFactory' class, calculating the duration time for each method call, as shown in the screenshot below:

![Time Capture for Search Methods](images/Time Capture.png "Time Capture")

## Performance Comparison

The difference in performance between each search algorithm is demonstrated in the following screenshots:

![Search Performance Result 1](images/Result 1.png "Result 1")
![Search Performance Result 2](images/Result 2.png "Result 2")

## Additional Enhancements and Outcomes

Further enhancements included updating animal attributes, deleting records, and canceling reservations, which increased the system's administrative versatility. The introduction of specific validation methods like 'validateAge' and 'validateWeight' ensured the accuracy and integrity of the data entered into the system. The change to 'Date' from 'String' for acquisition dates and the revamping of the user interface enhanced navigability and aesthetic appeal.

These enhancements not only improved the system's organization and maintainability but also demonstrated a commitment to best practices in software development. The incorporation of a help/about menu option and the diligent closure of system resources upon application termination highlighted attention to detail and security-minded practices.

Through these enhancements, I directly addressed and fulfilled key program outcomes, notably in designing and evaluating computing solutions with algorithmic principles and developing a security mindset that anticipates adversarial exploits in software architecture.

[Return to Home](/)

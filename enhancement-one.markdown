---
layout: default
title: Enhancement One: Software Engineering and Design
---

# Enhancement One: Software Engineering and Design

[Download Enhancement One](https://drive.google.com/file/d/1WwYssKLHy77b7uCjTqBroRx2x9RuhU_V/view?usp=sharing){:target="_blank"}

As a recap, the chosen artifact for this enhancement was a Java-based console application developed for Grazioso Salvare, initially created during the "Foundation in Application Development" (IT 145) course at SNHU. This project was selected for its potential to be transformed from a basic introductory object-oriented programming model to a sophisticated, scalable, and modular software system. The primary focus of this enhancement was the introduction of the `RescueAnimalFactory` class.

## About the Enhancement

The implementation of the `RescueAnimalFactory` class marked a significant improvement in the software's architecture. By centralizing object instantiation, this factory design pattern enforced the "separation of concerns" principle, crucial for maintaining a clean and manageable codebase. This design choice not only enhanced the modularity of the application but also facilitated future scalability and the integration of new animal types into the system seamlessly.

```java
// Example of centralized object creation in RescueAnimalFactory
public static Dog createDog(String name, String breed, String gender,
        String age, String weight, String acquisitionDate, 
        String acquisitionCountry, String trainingStatus, 
        boolean reserved, String inServiceCountry) {
    Dog dog = new Dog(name, breed, gender, age, weight, 
        acquisitionDate, acquisitionCountry, trainingStatus, 
        reserved, inServiceCountry);
    dogList.add(dog); // Dog ArrayList
    animalList.add(dog); // RescueAnimal ArrayList
    return dog;
}

public static Monkey createMonkey(String name, String tailLength, 
        String height, String bodyLength, String species, 
        String gender, String age, String weight, 
        String acquisitionDate, String acquisitionCountry, 
        String trainingStatus, boolean reserved, 
        String inServiceCountry) {
    Monkey monkey = new Monkey(name, tailLength, height, bodyLength, 
        species, gender, age, weight, acquisitionDate, 
        acquisitionCountry, trainingStatus, reserved, 
        inServiceCountry);
    monkeyList.add(monkey); // Monkey ArrayList
    animalList.add(monkey); // RescueAnimal ArrayList
    return monkey;
}
```

Further strengthening the software's architecture, comprehensive JavaDoc comments were introduced to enhance the clarity and instructional value of the code, aligning with the goal to produce professional-quality communications suitable for diverse audiences. This strategic move improved the overall comprehensibility of the codebase, serving both educational and practical purposes in software development.

Example of a JavaDoc comment:
```java
/**
 * The {@code RescueAnimalFactory} class is responsible for creating 
 * instances of rescue animals and managing the lists of animals 
 * within the rescue system. It provides factory methods to create 
 * new {@link Dog} and {@link Monkey} objects, and also maintains 
 * centralized lists of all animals, dogs, and monkeys for easy 
 * retrieval and management.
 */
```

## Alignment with Course Outcomes

This enhancement directly aligns with several core course outcomes, emphasizing the development of scalable software solutions and delivery of professional-quality communications. The structural innovations implemented in the `RescueAnimalFactory` class demonstrate advanced software engineering techniques and contribute significantly to the development of computing solutions that are valuable, efficient, and tailored to specific industry needs.

Specifically, this project addresses the course outcomes by enhancing collaborative environments through improved code modularity, fostering better teamwork and maintenance capabilities. It also supports the creation of innovative computing techniques by implementing a design pattern that anticipates future system expansions and integration challenges.

## Challenges and Learnings

Integrating the `RescueAnimalFactory` without disrupting existing functionalities presented a moderate challenge. This process required meticulous planning and testing to ensure compatibility and performance. Through this experience, I deepened my understanding of design patterns and their practical applications in enhancing software maintainability and scalability.

Adhering to rigorous documentation standards and employing JavaDoc effectively were key learnings that enhanced my ability to communicate complex technical details clearly. This practice not only facilitated easier code maintenance but also ensured that any programmer could understand and engage with the codebase effectively, highlighting the importance of clear and intentional commenting.

## Skills Demonstrated

Through this enhancement, I demonstrated proficiency in advanced object-oriented programming, application of software design patterns, and effective communication of complex technical details through code documentation. The successful implementation of the `RescueAnimalFactory` class showcases my capability to refactor and improve an existing codebase, enhancing its efficiency, maintainability, and adaptability.

[Return to Home](/)

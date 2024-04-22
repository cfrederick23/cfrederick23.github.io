---
layout: default
title: Enhancement Three - Databases
---

# Enhancement Three: Databases

[Download Enhancement Three](../EnhancementThree.zip)

Building on the solid foundations laid by previous enhancements in software engineering and algorithm optimization, the third enhancement marks a significant leap in the evolution of the Grazioso Salvare Rescue Animal Management System. This phase was dedicated to advancing the system's data management and security capabilities by incorporating a comprehensive SQLite database. The adoption of an SQLite database transformed the application from using transient in-memory storage to employing a persistent and secure data management approach. This was achieved through the design and implementation of a relational database schema that enabled efficient data relationships and transactions. The transformation entailed during this enhancement not only fortified the application's data persistence and integrity but also positioned it to adeptly handle complex data operations, thus paving the way for a future-proof and scalable architecture.

## About the Enhancement

In this third enhancement phase of the Grazioso Salvare Rescue Animal Management System, I focused on significant upgrades including a new system architecture with additional service and data classes, secure password handling using hashing and salting, role-based access controls for improved security, a robust database schema, and secure database operations with Java PreparedStatement. I will detail each of these enhancements in the sections below, explaining their roles in enhancing the system's functionality and security.

### New System Architecture
In addition to the `DatabaseHelper` class, the third enhancement of the Grazioso Salvare Rescue Animal Management System introduced several new service classes and essential data classes. `RescueAnimalService`, `ReservationService`, and `UserService` were added to provide specialized CRUD (Create, Read, Update, Delete) functionalities, establishing a robust interface between the application logic and the database operations. The `User` and `Reservation` classes significantly enhanced user management and booking capabilities, respectively.

**Updated Application Architecture:**  
The image below illustrates the new file structure, showcasing the addition of the `User` and `Reservation` classes, service classes, and the integration of the SQLite database, marking a significant advancement in the system's data management capabilities.  
<<<<<<<< HEAD:enhancement-three.md
![File Structure](/images/File Structure.png "New File Structure")
========
![File Structure](../images/File Structure.png "New File Structure")
>>>>>>>> ab16e54068cbc2837688f5fbc839559531469b64:_tabs/enhancement-three.md

### Secure Password Handling
Security enhancements were crucial in this phase. The system now includes secure user authentication mechanisms that use hashing and salting techniques instead of storing raw password strings, thereby preventing unauthorized access and enhancing data privacy.

**Salt Generation:**  
```java
/**
 * Generates a new salt for use in password hashing. The salt is a randomly
 * generated sequence of bytes.
 * 
 * @return A hexadecimal string representation of the generated salt.
 */
private String generateSalt() {
    SecureRandom random = new SecureRandom();
    byte[] salt = new byte[16];
    random.nextBytes(salt);
    return bytesToHex(salt);
}
```
**Password Hashing:**  
```java
/**
 * Generates a hash from a plaintext password and a salt using SHA-256 hashing
 * algorithm.
 * 
 * @param password The plaintext password to be hashed.
 * @param salt     The salt to be combined with the password before hashing.
 * @return A hexadecimal string representation of the hashed password, or null
 *         if hashing fails.
 */
 private String generateHash(String password, String salt) {
    try {
        MessageDigest md = MessageDigest.getInstance("SHA-256");
        byte[] hashedPassword = md.digest((password + salt).getBytes());
        return bytesToHex(hashedPassword);
    } catch (NoSuchAlgorithmException e) {
        System.out.println("Error generating hash: " + e.getMessage());
        return null;
    }
}
```
**Converting Bytes to Hexadecimal:**
```java
/**
 * Converts an array of bytes to its hexadecimal string representation.
 * 
 * @param bytes The byte array to be converted.
 * @return The hexadecimal string representation of the byte array.
 */
private static String bytesToHex(byte[] bytes) {
    StringBuilder sb = new StringBuilder();
    for (byte b : bytes) {
        sb.append(String.format("%02x", b));
    }
    return sb.toString();
}
```

### Role-Based Access Control
Additionally, role-based user access controls were introduced, providing differentiated admin functionalities that ensure only authorized users can access and modify sensitive data. This role-based security model is critical for maintaining data integrity and confidentiality while allowing flexible user management.

To enforce role-based access controls, the system checks the user's role before allowing access to admin-specific functionalities. This ensures that only users with administrative privileges can perform certain actions, such as managing user accounts or modifying system settings.

**Check if Current User is Admin:**  
```java
/**
 * Checks if the currently logged-in user has administrative privileges. This is
 * determined by evaluating whether the current user object exists and if the
 * user's role is set to 'admin'.
 *
 * @return true if the current user is an admin, false otherwise.
 */
private static boolean isAdmin() {
	return currentUser != null && "admin".equalsIgnoreCase(currentUser.getRole());
}
```

**Handling of Admin Menu Selection:** 
```java
/**
 * Processes the user's selection from the main menu by executing the
 * corresponding functionality. This method acts as a controller, directing the
 * application flow based on the user's choices, which include animal intake,
 * reservation, update, deletion, and viewing reservation details, as well as
 * system administration tasks for authorized users.
 *
 * @param selection The user's menu selection, represented as a string. The
 *                  method handles the selection case insensitively.
 */
private static void processMenuSelection(String selection) {
    switch (selection.toLowerCase()) {
        // Various switch cases
        case "a": // Admin-specific functionality
            if (isAdmin()) {
                adminFunctionality(scanner);
            } else {
                System.out.println("Unauthorized access. This function is reserved for admins.");
            }
            break;
        // Other switch cases
    }
}
```

**Admin Functionality:** 
```java
/**
 * Presents and processes the administrative functionality menu, offering
 * options such as viewing all users, changing user roles, resetting user
 * passwords, and deleting users. This method displays the available
 * administrative options and processes the user's selection by invoking the
 * corresponding method based on their choice. It ensures only valid options are
 * processed, and invalid selections prompt a message before returning to the
 * main menu.
 *
 * @param scanner The {@link Scanner} object for reading user input.
 */
private static void adminFunctionality(Scanner scanner) {
	System.out.println("Admin functionality accessed.");
	System.out.println("1. View All Users");
	System.out.println("2. Change User Role");
	System.out.println("3. Reset User Password");
	System.out.println("4. Delete User");
	String option = promptAndRead(scanner, "Select an option: ");
	if (option == null)
		return;
		switch (option) {
		case "1":
			viewAllUsersAdmin();
			break;
		case "2":
			changeUserRoleAdmin(scanner);
			break;
		case "3":
			resetPasswordAdmin(scanner);
			break;
		case "4":
			deleteUserAdmin(scanner);
		default:
			System.out.println("Invalid option. Returning to main menu.");
			break;
	}
}
```

### Database Schema
Transitioning to a database-focused framework required careful planning and execution, starting with the development of a robust database schema, followed by the creation of Java methods that facilitated direct interactions with the SQLite database. These methods were securely anchored with the use of prepared statements, which offered protection against SQL injection attacks while improving data handling efficiency.

**Database Schema:**
```java
/**
 * Creates the necessary tables in the SQLite database for the application to
 * function properly. This includes tables for rescue animals, dogs, monkeys,
 * users, and reservations. Each table is created only if it does not already
 * exist, ensuring that the application's data structure is correctly
 * initialized without overwriting any existing data.
 * 
 * SQL statements for creating each table are executed in sequence. If any
 * SQLExceptions occur during the execution, their messages are printed to the
 * console.
 */
 public void createTables() {
    String[] sqlStatements = new String[] {
        "CREATE TABLE IF NOT EXISTS RescueAnimal (" +
            "id INTEGER PRIMARY KEY AUTOINCREMENT," +
            "name TEXT NOT NULL," +
            "animalType TEXT NOT NULL," +
            "gender TEXT," +
            "age INTEGER," +
            "weight REAL," +
            "acquisitionDate TEXT," +
            "acquisitionLocation TEXT," +
            "trainingStatus TEXT," +
            "available INTEGER);", // 0 for false, 1 for true

        "CREATE TABLE IF NOT EXISTS Dog (" +
            "animalId INTEGER PRIMARY KEY," +
            "breed TEXT NOT NULL," +
            "FOREIGN KEY (animalId) REFERENCES RescueAnimal (id) ON DELETE CASCADE);",

        "CREATE TABLE IF NOT EXISTS Monkey (" +
            "animalId INTEGER PRIMARY KEY," +
            "tailLength REAL," +
            "height REAL," +
            "species TEXT NOT NULL," +
            "FOREIGN KEY (animalId) REFERENCES RescueAnimal (id) ON DELETE CASCADE);",

        "CREATE TABLE IF NOT EXISTS User (" +
            "userId INTEGER PRIMARY KEY AUTOINCREMENT," +
            "username TEXT NOT NULL UNIQUE," +
            "hashedPassword TEXT NOT NULL," +
            "salt TEXT NOT NULL," +
            "role TEXT);",

        "CREATE TABLE IF NOT EXISTS Reservation (" +
            "reservationId INTEGER PRIMARY KEY AUTOINCREMENT," +
            "animalId INTEGER NOT NULL," +
            "reservedBy TEXT NOT NULL," +
            "serviceDate TEXT," +
            "serviceLocation TEXT," +
            "FOREIGN KEY (animalId) REFERENCES RescueAnimal (id) ON DELETE CASCADE);"
    };

    try (Connection conn = this.connect();
        Statement stmt = conn.createStatement()) {
        for (String sql : sqlStatements) {
            stmt.execute(sql);
        }
    } catch (SQLException e) {
        System.out.println(e.getMessage());
    }
}
```

### Java PreparedStatement
To enhance security and maintain data integrity, the system uses Java `PreparedStatement` for all SQL operations, which helps prevent SQL injection. Below is an example from the `RescueAnimalService` class, where a new rescue animal is added to the database. This method demonstrates setting parameters on a `PreparedStatement` to insert data safely into the database.

**Demonstration of Java PreparedStatement**
```java
/**
 * Adds a new rescue animal to the database. The specific type of animal (e.g.,
 * Dog or Monkey) determines additional attributes to be stored.
 * 
 * @param animal The {@link RescueAnimal} object representing the animal to be
 *               added to the database.
 */
public void addRescueAnimal(RescueAnimal animal) {
    String insertRescueAnimalSQL = "INSERT INTO RescueAnimal (name, animalType, gender, 
        age, weight, acquisitionDate, acquisitionLocation, trainingStatus, available) 
        VALUES (?, ?, ?, ?, ?, ?, ?, ?, ?)";

    // Attempt to establish a connection to the database and add the animal
    try (Connection conn = databaseHelper.connect();
            PreparedStatement pstmt = conn.prepareStatement(insertRescueAnimalSQL,
                    Statement.RETURN_GENERATED_KEYS)) {

        // Set the values for the prepared statement
        pstmt.setString(1, animal.getName());
        pstmt.setString(2, animal.getAnimalType());
        pstmt.setString(3, animal.getGender());
        pstmt.setInt(4, animal.getAge());
        pstmt.setDouble(5, animal.getWeight());
        // Convert Date to String
        SimpleDateFormat sdf = new SimpleDateFormat("MM/dd/yyyy");
        pstmt.setString(6, sdf.format(animal.getAcquisitionDate()));
        pstmt.setString(7, animal.getAcquisitionLocation());
        pstmt.setString(8, animal.getTrainingStatus());
        pstmt.setBoolean(9, animal.getAvailable());

        int affectedRows = pstmt.executeUpdate();

        if (affectedRows > 0) {
            // Retrieve the generated ID
            try (ResultSet rs = pstmt.getGeneratedKeys()) {
                if (rs.next()) {
                    int animalId = rs.getInt(1);
                    if (animal instanceof Dog) {
                        addDog((Dog) animal, animalId);
                    } else if (animal instanceof Monkey) {
                        addMonkey((Monkey) animal, animalId);
                    }
                }
            }
        }

    } catch (SQLException e) {
        System.out.println(e.getMessage());
    }
}
```

## Alignment with Course Outcomes

Enhancement Three of the Grazioso Salvare Rescue Animal Management System aligns closely with core course outcomes by implementing innovative computing techniques and enhancing security measures. The integration of a SQLite database significantly improved data management and scalability, while the use of Java's PreparedStatement ensured data integrity and security against SQL injection. Additionally, sophisticated password handling techniques, including hashing and salting, alongside role-based access controls, advanced the security of the system by mitigating potential vulnerabilities and enhancing user authentication processes.

These improvements demonstrate effective use of innovative techniques that deliver value and achieve industry-specific goals, emphasizing a proactive security mindset within software architecture.

## Challenges and Learnings

Integrating a comprehensive SQLite database into the existing Grazioso Salvare application presented a significant challenge, particularly in ensuring that the new database system interacted seamlessly with the existing codebase without disrupting its functionality. This process involved meticulous attention to database management systems, advanced programming techniques, and security protocols, significantly enhancing my understanding and skills in these areas.

One of the main challenges was maintaining the integrity and security of user data, a crucial aspect given the system's new capabilities for user authentication and role-based functionality. Implementing robust security measures such as password hashing, salting, and the use of prepared statements to prevent SQL injection attacks required a deep dive into secure coding practices, further developing my security mindset.

The learning curve was steep, yet it provided profound insights into the practical application of database management and the importance of security in software development. These experiences not only reinforced my technical skills but also honed my problem-solving capabilities, ensuring I am well-prepared to tackle similar challenges in future projects.

## Skills Demonstrated

Through this enhancement, I demonstrated advanced skills in database management, secure coding practices, and the integration of complex software functionalities. The successful implementation of the SQLite database exemplifies my ability to enhance data persistence and scalability within an application. Utilizing Java's PreparedStatement interface, I showcased my commitment to security by effectively preventing SQL injection attacks, a crucial aspect of secure software development.

Additionally, my proficiency in applying innovative techniques was evident in the way I structured user authentication and role-based access control, which significantly improved the security and functionality of the system. These advancements not only reflect my technical expertise but also emphasize my ability to develop and implement computing solutions that deliver value and accomplish industry-specific goals, ensuring robust security measures within software applications.

This enhancement vividly demonstrates my capability to blend well-founded computing practices with innovative solutions to solve complex challenges, thereby contributing effectively to the field of computer science.

[Return to Home](/)  
[Enhancement One Page](/enhancement-one)  
[Enhancement Two Page](/enhancement-two)   
  
[Download Enhancement Three](../EnhancementThree.zip)
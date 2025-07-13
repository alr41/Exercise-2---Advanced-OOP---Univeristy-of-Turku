# Exercise-2---Advanced-OOP---Univeristy-of-Turku
## 1. Student ID
Student ID: 2406530

## 2. Exercise
In the library's book database, objects of type "**Book**" are stored. Assume that a book has typical fields such as **title, publication year, publisher**, etc.

The library's customers and staff can make queries in the book database to search for specific books. Additionally, the database supports updates to the data by library staff. Why is this? For example, there may have been initial errors in the data, or it might be necessary to remove a book from the collection, mark it as lost, etc.

(In reality, the database would likely be stored on disk and use some type of database engine, but let's assume here that the database is always entirely in the memory of a Java process as simple objects, and the state of the objects is saved back to a file at the end of the day and reloaded into memory at the beginning of the next day. All data processing would thus simply take place with objects in the memory of the Java process.)

**Task**: What principle of data protection would you choose in the case of the **Book** type when you want to serve the two different roles mentioned:

1. A library customer makes a search query and you want to offer the customer a view that only supports reading the books.

2. Library staff want to permanently edit the information of a specific book.

Describe the mechanisms you choose and their consequences for class features, class invariant, and usage. It will suffice to focus mainly on the Book type. For simplicity, we can assume that the database is an array (Book[]) or a list (List<Book>) of books (you can choose either - arrays should be familiar to you from previous courses). You may also implement the program if you wish, but just creating the specifications is enough.

## 3. Answer
In the situation described, the data needs to behave differently depending on the type of user. 

In the first scenario, the user has limited acess and should only be allowed to query and view, without the ability to modify the data.

In the second scenario, the user, as staff of the library, should be able permanently edit the information of a specific book (which means the data cannot be immutable).

In order to achieve this, it is necesary to implement the **encapsulation** principle, which allows the access to the object's internal state to be controlled. For this to work, the class variables need to be set to private and the **get** and **set** methods need to be public.

To apply this concept to the problem in question, two separate classes need to be created. 

For the staff, the class (e.g. "Book") will have both **get** and **set** methods, allowing them to read and write data. However, the set methods must still enforce constraints to preserve the integrity of the information. For this reason, the **class invariant** - a set of rules that ensures the object's state is always valid - is a key point to prevent the staff users from introducing invalid data, such as an empty title or a negative year. 

As for the customers, a read-only interface (e.g. "ReadableBook") can be provided. This interface will expose only the get methods, allowing them to query and view information without any possibility of altering it. Because no changes are permitted through this interface, the class invariant remains fully protected when accessed by customers. Additionally, an interface was chosen instead of creating a separate class to avoid unnecessary duplication of code.

The outlined process ensures that customers can safely query and view the data (due to the public get methods) while being prevented from making any modifications. At the same time, it allows library staff to access and update the data as needed, through the use of both public get and set methods.

## 4. Formal Specification - Book Class
**Purpose**: represents a book in the library system an provides full access (read and write) for staff users.

**Fields (Private)**: 

String title 

int publicationYear

String publisher

**Constructor**: initializes the book with valid, non-empty values, and enforces the class invariant (e.g. title must not be empty, year must be positive.

**Methods**: 

String getTitle()

void setTitle(String title) - validates that the title is non-empty.

int getPublicationYear()

void setPublicationYear(int year) - validates that the year is positive.

String getPublisher()

void setPublisher(String publisher) - validates that the publisher is non-empty.,

**Class invariant**: title must not be null or empty, publication year must be a positive integer and publisher must not be null or empty.

## 4. Formal Specification - ReadableBook Interface
**Purpose**: provides a restricted, read-only view of a book for customer use.

**Fields (Private)**: 

String title 

int publicationYear

String publisher


**Methods**: 

String getTitle()

int getPublicationYear()

String getPublisher()


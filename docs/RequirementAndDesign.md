# LIBRARY  MANAGEMENT SYSTEM SPECIFICATION
## I.	Functional Requirements
The library needs to build an online library management system to support book borrowing and returning, document searching, member management and library operations. The system includes the following main features:
### 1.	Search and view book information
-	Guests and members can browse or search for books by multiple criteria such as title, author, subject, or publication date.
-	The catalog can be sorted in ascending or descending order according to parameters such as book title, year of publication, or number of available copies.
-	The system displays search results including: book title, author, publication year, status (available / borrowed), and storage location.
-	When viewing a specific book, users can see its ISBN, summary description, language, number of pages, and rack position.
-	For instance, if a user searches for the keyword “science”, the system displays all books whose titles or descriptions include “science”. Each book result shows name, author, year, position, and availability status.
### 2.	Register and manage member accounts
-	Users can register for a library account by providing information such as full name, date of birth, gender, address, phone number, email and password.
-	The system checks for duplicate emails, ensures passwords minimum security requirements(at least 6 characters).
-	Upon successful registration, the system creates:
+ A new account record.
+ A Library Card object with attributes: Card Number, Barcode, Issued Date,  Active.
-	Member can log in, log out and manage their personal information at any time.
-	If members forgot their password, they select the “Forgot password” function on the login screen. The system displays a field asking the user to enter their registerd email address.
-	The system verifies the provided email:
+ If the email does not exit, the system shows an error message: “This email is not registerd in the system.”
+ If the email is vaild, the sytem sends a verification code ore a reset link to that email.
-	After verifying seccessfully, the system displays a form that allows the user to enter a new password.
-	Once the user confirms, the system upsdates the password in the database and replaces the old one.
-	Passwords are stored in encrypted form for security.
### 3.	Borrow and return books
-	Only logged-in members can borrow books.
-	The system displays a list of books available for borrowing.
-	When borrowing the system verifies:
+ Whether the book is available.
+ Whether the member has not exceeded the maximum borrowing limit.
-	If valid, the system generates a loan record that includes:
+ Borrower information.
+ List of borrowed Book Items.
+ Borrowing date and expected return date.
-	Upon returning a book:
+ The librarian confirms the return.
+ The system updates the book’s status back to available.
-	If the return is late, the system calculates a fine based on the number of overdue days. Payment can be made through cash, credit card.
### 4.	Manage loan slips and loan history
-	Member can view the list of books they are currently borrowing, the expected return dates, and the history of previous loans.
-	If the book has not been reserved by another user and has not reached the maximum renewal limit, the member can renew the loan.
-	The system updates the due Date and records the renewal history.
-	Librarian can:
+ View the list of loan slips of all members.
+ Update the status(return, overdue).
+ Send reminders to members nearing their due date.
### 5.	Book management(librarian function)
-	Librarians can manage all books in the system by:
+ Add new books to the system(name, author, genre, year of publication, quantity, location).
+ Editing book information when there is a change.
+ Removing books when the book is damaged or unavailable.
-	When removing a book, the system first checks if the book is currently on loan. If yes, deletion is disallowed to maintain date consistency.
-	Librarians can also look up specific books quickly using the barcode, title, or subject.
### 6.	Manage loan and return vouchers(librarian function)
-	Librarians can view and manage all member loans.
-	Create a manual loan voucher when books are borrowed directly at the counter.
-	When members return books, librarians update the corresponding records:
+ Calculates overdue days.
+ Updates the status from “On loan” “Returned”.
+ Applies the “Overdue” label if not returned on time.
-	The system automatically updates book availability and fine calculation in real-time.
### 7.	Notifications and reminders for returned books
-	The system  automatically send notifications to members in specific scenarios:
+ When a borrowed book is nearing its due date.
+ When a book becomes overdue.
+ When a reserved book becomes available.
+ When a reservation is canceled.
-	Notifications are sent either via email or postal mail, depending on member preferences.
-	These notifications help members manage their borrowing activities efficiently and avoid fines.
## II.	Non-functional Requirements
### 1.	Usability
-	The system must be used for its intended purpose.
-	Friendly and easy-to-use system interface.
-	System access should be quickly and easy.
### 2.	Realiability
-	Information on the system must be authentic and trustworthy by users.
-	In case of system downtime, the system must ensure 99,9% recovery within 24 hours.
### 3.	Performance
-	The maximum time allowed for query results to be returned in the system is 10 seconds.
-	The time to process user requests with the system(add, edit, delete…)is 5 seconds.
-	The system load capacity when many people access it must ensure normal operation.
### 4.	Supportibility
-	The system needs to support remote maintenance and updates without shutting down the entire system.
-	Components such as the database, server and user interface must be designed so that they can be maintained independently when needed.
### 5.	Security
-	The stored information must be strictly protected by the system to prevent information leakage to the outside.
-	The system must have data backup to avoid data los in case of problems and be able to restore data faster.
-	User accounts and passwords installed in the system must be highly secure and changed periodically. 
-	Passwords must be encrypted and not allowed to be copies.Authentication is required when accesing data.
### 6.	Design Constraints
-	The Library Management System must be developed using ưeb-based tecnologies(Python, C++…)
-	The system database must use MySQL or PostgreSQL.
-	The design must follow client-server architecture and support at least Google Chrome browsers.
## III.	Use Case Diagram
### 1.	Overview Diagram
#### 1.1.	 List of Actor

| No. | Actor     | Meaning                                                                 |
|------|-----------|-------------------------------------------------------------------------|
| 1 | Guest | Guests and users who have not logged into the system. |
| 2 | Member | Members, users who have an account and have logged into the system. |
| 3 | Librarian | Librarian is a library manager. |
| 4 | System | The system automatically processes notifications, updates, and sends reminders. |
#### 1.2.	List of Use-cases

| No. | Use case | Meaning |
|------|-----------|----------|
| 1 | View catalog | Users view detailed information. |
| 2 | Search catalog | Users browse the overall catalog. |
| 3 | Register | A new user creates an account in the library system. |
| 4 | Renew book | Users extend the borrowing period of a book if it has not been reserved by another user. |
| 5 | Reserve book | Users reserve a book that is currently borrowed by someone else. |
| 6 | Return book | Used to return borrowed books to the library once the borrowing period ends. |
| 7 | Check out book | The librarian lends a book to a registered member. |
| 8 | Issue book | The process of issuing or approving a borrowing request after verifying book availability and member status. |
| 9 | Update book | The librarian maintains the book database. |
| 10 | Manage member | Enables the librarian to manage all member records. |
| 11 | Send Overdue Notification | Automatically notifies members who have not returned borrowed books by the due date. |
| 12 | Send Reservation Available Notification | When a reserved book becomes available, the system sends a notification to the member who placed the reservation. |
| 13 | Send Reservation Canceled Notification | Notifies members when a book reservation is canceled—either by the user, librarian, or system. |


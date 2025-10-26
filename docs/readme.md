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

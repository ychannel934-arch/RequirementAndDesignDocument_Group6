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
- System architecture diagrams and conceptual models must be designed using draw.io to ensure standardized and easily maintainable visual representations.
-	The Library Management System must be developed using web-based tecnologies(Python, C++…)
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
### 2. Use-case: View Catalog

#### 2.1. Summary
This use case allows a user (Guest or Member) to view detailed information about a selected book from the catalog.

#### 2.2. Flow of Events

##### 2.2.1. Main Flow
- The use case begins when the user selects a book from the search results or catalog list.  
- The system retrieves detailed information of the selected book.  
- The system displays book details including title, author, subject, publication date, ISBN, status (available or borrowed), and description.

##### 2.2.2. Alternative Flows
- **Book Not Found:**  
  If the selected book record no longer exists in the system, the system displays a message indicating the book is unavailable.

#### 2.3. Special Requirements
- The book information must be accurate and synchronized with the database.  
- The page must load within 2 seconds.

#### 2.4. Preconditions
- The user has performed a search or accessed the book list.  
- The selected book exists in the system.

#### 2.5. Postconditions
- The book details are displayed on screen.

#### 2.6. Extension Points
- None.
### 3. Use-case: Search Catalog

#### 3.1. Summary
Allows a user (Guest or Member) to search for books in the catalog by title, author, subject, or publication date.

#### 3.2. Flow of Events

##### 3.2.1 Main Flow
- The user selects the search option.
- The system displays the search interface.
- The user enters search criteria or keywords.
- The system retrieves and displays matching books.
- The user can refine the search using advanced filters.

##### 3.2.2 Alternative Flow
- **No Results Found:** The system notifies the user and suggests trying different keywords.

#### 3.3. Special Requirements
- Supports partial keyword matching and is case-insensitive.  
- Results must load within 3 seconds.

#### 3.4. Preconditions
- The system is connected to the library database.

#### 3.5. Postconditions
- A list of books matching the criteria is displayed.

#### 3.6. Extension Points
- Search by title, author, subject, or publication date.
### 4. Use-case: Register
#### 4.1. Summary
This use case allows a guest to register for a membership account in the library system.
#### 4.2. Flow of Events
##### 4.2.1. Main Flow
The use case begins when a guest selects the option to register for a new account.
1.	The system displays a registration form.
2.	The guest enters required information such as full name, email, password, and contact details.
3.	The system validates the entered information.
4.	The system creates a new member account and confirms successful registration.
##### 4.2.2. Alternative Flows
•	Invalid Information:
If any field is missing or invalid, the system highlights the error and requests correction.
#### 4.3. Special Requirements
•	Password must meet security requirements (minimum length, character type).
•	Email must be unique in the system.
#### 4.4. Preconditions
•	The user is not logged in (guest).
#### 4.5. Postconditions
•	A new member account is successfully created and stored in the database.
#### 4.6. Extension Points
•	None
### 5. Use-case: Reserve Book
#### 5.1. Summary
This use case allows a member to reserve a book that is currently unavailable.
#### 5.2. Flow of Events
##### 5.2.1. Main Flow
The use case begins when a member selects an unavailable book and chooses to make a reservation.
1.	The system checks the book’s availability status.
2.	The system allows the member to confirm a reservation request.
3.	The system records the reservation in the database and displays a confirmation message.
##### 5.2.2. Alternative Flows
•	Book Available:
If the book is currently available, the system suggests the member to check out the book instead of reserving it.
#### 5.3. Special Requirements
•	A member can only reserve a limited number of books at a time.
•	Reservations expire after a specific period.
#### 5.4. Preconditions
•	The user is logged in as a member.
•	The selected book is unavailable (already checked out).
#### 5.5. Postconditions
•	The reservation information is stored in the system.
#### 5.6. Extension Points
•	None
### 6. Use-case: Renew Book
#### 6.1. Summary
This use case allows a member to renew a borrowed book to extend the borrowing period, provided the book has not been reserved by another member and has not exceeded the allowed renewal limit.
#### 6.2. Flow of Events
##### 6.2.1. Main Flow
The use case begins when a member selects the option to renew a borrowed book.
1.	The system displays a list of books currently borrowed by the member.
2.	The member selects the book they wish to renew.
3.	The system checks whether the book is reserved by another member and verifies that the renewal limit (2 times) has not been exceeded.
4.	The system updates the due date and confirms successful renewal.
##### 6.2.2. Alternative Flows
•	Renewal Not Allowed:
If the book has been reserved by another member or has reached the renewal limit, the system notifies the member that renewal is not permitted.
#### 6.3. Special Requirements
•	The new due date must follow library policy.
•	Renewal actions must be logged for tracking.
#### 6.4. Preconditions
•	The user is logged in as a member.
•	The selected book is currently borrowed by the member.
#### 6.5. Postconditions
•	The borrowing record is updated with a new due date.
#### 6.6. Extension Points
•	None.
### 7. Use-case: Return Book
#### 7.1. Summary
This use case allows a member to return a borrowed book to the library.
#### 7.2. Flow of Events
##### 7.2.1. Main Flow
The use case begins when a member selects the option to return a borrowed book.
1.	The system displays a list of books currently borrowed by the member.
2.	The member selects the book to return.
3.	The system updates the book’s status to “available” and records the return date.
4.	The system confirms the successful return.
##### 7.2.2. Alternative Flows
•	Overdue Book:
If the book is overdue, the system extends to the “Pay fine” use case.
#### 7.3. Special Requirements
•	The system must update the inventory in real time.
#### 7.4. Preconditions
•	The user is logged in as a member.
•	The book is currently checked out by the member.
#### 7.5. Postconditions
•	The book is marked as available in the system.
•	The borrowing record is updated.
#### 7.6. Extension Points
•	Pay fine – If the book is returned after the due date.
### 8. Use-case: Check out Book
#### 8.1. Summary
This use case allows a librarian to issue a book to a member for borrowing.
#### 8.2. Flow of Events
##### 8.2.1. Main Flow
The use case begins when a librarian selects the “Check out Book” option.
1.	The librarian enters the member’s ID and book ID.
2.	The system verifies the member’s eligibility and book availability.
3.	The system records the issue date and due date.
4.	The system confirms successful checkout.
##### 8.2.2. Alternative Flows
•	Member Has Overdue Books:
The system notifies the librarian and prevents new checkouts until overdue items are returned.
•	Book Unavailable:
If the book is already issued or reserved, the system disallows the operation.
#### 8.3. Special Requirements
•	Each book must have a unique ID.
•	The due date should be calculated automatically based on library policy.
#### 8.4. Preconditions
•	The user is logged in as a librarian.
•	The book is available in the library.
#### 8.5. Postconditions
•	The book is marked as checked out and associated with the member’s record.
#### 8.6. Extension Points
•	Remove reservation – If the book was previously reserved by the same member.
### 9. Use-case: Issue Book
#### 9.1. Summary
This use case allows a librarian to issue a book to a member who wants to borrow it.
#### 9.2. Flow of Events
##### 9.2.1. Main Flow
The use case begins when a librarian selects the Issue Book option from the system menu.
1.	The librarian searches for a member and selects the desired member record.
2.	The librarian searches for the book to be issued and selects it from the list.
3.	The system checks the book’s availability status. If the book is available, the librarian confirms the issuance.
4.	The system records the book issuance details in the database and updates the book’s status to “Checked Out”. 
5.	The system displays a confirmation message including the due date.
##### 9.2.2. Alternative Flows
•	Book Unavailable:
If the selected book is already checked out or reserved by another member, the system notifies the librarian and cancels the issuance process.
•	Member Has Outstanding Fines:
If the member has unpaid fines or has reached the maximum borrowing limit, the system alerts the librarian and prevents the issuance until the issue is resolved.
#### 9.3. Special Requirements
•	Only authorized librarians can issue books.
•	The system must validate the member’s borrowing limit and fine status before issuing.
•	The due date for return is calculated automatically based on library policy.
#### 9.4. Preconditions
•	The librarian is logged into the system.
•	The member’s account is active.
•	The selected book is available for borrowing.
#### 9.5. Postconditions
•	The book’s status is updated to “Checked Out.”
•	The issuance record is stored in the system.
•	The member’s borrowing list is updated.
#### 9.6. Extension Points
•	None.
### 10. Use-case: Update Book
#### 10.1. Summary
This use case allows a librarian to modify information about an existing book in the library’s catalog.
#### 10.2. Flow of Events
##### 10.2.1. Main Flow
The use case begins when a librarian selects the “Update Book” option.
1.	The system displays a list of all books or allows the librarian to search for a specific book.
2.	The librarian selects the book to update.
3.	The system displays the book’s current details.
4.	The librarian edits the desired information and submits the update.
5.	The system validates the input and updates the record in the database.
6.	The system confirms successful update.
##### 10.2.2. Alternative Flows
•	Invalid Information:
If the updated information is invalid (e.g., missing fields, wrong data format), the system requests correction.
#### 10.3. Special Requirements
•	Only librarians can update book data.
•	Data validation must ensure consistency with catalog rules.
#### 10.4. Preconditions
•	The user is logged in as a librarian.
•	The selected book exists in the catalog.
#### 10.5. Postconditions
•	The book record in the database is updated.
#### 10.6. Extension Points
•	Add book – If the book does not exist, the librarian can add a new one.
•	Edit book – The librarian modifies details of an existing book.
•	Remove book – The librarian deletes a book record from the catalog.
### 11. Use-case: Manage Member
#### 11.1. Summary
This use case allows a librarian to manage member accounts, including viewing, updating, or canceling memberships.
11.2. Flow of Events
##### 11.2.1. Main Flow
The use case begins when a librarian selects the “Manage Member” option.
1.	The system displays the list of registered members.
2.	The librarian selects a member to manage.
3.	The system displays the member’s information and available management options.
4.	The librarian performs the desired action (update or cancel membership).
5.	The system updates the member record accordingly.
##### 11.2.2. Alternative Flows
•	Member Not Found:
If the entered member ID does not exist, the system notifies the librarian.
11.3. Special Requirements
•	Only authorized librarians can access and modify member information.
11.4. Preconditions
•	The librarian is logged into the system.
11.5. Postconditions
•	Member information is updated or deactivated as required.
11.6. Extension Points
•	Update member – To change member details.
•	Cancel membership – To deactivate a member account.

12. Use-case: Send Overdue Notification
12.1. Summary
This use case allows the system to automatically notify members when borrowed books are overdue.
12.2. Flow of Events
##### 12.2.1. Main Flow
The use case begins automatically when the system detects that one or more borrowed books have passed their due date.
1.	The use case is triggered automatically by the system’s scheduler.
2.	The system checks all borrowing records for overdue books.
3.	The system identifies members with overdue books.
4.	The system sends overdue notifications via email or internal messages.
##### 12.2.2. Alternative Flows
•	Notification Delivery Failure:
If an email fails to send, the system logs the error for review.
#### 12.3. Special Requirements
•	The system must run the overdue check daily at a specified time.
#### 12.4. Preconditions
•	Borrowing records exist in the system.
#### 12.5. Postconditions
•	Members with overdue books are notified.
#### 12.6. Extension Points
•	None.

### 13. Use-case: Send Reservation Available Notification
#### 13.1. Summary
This use case allows the system to notify a member when a reserved book becomes available for borrowing.
#### 13.2. Flow of Events
##### 13.2.1. Main Flow
The use case begins when a reserved book is returned and becomes available.
1.	The system detects that the reserved book’s status has changed to “Available.”
2.	The system identifies the first member in the reservation queue for the book.
3.	The system automatically generates a notification message (email or system alert).
4.	The system sends the notification to the corresponding member, informing them that the reserved book is now available for borrowing.
5.	The system records the notification event in the system logs.
##### 13.2.2. Alternative Flows
•	None.
#### 13.3. Special Requirements
•	The system must ensure notifications are sent promptly upon book availability.
•	The notification message must include book details and the reservation expiry date.
#### 13.4. Preconditions
•	The reserved book has been returned and marked as available.
•	The member has an active reservation for the book.
#### 13.5. Postconditions
•	The member receives a notification.
•	The system logs the notification event.
#### 13.6. Extension Points
•	None.

### 14. Use-case: Send Reservation Canceled Notification
#### 14.1. Summary
This use case allows the system to notify a member when their book reservation is canceled, either automatically by the system or manually by the user.
#### 14.2. Flow of Events
##### 14.2.1. Main Flow
The use case begins when a reservation is canceled.
1.	The system detects that a reservation has been canceled (due to expiry, system action, or user request).
2.	The system retrieves the member’s contact information.
3.	The system generates a cancellation notification message including the book title and reason for cancellation.
4.	The system sends the notification to the member via email or system message.
5.	The system records the notification event in the system logs.
##### 14.2.2. Alternative Flows
•	None.
#### 14.3. Special Requirements
•	The system must ensure accurate and timely delivery of cancellation notifications.
•	The notification must clearly state the reason for cancellation (e.g., expired reservation, manual cancellation).
#### 14.4. Preconditions
•	A reservation exists and has been canceled.
•	The member’s contact information is available.
#### 14.5. Postconditions
•	The member is informed that their reservation has been canceled.
•	The system logs the notification activity.
#### 14.6. Extension Points
•	None.
## IV. Class Diagram
## V. Data Model
## VI: Data Flow Diagram:
### 1. DFD-Level 0
### 2. DFD-Level 1


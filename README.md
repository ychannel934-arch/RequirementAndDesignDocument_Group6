# RequirementAndDesignDocument_Group6
Use Case Specification — Library Management System
Use Case 1: View catalog
•	Actors: Guest, Member
•	Stakeholders & Interests: Users want to browse books by category, author, or year.
•	Preconditions: Catalog data exists.
•	Postconditions: User sees a filtered/sorted list of books.
•	Main Flow:
1.	User selects browsing criteria (genre, author, year, or all).
2.	System retrieves matching records.
3.	System displays a paginated list with summary info (title, author, year, status, shelf location).
•	Alternative Flows: No results → display "No results found" and suggest related categories.
•	Business Rules: Sorting can be ascending/descending by title, year, or quantity.

Use Case 2: Search catalog
•	Actors: Guest, Member
•	Stakeholders & Interests: Users want fast, accurate keyword search.
•	Preconditions: Catalog indexed for search.
•	Postconditions: Search results shown.
•	Main Flow:
1.	User enters keyword(s) (title, author, ISBN, or keywords in description).
2.	System runs search and ranks results.
3.	System returns results with detail (title, book code/ID, author, genre, year, status, number of loans).
•	Alternative Flows: Spell-correction or suggestions when no exact match. Show "Did you mean...".
•	Business Rules: Search should support partial matches and boolean operators (optional).

Use Case 3: Register
•	Actors: Guest
•	Stakeholders & Interests: New users want a valid account to borrow books.
•	Preconditions: Email / identity not already registered.
•	Postconditions: Account created and persisted securely.
•	Main Flow:
1.	Guest opens registration form and supplies required data (full name, DOB, gender, address, phone, email, password).
2.	System validates input (required fields, email format, password length >= 6).
3.	System checks for duplicate email.
4.	System saves member record with encrypted password and initial membership state.
5.	System sends confirmation email (optional activation link).
•	Alternative Flows: Duplicate email → report error and ask to login or reset password.
•	Business Rules: Passwords stored with strong hashing (bcrypt/argon2). Email verification recommended.

Use Case 4: Renew book
•	Actors: Member
•	Stakeholders & Interests: Members want to extend loan period when eligible.
•	Preconditions: Member has an active loan for the book; renewal count < allowed limit; book not reserved.
•	Postconditions: Loan due date updated; renewal count incremented; history updated.
•	Main Flow:
1.	Member views current loans and selects a book to renew.
2.	System checks eligibility: reservations, renewal count, outstanding fines.
3.	If eligible, system extends due date by configured period and persists renewal record.
4.	System displays confirmation with new due date.
•	Alternative Flows: If not eligible → display reason (reserved, max renewals reached, unpaid fines).
•	Business Rules: Maximum renewals set to 2. Renewal period configurable (e.g., 2 weeks).

Use Case 5: Reserve book
•	Actors: Member
•	Stakeholders & Interests: Members want to reserve currently unavailable titles.
•	Preconditions: Book is currently on loan or all copies are borrowed.
•	Postconditions: Reservation record created and queued.
•	Main Flow:
1.	Member selects "Reserve" on a book detail page.
2.	System verifies that the book is reservable (not already reserved by same user, within reservation policy).
3.	System creates reservation with timestamp and status "Waiting".
4.	If copy becomes available, system notifies next eligible member.
•	Alternative Flows: If reservation limit reached → inform user.
•	Business Rules: Reservation TTL (time-to-live) after notification (e.g., 48 hours to pick up) before reservation passes to next user.

Use Case 6: Return book
•	Actors: Member, Librarian
•	Stakeholders & Interests: Members return books; library updates inventory and fines.
•	Preconditions: Book currently loaned under a LoanSlip.
•	Postconditions: LoanSlip updated, book status set to available, overdue days calculated.
•	Main Flow:
1.	Member or librarian initiates return (via user interface or scanning barcode at counter).
2.	System locates the LoanSlip by book copy ID and member.
3.	System records returnDate and computes overdue days (if returnDate > dueDate).
4.	System updates Book.quantity and Book.status and LoanSlip.status.
5.	If overdue, system records fine and optionally notifies member.
•	Alternative Flows: Damaged/lost book → librarian records loss/damage and triggers replacement/fine workflow.
•	Business Rules: Late penalty rules configurable (per day or fixed tiers).

Use Case 7: Check out book (Counter checkout)
•	Actors: Librarian
•	Stakeholders & Interests: Librarian processes in-person borrow transactions.
•	Preconditions: Member account valid; book available.
•	Postconditions: LoanSlip created and book marked as borrowed.
•	Main Flow:
1.	Member presents library card or member ID to librarian.
2.	Librarian scans barcode(s) or searches book(s) and verifies availability.
3.	Librarian verifies member eligibility (no account blocks, fines, within limit).
4.	Librarian creates LoanSlip in system (manual entry or scanned items).
5.	System assigns due date and updates inventory/status.
6.	System prints or sends loan confirmation to member.
•	Alternative Flows: Member has outstanding fines or account restriction → librarian refuses checkout and prompts for payment/clearance.

Use Case 8: Issue book (Process a borrowing request)
•	Actors: Librarian, System
•	Stakeholders & Interests: Process reservations or online borrow requests.
•	Preconditions: Member requested a borrow or reservation; book status verified.
•	Postconditions: Loan is confirmed and LoanSlip created, or request rejected.
•	Main Flow:
1.	System receives borrow request (online) or librarian receives request (phone/email).
2.	System/librarian validates member credentials and request rules.
3.	If book available and member eligible, create LoanSlip and mark book as borrowed.
4.	Notify member with loan details.
•	Alternative Flows: If book not available → place reservation or inform member.

Use Case 9: Update book
•	Actors: Librarian
•	Stakeholders & Interests: Maintain accurate book metadata and stock.
•	Preconditions: Librarian authenticated and authorized.
•	Postconditions: Book metadata or inventory updated.
•	Main Flow:
1.	Librarian searches for the book.
2.	Librarian edits fields (title, author, genre, year, quantity, location, barcode).
3.	System validates input and updates the book record.
•	Alternative Flows: Attempt to delete a book currently on loan → system blocks deletion and reports active loans.

Use Case 10: Manage member
•	Actors: Librarian
•	Stakeholders & Interests: Keep member records accurate and handle administrative events.
•	Preconditions: Librarian authenticated.
•	Postconditions: Member records changed or administrative action recorded.
•	Main Flow:
1.	Librarian searches for or selects a member account.
2.	Librarian updates personal details, membership status, or blocks/unblocks account.
3.	System persists changes and logs the action.
•	Alternative Flows: Create member on behalf of guest (manual registration), or delete member (only allowed if no active loans/reservations).

Use Case 11: Send Overdue Notification
•	Actors: System
•	Stakeholders & Interests: Remind members to return overdue items.
•	Preconditions: Scheduled job or trigger checks for loans past dueDate.
•	Postconditions: Notifications queued/sent; member notified via email or UI alerts.
•	Main Flow:
1.	System job queries LoanSlips with dueDate <= today and status = OnLoan.
2.	Fo
Use Case 12: Send Reservation Available Notification
Description: When a reserved book becomes available (because another member returned it), the system automatically notifies the member who made the reservation.
Actors:
•	System
•	Member
Main Flow:
1.	A book previously reserved by Member A is returned to the library.
2.	The system detects that the returned book matches an existing reservation.
3.	The system retrieves the reservation details (member info, book info).
4.	The system generates a notification message.
5.	The system sends the “Reservation Available” notification to the member (email or on-screen).
6.	The member receives and reads the notification.

Use Case 13: Send Reservation Canceled Notification
Description: When a reservation is canceled (by member, librarian, or system), the system notifies the member who made the reservation.
Actors:
•	Member (who cancels or is notified)
•	Librarian (may cancel)
•	System
Main Flow:
1.	Member or Librarian cancels a reservation.
2.	The system verifies cancellation validity.
3.	The system updates reservation status → “Canceled.”
4.	The system generates a “Reservation Canceled” notification.
5.	The system sends notification to the member (email or app interface).
6.	The member receives and reads the notification.

Class Diagram Specification — Library Management System
1. Class: Book
Description:
Represents a book in the library catalog.
Attributes:
Name	Type	Visibility	Description
bookID	String	Private	Unique identifier of the book
title	String	Private	Title of the book
author	String	Private	Author name
publisher	String	Private 	Publisher name
genre	String	Private	Category/ genre of the book
year	int	Private	Year of publication
status	String	Private	Status (Avaliabke / Borrowed / Reserved )
Methods:
Name	Return Type	Description
getBookInfro()	void	Displays detailed book infomation
updateStatus (status)	void	Updates current status of book 
isAvailable	boolean	Check if book is available for borrowing
Relationships:
-	1 Book -> * Loan (one-to-many)
-	1 Book -> *Reservation (one-to-many)
2.	Class: Member
Description: Represent a registered library membber.
Attributes:
Name	Type	Visibility	Description
memberID	String	Private	Unique ID of the member
name	String	Private	Full name
email	String	Private	Email address
password	String	Private	Encrypted password
phone	String	Private	Contact number
address	String	Private	Members address
status	String	Private	Active/ Inactive

Methods: 
Name	Return Type	Description
register()	boolean	Creates a new member account
login(email, password)	boolean	Validates login credentials
updateProfile()	void	Update member personal data
Relationship:
-	1 Member -> * Loan
-	1 Member -> * Reservation
3.	Class: Librarian
Description: 
Represent the administrator managing the library system. 
Attribbutes:
Name	Type	Visibility	Description
librarianID	STring	Private	Unique identifier
name	String	Private	Librarian full name
email	String	Private	Login email
password	String	Private	Encrypted password
Methods
Name	Return Type	Description
addBook (book)	void	Add a new book to the catalog
updateBook (book)	void	Updates book details
deleteBook (bookID)	void	Removes book record
issueBook (member, book)	void	Issues a book to a member
receiveBook (bookID)	void	Marks book as returned
Relationships: 
-	1 Librarian -> * Book 
-	1 Librarian -> * Loan
4.	Class: Loan
Description: Represents a record of a book being borrowed by a member.
Attributes: 
Name	Type 	Visibility	Description
loanID	String	Private	Loan record ID
borrowDate	Date	Private	Date when borrowed
dueDate	Date	Private	Expected return date
returnDate	Date	Private	Actual date returned
fine	Double	Private	Fine for late returns

Methods: 
Name	Return Type	Description
calculateFine()	double	Calculates fine based on overdue days
renewLoan()	void	Extends due date
closeLoan()	void	Marks loan as completed
Relationships:
-	Each Loan links one Member and one Book (Many-to-One both sides)
5. Class: Reservation
Description: Represents a reservation made by a member for a book.
Attributes:

Name	Type	Visibility	Description
reservationID	String	Private	Unique ID
reservationDate	Date	Private	Date of reservation
status	String	Private	Active / Canceled / Completed
Methods:
Name	Return Type	Description
createReservation()	void	Adds a reservation record
cancelReservation()	void	Cancels the reservation
notifyMember()	void	Sends notification when available
Relationships:
-	1 Reservation → 1 Member
-	1 Reservation → 1 Book
6. Class: Notification
Description: 
Handles automated messages to users regarding due dates, returns, or reservations.
Attributes:
Name	Type	Visibility	Description
notificationID	String	Private	Unique ID
type	String	Private	Type (Overdue, ReservationAvailable, Cancellation)
content	String	Private	Message body
sentDate	Date	Private	Date sent
Methods: 
Name	Return Type	Description 
sendNotification()	void	Sends the notification to member
generateMessage()	String	Creates message content dynamically
Relationships:
-	1 Notification → 1 Member
7. Class: System
Description: Represents the overall control and interaction manager for all subsystems.
Attributes:
Name	Type	Visibility	Description
systemName	String	Private	System name
currentDate	Date	Private	System name
Methods: 
Name	Return Type	Description
login(user)	boolean	Authenticates use(member/librarian)
sendOverdueNotifications()	void	Automatically sends reminders
sendReservationNotifications()	void	Sends alerts for available books
Relationships Summary
Class 1	Relationship 	Class 2 	Type
Member	borrows	Book	Association
Librarian	manages	Book	Association
Member	makes	Reservation	Association
Reservation	refers to	Book	Association
Loan	links	Member & Book	Association
System	triggers	Notification	Dependency


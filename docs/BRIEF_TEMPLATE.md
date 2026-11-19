# Project Brief: FindIt – Campus Lost & Found Management System

## What we want

FindIt is a campus lost-and-found web application that helps students report lost belongings, report found items, search listings, and submit ownership claims. It provides administrators with the ability to review claims, approve or reject them, and update item statuses when belongings are returned. The main goal is to make recovering lost belongings on campus easier and more organized.

## Users

- **Students:** Use a web browser on a computer or mobile device to register, log in, report lost and found items, search listings, submit claims, and track claim status.
- **Administrators:** Use the web application to review ownership claims, approve or reject claims, and mark items as returned.
- **Campus staff:** May assist with managing lost-and-found records and item handling.

Anyone can browse available listings. Reporting and claiming require a student account.

Accessibility: The application should provide understandable navigation, readable pages, and clear form validation messages. Specific accessibility standards are TODO.

## Must do   (numbered; each one testable)

1. **User registration and authentication:** Allow students to register, log in, and log out using their accounts. Passwords must be securely hashed.

2. **Report lost items:** Allow authenticated students to report lost items with item name, category, description, date, and location. Save valid reports in SQLite.

3. **Report found items:** Allow authenticated students to submit found-item reports with the required details and display them in the found-items listing.

4. **Search and filter:** Allow users to search and filter listings by keyword, category, location, date, and report type.

5. **Submit ownership claims:** Allow authenticated students to submit claims for open found items with an ownership message. Prevent users from claiming their own reported items and prevent duplicate claims from the same student for the same item.

6. **Administrator claim management:** Allow authenticated administrators to review pending claims and approve or reject them. Approval changes the item status to Claimed; rejection leaves the item status unchanged.

7. **Track item status and returns:** Allow students to view their claim status. Allow administrators to mark an item as Returned after pickup. Returned items must not receive additional claims.

8. **Input validation and security:** Validate submitted information, protect POST requests using CSRF tokens, hash passwords, and restrict administrator functionality to authorized administrators.

## Should do   (if time allows)

- Add email notifications for claim approval and rejection.
- Support image uploads for lost and found items.
- Improve search and matching functionality.
- Improve mobile-friendly interface design.
- Support multiple campus locations.
- Improve authentication and role management.

## Constraints

- **Platform / technology:** Python Flask backend, HTML templates, CSS, JavaScript, and SQLite database. Use the existing Flask application structure with separate routes, models, database operations, templates, and tests.

- **Data:** Store user accounts, item reports, and claims in SQLite. Passwords must be stored as secure hashes. User information and account credentials must not be exposed to unauthorized users. Database records must maintain consistency.

- **Cost:** No external AI model or paid AI service is used at runtime. Runtime AI cost per use: $0.

- **Accessibility / privacy / legal:** Provide clear navigation and form validation. Protect user credentials, use CSRF protection, and restrict administrator access. Do not expose confidential user information.

## Out of scope (so nobody builds it by accident)

- Real-time GPS tracking.
- Online payment functionality.
- AI-based image recognition.
- Runtime AI-based item matching.
- Live chat.
- Separate native mobile application.
- External email notification service in the initial version.

## Quality expectations

- Keep business logic separate from HTML presentation.
- Organize the application using Flask routes, models, and database operations.
- Use SQLite for persistent application data.
- Validate user inputs before storing records.
- Use Werkzeug for password hashing and security utilities.
- Protect administrator functions and POST requests.
- Maintain automated tests using pytest.
- The project includes 15 automated test cases across five test files.
- Keep the main GitHub branch stable and review code changes before merging.
- Ensure item and claim status transitions follow the defined business rules.

## Acceptance criteria

1. **Item reporting:** Register and log in as a student, submit a valid lost or found item report, and verify that it is stored in SQLite and displayed in the appropriate listing.

2. **Search and filtering:** Search using different keywords, categories, locations, dates, and report types. Verify that matching items are displayed.

3. **Claim management:** Submit a claim for an open found item. Verify that its initial status is Pending. Log in as an administrator, approve or reject the claim, and verify the resulting claim and item statuses.

4. **Return process:** Approve a claim, mark the item as Returned after pickup, and verify that another student cannot submit a claim for that returned item.

5. **Security:** Attempt to access administrator functionality without administrator authentication and submit invalid form information. Verify that unauthorized access is denied and invalid information is rejected.

## Open questions

- What measurable response-time target should be used for search?
- Should students receive email notifications when claims are approved or rejected?
- Should item images be supported in a future version?
- How long should returned or unclaimed items remain in the database?
- Should FindIt support only UNT or multiple campuses?
- What accessibility standards should the application follow?
- What deployment and hosting approach should be used?
- What are the exact rules for verifying ownership before approving claims?


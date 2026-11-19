# Full Spec: FindIt – Campus Lost & Found Management System

**Team:** Code Eagles  **Date:** November 19, 2026  **Committer:** TODO: Confirm team member responsible for final commit.

> How to use this file: copy it to `docs/FULL_SPEC.md` in your fork. Fill every section. There is **no length limit** here (the Run Brief has one).
> Put a name next to each section: that person owns it and can explain it without the AI.
> If you do not know something, write `TODO:` or add it to Open questions. A marked gap scores better than an invented answer.
> In every section, finish with one line: **AI contribution:** what an AI suggested, and what you changed or rejected (write "none" if none).

**Roles:** Product Owner Kruthika Reddy | Process lead Rithika Pujari | Architect Tobias | Quality lead Chantelle | Prompt engineer :Kruthika Reddy Panchalingala

---

## 0. The idea (Chapter 1)

- The single main problem, and for whom (one sentence):

  FindIt solves the problem of students losing personal belongings on campus by providing a centralized web application where students can report lost and found items, search listings, submit ownership claims, and track the return process.

- Who is harmed if this app fails, is wrong, or leaks data?

  - Students may be unable to recover their lost belongings.
  - Students may receive incorrect information about item availability or claim status.
  - Users' personal information, including names, email addresses, and account information, could be exposed.
  - Administrators may incorrectly approve or reject ownership claims.
  - The university may lose trust in the campus lost-and-found service.

- Anything the app must never do (privacy, safety, legal):

  - It must never expose user passwords or password hashes.
  - It must never allow unauthorized users to access administrator functions.
  - It must never allow users to claim their own reported items.
  - It must never allow returned items to receive new claims.
  - It must never allow multiple claims from the same student for the same item.
  - It must not expose confidential user information.
  - It must validate submitted information before storing records.

**AI contribution:** AI suggested identifying the main problem, affected stakeholders, and privacy risks. The team retained the points relevant to the actual FindIt application.

## 1. Process and plan (Chapters 2 and 3)  Owner: Rithika Pujari

- Process model we chose (plan-driven, incremental, or agile) and **why it fits this app** (2 sentences):

  We chose an Agile iterative development process using short sprints. This allows our team to develop the application in smaller increments, review progress regularly, and make changes based on feedback.

- Practices we actually use: stand-up / sprints / board / retrospective / code review / tests on every change

  - Stand-up and team progress updates.
  - Sprints.
  - GitHub for version control and task tracking.
  - Retrospectives.
  - Code review through GitHub.
  - Automated tests using pytest.

- **Definition of Done** (checklist, 4 or more items):
  - [ ] The feature meets the agreed acceptance criteria.
  - [ ] The code follows the project's coding standards.
  - [ ] Appropriate tests are written and pass.
  - [ ] The code is reviewed by another team member.
  - [ ] No critical bugs remain.
  - [ ] Documentation is updated.
  - [ ] Changes are merged into the main branch.

- Sprint plan (what is working at the end of each sprint):

| Sprint | Working software at the end | se-agent run? |
|---|---|---|
| 1 | Project planning, requirements, identified users, and initial application scope. | TODO: Not recorded |
| 2 | Flask application architecture, SQLite database structure, and initial design. | TODO: Not recorded |
| 3 | Core lost-item reporting, found-item reporting, and search functionality. | TODO: Not recorded |
| 4 | User claims, administrator claim approval/rejection, and returned-item functionality. | TODO: Not recorded |
| 5 | Automated testing, documentation, final application demonstration, and project finalization. | TODO: Not recorded |

- Biggest schedule risk and what we will do about it:

  Integration issues between frontend, backend, and database components could delay development. We will use GitHub for version control, maintain clear module responsibilities, integrate features early, and perform automated testing throughout development.

- AI contribution:

  ChatGPT and Claude suggested an iterative development process, sprint planning, and Definition of Done criteria. The team reviewed and adapted these suggestions to the FindIt project.

## 2. Requirements (Chapter 4)  Owner (Product Owner): Kruthika Reddy

**Stakeholders and what each wants:**

| Stakeholder | Wants |
|---|---|
| Students | Easily report lost belongings, search for found items, and submit ownership claims. |
| Campus staff | Manage lost-and-found records efficiently. |
| Administrators | Review claims, prevent fraudulent claims, and update item statuses. |
| University | Provide a reliable and user-friendly campus service. |
| Development team | Build a maintainable, testable, and functional application. |

**User stories** (as a ___, I want ___, so that ___), each with acceptance criteria:

1. **Report a lost item**

   As a student, I want to report a lost item with its name, category, description, date, and location, so that other students can identify it.

   Acceptance criteria:
   - The user must be logged in.
   - The user enters the required item details.
   - Invalid or missing information must be rejected.
   - A valid report must be stored and displayed.

2. **Report a found item**

   As a student, I want to report a found item, so that its owner can find it.

   Acceptance criteria:
   - The user must be logged in.
   - The found item must be saved with its details.
   - The item must appear in the found-items listing.

3. **Search for items**

   As a student, I want to search and filter items by category, location, date, and report type, so that I can find a possible match.

   Acceptance criteria:
   - Users can browse item listings.
   - Users can filter by category, location, date, and report type.
   - Only matching results should be displayed.

4. **Submit an ownership claim**

   As a student, I want to submit a claim for a found item, so that I can request the return of my belongings.

   Acceptance criteria:
   - The user must be logged in.
   - The item must be a found item with open status.
   - The claimant must not be the person who reported the item.
   - Only one claim per student per item is allowed.
   - The claim must be stored with pending status.

5. **Review claims and return items**

   As an administrator, I want to review ownership claims and approve or reject them, so that items are returned to their rightful owners.

   Acceptance criteria:
   - Only administrators can access administrator functions.
   - Administrators can approve or reject pending claims.
   - Approval changes the item status to claimed.
   - Rejection leaves the item status unchanged.
   - After pickup, the administrator can mark the item as returned.
   - Returned items cannot receive new claims.

**Requirements table**

| ID | Type (F = functional, NF = non-functional) | Requirement (one testable sentence) | Priority (Must/Should) | Acceptance test (input -> expected result) |
|---|---|---|---|---|
| R1 | F | Users can report lost and found items with the required item details. | Must | Submit valid lost/found details -> item is stored and displayed. |
| R2 | F | Users can search and filter items by category, location, date, and report type. | Must | Enter search filters -> only matching items are displayed. |
| R3 | F | Users can submit claims for open found items and administrators can review claims. | Must | Submit a valid claim -> pending status; approve/reject -> corresponding claim status is updated. |
| R4 | NF (performance) | The application must return search results within an acceptable response time. | TODO: Specify measurable time limit | Perform a search -> results should appear within the agreed response-time limit. |
| R5 | NF (usability) | The application must allow students to report and search for items through understandable web pages and forms. | Should | Ask at least three students to report and search for items -> record task completion and feedback. |
| R6 | NF (security or privacy) | The application must protect passwords and restrict administrator functions to authenticated administrators. | Must | Attempt unauthorized administrator access and inspect password storage -> access is denied and passwords are hashed. |
| R7 | NF (cost) | The initial application must not require a paid runtime AI service. | Must | Run the application without an external AI service -> core functionality continues without runtime AI charges. |

**Out of scope** (so nobody builds it by accident):

- Real-time GPS tracking.
- Online payment functionality.
- AI-based image recognition.
- Live chat.
- Separate native mobile application.
- Runtime AI-based item matching.
- External email notification service in the initial version.

**Requirements we removed as unnecessary, and why:**

- Real-time GPS tracking: Campus location descriptions are sufficient for the initial version.
- Online payment functionality: The application does not involve financial transactions.
- AI-based image recognition: It increases complexity and is not essential to the main functionality.
- Live chat: Users can communicate through the claim process.
- Mobile application: A responsive web application is sufficient for the initial project scope.

**Open questions** (better listed than guessed):

- Should users receive email notifications when a claim is approved?
- Should item images be supported in a future version?
- How long should returned or unclaimed items remain in the database?
- Should the application support multiple campuses?
- What measurable response-time target should be used for search?
- What is the deployment and hosting cost?
- What is the agreed usability success target?
- What are the exact rules for verifying ownership before an administrator approves a claim?

**Check:** could two people read each requirement and build different things? Are there words like *fast*, *easy*, *secure*? Replace each with something observable.

  The functional requirements are supported by specific application workflows and tests. The performance target and usability success target still need measurable values. These are recorded as open questions rather than assumed.

- AI contribution:

  ChatGPT and Claude helped draft functional and non-functional requirements, user stories, and acceptance criteria. The team reviewed the suggestions, retained features within the project scope, and removed unnecessary functionality such as GPS tracking, payments, and AI image recognition.

## 3. Models (Chapter 5)  Owner (Architect): Tobias

Text, bulleted lists, or Mermaid are all fine.

**Context model** (what is inside the system, what is outside, what crosses the boundary):

Inside the FindIt system:
- Flask application.
- User authentication and registration.
- Lost and found item reporting.
- Search and filtering functionality.
- Claim submission and review.
- Administrator functions.
- SQLite database.
- HTML templates, CSS, and JavaScript.

Outside the FindIt system:
- Students.
- Campus staff.
- Administrators.
- University environment.
- Student browsers.

Information crossing the system boundary:
- Students submit registration and login information.
- Students submit lost and found item details.
- Students search for listings and submit claims.
- Administrators approve or reject claims.
- Administrators update item statuses.
- The application retrieves and displays stored information.

**Use cases or a sequence model for the most important story:**

Main use cases:
1. Register an account.
2. Log in.
3. Report a lost item.
4. Report a found item.
5. Search and filter items.
6. View item details.
7. Submit an ownership claim.
8. View personal claim status.
9. Review pending claims as an administrator.
10. Approve or reject claims.
11. Mark an item as returned.
12. Log out.

Important sequence model – Found item claim and return:

```text
Finder
  |
  v
Log in
  |
  v
Submit Found Item Report
  |
  v
Flask validates item information
  |
  v
SQLite stores item (Open)
  |
  v
Owner searches for item
  |
  v
Owner submits claim
  |
  v
Claim stored (Pending)
  |
  v
Administrator reviews claim
  |
  +------ Reject ------> Claim Rejected
  |
  +------ Approve -----> Claim Approved
                           |
                           v
                     Item Claimed
                           |
                           v
                    Item picked up
                           |
                           v
                 Administrator marks
                      Returned
```

**Class or data model** (main entities and how they relate):

Main entities:

1. User
   - User ID
   - Name
   - Email
   - Password hash
   - Administrator status

2. Item
   - Item ID
   - Kind (Lost or Found)
   - Name
   - Category
   - Description
   - Date
   - Location
   - Status
   - Reporter ID

3. Claim
   - Claim ID
   - Item ID
   - Claimant ID
   - Ownership message
   - Claim status

Relationships:
- One user can report multiple items.
- One item can have multiple claims.
- One claim belongs to one item and one claimant.
- An administrator can review multiple claims.
- Database operations are managed through `database.py`.

**State model** (only if the app has modes; otherwise write "no modes"):

Item lifecycle:

```text
Open → Claimed → Returned
```

Claim lifecycle:

```text
Pending → Approved
Pending → Rejected
```

Rules:
- Only open found items can receive claims.
- A student's own reported item cannot be claimed by that student.
- A student cannot submit duplicate claims for the same item.
- Only an administrator can approve or reject claims.
- Only an item with an approved claim can be marked returned.
- Returned items cannot receive additional claims.

**Consistency check:** a requirement that appears in no model, or a model element no requirement needs, and how we resolved it:

The main requirements are represented in the use cases and application models. User authentication, item reporting, search, claim processing, and administrator operations are included in the models. Runtime AI matching and GPS tracking are excluded because they are outside the approved project scope.

- AI contribution:

  AI helped suggest the context, use-case, class, and state models. The team reviewed them against the actual Flask routes, SQLite tables, and implemented workflows.

## 4. Architecture (Chapter 6)  Owner (Architect): Tobias

- Pattern we chose (layered, MVC, client-server, pipe-and-filter, other):

  Three-layer architecture with MVC-style separation.

  1. Presentation Layer: HTML templates, CSS, and JavaScript.
  2. Application Layer: Python Flask application and routes.
  3. Data Layer: SQLite database and database operations.

  The application also uses a repository-style approach for database operations.

- Which non-functional requirements drove it (name the R-numbers):

  - R5: Usability.
  - R6: Security and privacy.
  - R4: Performance considerations.
  - R7: Cost.

- Alternatives we rejected, and why:

  - Django: Rejected because Flask is simpler for the project's limited scope.
  - React: Rejected because a separate frontend framework is unnecessary for the initial application.
  - PostgreSQL: Rejected for the prototype because SQLite is easier to configure and sufficient for a small application.
  - Microservices: Rejected because the application does not require distributed services.

- **If the app uses an AI model:** where it is used; what happens when it is slow, wrong, or down (the non-AI fallback); the cost per use:

  The FindIt application does not use an AI model or external AI service at runtime.

  ChatGPT and Claude were used as development-assistance tools for requirements drafting, code explanations, and test-case suggestions.

  If AI assistance is unavailable, the team can continue development using project documentation, manual coding, and testing.

  Runtime AI cost per use: $0.

**Decisions log**

| # | Decision | Alternatives | Reason (tie to an R-number) | Consequence |
|---|---|---|---|---|
| D1 | Use Flask | Django, FastAPI | Simplicity and maintainability (R5) | Team must organize modules carefully. |
| D2 | Use SQLite | PostgreSQL, MySQL | Simple setup and local storage (R7) | Limited scalability for larger deployments. |
| D3 | Use three-layer architecture | Unstructured monolithic design | Maintainability and testability (R5, R6) | Requires clear module boundaries. |
| D4 | Use GitHub for version control | GitLab, Bitbucket | Supports collaboration and code review | Team must follow branching and review rules. |
| D5 | Exclude AI from runtime functionality | AI-based image matching | Keeps initial scope and runtime cost manageable (R7) | Search is based on filters rather than AI matching. |

- AI contribution:

  ChatGPT suggested a simple Flask architecture using SQLite and separation between routes, models, and database operations. The team reviewed the architecture and selected it based on project requirements and scope.

## 5. Design and implementation (Chapter 7)  Owner: Kruthika Reddy

- Modules, and the owner of each:

| Module | Owner | Responsibility |
|---|---|---|
| `app.py` | Tobias | Flask application, application configuration, CSRF protection, and application initialization. |
| `routes/auth.py` | Tobias | User registration, login, logout, and authentication. |
| `routes/items.py` | Tobias | Lost and found item reporting, searching, filtering, and item details. |
| `routes/claims.py` | Tobias | Claim submission and claim validation. |
| `routes/admin.py` | Tobias | Administrator functions, claim approval/rejection, and returned-item updates. |
| `models.py` | Rithika | User, Item, and Claim validation and data-related models. |
| `database.py` | Rithika | SQLite database connection, schema, and CRUD operations. |
| `templates/` | Kruthika | HTML pages and user interface. |
| `static/` | Kruthika | CSS and frontend styling. |
| `tests/` | Chantelle | Automated tests and quality checks. |

- Where the logic lives **apart from the display** (so it can be unit-tested):

  - Business logic is handled by Flask routes in the `routes/` directory.
  - Item and registration validation is handled in `models.py`.
  - Database operations are handled separately in `database.py`.
  - Presentation is handled through HTML templates in `templates/` and CSS in `static/`.
  - Automated tests are maintained in `tests/`.

- Design patterns we will use, and where (or "none yet"):

  - MVC-style separation: Routes, models, and templates are separated.
  - Repository pattern: Database operations are organized in `database.py`.
  - Input validation: Used for user registration, item reporting, and claim submission.
  - Blueprint organization: Flask routes are separated into authentication, items, claims, and administrator modules.

- Code or libraries we will reuse, with their licenses:

| Library | Purpose | License |
|---|---|---|
| Flask | Web application framework | BSD-3-Clause |
| SQLite | Database | Public domain |
| Werkzeug | Password hashing and Flask utilities | BSD-3-Clause |
| pytest | Automated testing | MIT |
| pytest-cov | Test coverage measurement | MIT |
| Click | Command-line utilities | BSD-3-Clause |

- Branching and review rule (for example: pull request, one approval, tests green):

  - The main branch must remain stable.
  - Each feature must be developed in a separate branch.
  - Pull requests must be reviewed by at least one team member.
  - Automated tests must pass before merging.
  - Commit messages must describe the changes.
  - No passwords, API keys, or confidential data may be committed.
  - GitHub Issues will be used to track bugs and development tasks.

- Technical debt we are knowingly accepting:

  - SQLite is suitable for the prototype but may need replacement for production deployment.
  - Email notifications are excluded from the first version.
  - The initial application uses basic search filters instead of advanced matching.
  - Deployment and large-scale performance testing may be limited.
  - The initial application may use a basic interface rather than a fully optimized mobile experience.

- AI contribution:

  ChatGPT and Claude provided suggestions for application architecture, module organization, and implementation approaches. The team reviewed and adapted these suggestions to the actual Flask and SQLite project structure.

## 6. Testing (Chapter 8)  Owner (Quality lead): Chantelle

**Requirement-to-test map** (every Must-do needs at least one):

| Requirement | Test (file::name) | Type (unit / component / system / user) | How we will check it can fail |
|---|---|---|---|
| R1 | `tests/test_items.py::test_create_lost_item` and `tests/test_items.py::test_create_found_item` | Component | Submit invalid item information and verify that the test fails if validation or saving is broken. |
| R2 | `tests/test_items.py::test_search_filter` | Component | Change search filters or expected results and verify that the assertion fails. |
| R3 | `tests/test_claims.py::test_submit_claim`, `tests/test_admin.py::test_review_claim`, `tests/test_admin.py::test_reject_claim` | Integration | Break claim creation or status updates and verify that the expected status assertions fail. |
| R4 | TODO: Performance test not documented | System | TODO: Define a measurable response-time limit and test against it. |
| R5 | TODO: External usability test | User | Ask at least three students to complete reporting and searching tasks and record their results. |
| R6 | `tests/test_admin.py::test_unauthorized_access`, `tests/test_validation.py::test_csrf_required` | Integration | Remove authorization or CSRF checks and verify that the expected access-denial or validation assertions fail. |
| R7 | TODO: Runtime AI cost test not required; application has no runtime AI service | System | Run the core application without an AI service and verify that its main functions work. |

Additional implemented test cases:

- `tests/test_items.py::test_mark_returned`
- `tests/test_items.py::test_item_status_display`
- `tests/test_claims.py::test_cannot_claim_returned_item`
- `tests/test_admin.py::test_reject_claim`
- `tests/test_validation.py::test_invalid_input`
- `tests/test_validation.py::test_validate_item_ok`
- `tests/test_validation.py::test_registration_rules`
- `tests/test_database.py::test_record_consistency`

The project contains 15 automated test cases across five test files.

**The three most important tests, in plain language** (input -> expected result):

1. **Lost and found item reporting**

   Input: A registered student submits a valid lost or found item report containing the required details.

   Expected result: The application saves the item in SQLite and displays it in the appropriate listing.

2. **Claim approval and rejection**

   Input: A student submits an ownership claim for an open found item, and an administrator approves or rejects it.

   Expected result: The claim status changes to approved or rejected. Approval changes the item status to claimed, while rejection leaves the item open.

3. **Unauthorized access and returned-item protection**

   Input: A normal student attempts to access administrator functions or submit a claim for a returned item.

   Expected result: Administrator access is denied, and the returned item cannot receive another claim.

- Edge cases we will try to break each Must-do with (zero, negative, empty, huge, missing):

  - Lost and found reporting:
    - Empty item name.
    - Missing category.
    - Missing description.
    - Invalid date.
    - Future date.
    - Missing location.
    - Invalid item information.

  - Search:
    - Empty search.
    - Non-existing category.
    - Non-existing location.
    - Date filter with no matching results.
    - Different report types.

  - Claims:
    - Claiming an item reported by the same user.
    - Duplicate claims.
    - Claiming a lost item.
    - Claiming a returned item.
    - Submitting an empty ownership message.
    - Claiming an item that is no longer open.

  - Administrator functions:
    - Anonymous access.
    - Normal student access.
    - Approving an already decided claim.
    - Marking an item returned without an approved claim.

  - Database:
    - Duplicate claims.
    - Invalid foreign-key references.
    - Missing required records.

- User testing: who (outside the team), and what we want to learn:

  Who: Campus students who are not members of the development team.

  We want to learn:
  - Whether students can register and log in.
  - Whether students can report lost and found items.
  - Whether students can search and filter listings.
  - Whether students understand how to submit an ownership claim.
  - Whether users can understand their claim status.
  - Whether the application is easy to navigate.

  At least three students will be asked to complete reporting, searching, and claiming tasks.

- What we are deliberately **not** testing, and why:

  - Large-scale performance testing: Outside the initial project scope.
  - Production deployment: The project is currently focused on local application functionality.
  - External email notifications: Email notifications are not included in the initial version.
  - AI image recognition: No runtime AI functionality is implemented.
  - GPS tracking: Excluded from the project scope.

- Test command: `pytest -v`

  Coverage command: `pytest --cov=. --cov-report=term-missing`

- AI contribution:

  ChatGPT suggested pytest test cases for lost-item reporting, found-item reporting, claim submission, and validation. The team implemented and reviewed test cases against actual application behavior. The actual project includes 15 automated test cases across five test files.

## 7. Evolution (Chapter 9)  Owner: Rithika Pujari

- The most likely future change:

  Add email notifications for claim status updates so that students can receive information when an administrator approves or rejects their claim.

- Impact analysis: modules, models, requirements and tests that would change, and about how long:

  The email notification enhancement would require changes to:

  - `routes/claims.py`: Trigger notification-related actions when a claim is processed.
  - `routes/admin.py`: Trigger notifications after claim approval or rejection.
  - `database.py`: Store any additional notification information if required.
  - `templates/`: Display notification-related information if needed.
  - `tests/`: Add tests for notification behavior.

  Models:
  - User model may require notification-related information if preferences are introduced.
  - Claim model remains responsible for claim status.

  Requirements:
  - Add a new functional requirement for email notifications.

  Estimated time: TODO: Determine after selecting an email service and defining notification behavior.

- What design choice today would make that change easier:

  Separating routes, database operations, and presentation makes future notification functionality easier to introduce. Keeping business logic outside the HTML templates also supports testing and maintenance.

- AI contribution:

  AI suggested possible future enhancements such as email notifications, improved search, image uploads, and better authentication. The team selected email notifications as a possible future enhancement based on project scope.

## 8. Decisions we are least sure about

(Prepare to be asked about these.)

- SQLite is suitable for the prototype, but its suitability for larger production deployments needs further evaluation.
- The application does not currently provide email notifications.
- Search uses filters rather than advanced AI-based matching.
- The application does not include real-time GPS tracking.
- The measurable performance target has not yet been finalized.
- External usability testing results need to be documented.
- The future hosting and deployment approach has not been finalized.
- The exact retention period for returned and unclaimed items needs clarification.

## 9. Run plan and cost (se-agent)  Owner (Prompt engineer): TODO: Assign a team member.

- Prompts in `prompts/` we will use, in order:

  1. Suggest functional and non-functional requirements for a campus lost and found web application.
  2. Suggest a simple Flask architecture for a lost and found application using SQLite.
  3. Suggest project features and implementation approaches for a campus lost and found application.
  4. Generate pytest test cases for lost item reporting and claim submission.

  TODO: Confirm whether these prompts are saved in the repository's `prompts/` directory.

- Model (use `gpt-6-luna` for iteration; ask before using a stronger one):

  Previously documented AI tools:
  - ChatGPT GPT-6.
  - Claude (exact model/version not recorded).

  TODO: Confirm whether se-agent was used and which model was used for its runs.

- Planned runs (default: one per sprint):

| Run | Sprint | Prompts | Model | Estimated cost (`uv run python cost_estimate.py docs/RUN_BRIEF.md`) |
|---|---|---|---|---|
| 1 | TODO: Confirm | TODO: Confirm saved prompt files | TODO: Confirm se-agent model | TODO: Run cost estimation command |

- Before we request a run, we confirmed: `uv run pytest` passes / Run Brief is 4,000 characters or fewer / each prompt follows the 8-section template

  TODO: Confirm these three checks before requesting any se-agent run.

## 10. Run Brief

The Run Brief is a **separate file**: `docs/RUN_BRIEF.md`. It is what se-agent reads, and it must be **4,000 characters or fewer** (about 700 words). The agents do not read this Full Spec, so anything a model must know has to be in the Run Brief, in words.

**Keep:** the main problem and user; numbered Must-dos (each testable); technology and data constraints; any cost limit on AI features; the out-of-scope list; 3 to 5 acceptance checks.

**Cut:** process reasoning, stakeholder analysis, long rationale, diagrams (describe the one relationship that matters in a sentence).

**Translate:** non-functional requirements become constraints with numbers; the architecture becomes one sentence; the test plan becomes quality expectations and acceptance criteria.

Check the length:

```bash
python -c "print(len(open('docs/RUN_BRIEF.md', encoding='utf-8').read()))"
```

- Characters in our Run Brief: TODO: Run the command above after creating `docs/RUN_BRIEF.md`.
- What we cut to fit, and why it was safe to cut:

  Detailed process explanations, stakeholder discussions, architecture rationale, and retrospective notes can be excluded because the Run Brief is intended to provide the implementation requirements and constraints needed by the agent. Core functional requirements, security rules, technology choices, and acceptance checks must remain.

## 11. Presentation notes (six beats; every member speaks)

| Beat | Who | One sentence we will say |
|---|---|---|
| 1. Problem, user, Must-dos (Ch 4) | Kruthika Reddy | FindIt helps students report lost and found belongings, search listings, submit ownership claims, and track the return process. |
| 2. Process choice and Definition of Done (Ch 2, 3) | Rithika Pujari | We selected Agile development with short sprints so we could build, review, and test the application incrementally. |
| 3. Context model and one more model (Ch 5) | Tobias | FindIt connects students and administrators through a Flask application and SQLite database, with item and claim state transitions controlling the workflow. |
| 4. One architecture decision: chosen, rejected, which requirement forced it (Ch 6) | Tobias | We selected a three-layer Flask and SQLite architecture instead of a more complex framework or microservices approach because simplicity and maintainability were important to our project. |
| 5. Three most important tests, and how we know they can fail (Ch 8) | Chantelle | We test item reporting, claim approval and rejection, and unauthorized access by checking expected database states and HTTP responses. |
| 6. Likely change, Run Brief, cost plan (Ch 9, 4) | Kruthika Reddy | A likely future enhancement is email notifications for claim updates, while our current application does not depend on paid runtime AI services. |


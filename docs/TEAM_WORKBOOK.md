# Team Workbook — fill this in as you go

**Team name:** Code Eagles **App:** FindIt – Campus Lost & Found Management System **Members & roles:** Rithika Pujari – Project Coordinator & Data/Database Lead; Kruthika Reddy – Requirements & UI/UX Lead; Chantelle – Testing & Quality Assurance Lead; Tobias – Backend & Architecture Lead.

---

## 0. Charter (Ch 2, 3)

- Process model chosen and **why** (2–3 sentences):  
  We chose an Agile iterative development process using short sprints. This allows our team to develop the application in smaller increments, review progress regularly, and make changes based on feedback. Since the project has multiple features, an iterative approach helps us identify problems early and improve the application throughout development.

- Agile practices we use: ☑ user stories ☑ sprints ☑ daily stand-up ☑ retrospective ☑ pair/peer review ☑ CI tests

- Definition of Done (checklist):
  - [ ] It meets the agreed acceptance criteria.
  - [ ] The code follows the project's coding standards.
  - [ ] Appropriate tests are written and pass.
  - [ ] The code is reviewed by another team member.
  - [ ] No critical bugs remain.
  - [ ] Documentation is updated.
  - [ ] Changes are merged into the main branch.

- How we communicate / meeting times:  
  Our team uses Microsoft Teams for meetings, discussions, and sharing project updates. GitHub is used for version control, task tracking, issue management, and code reviews. Team members communicate their progress and blockers during team meetings and through project discussions. Meeting times are coordinated through Microsoft Teams based on team availability.

- How we resolve disagreements:  
  Team members first discuss disagreements using project requirements, technical feasibility, and user needs. We try to reach a consensus by comparing possible solutions. If consensus cannot be reached, the team votes on the preferred option. For major technical or project-scope decisions, we may seek guidance from the instructor.

- AI-use rules we agree to (see Guide §5):
  - AI tools such as ChatGPT and Claude may be used for brainstorming, requirements drafting, code explanations, and test-case generation.
  - AI-generated code must be reviewed and tested before being included in the application.
  - Significant AI contributions must be documented in the AI & prompt log.
  - Team members must understand the code they submit.
  - AI tools must not receive passwords, API keys, or confidential user information.
  - AI-generated suggestions must be checked for correctness, security, and relevance.
  - The team will follow the instructor's AI-use guidelines.

## 1. Requirements (Ch 4)

| **ID** | **Type (F/NF)** | **Requirement** | **Priority** | **Acceptance test** | **Owner** |
| ------ | --------------- | --------------- | ------------ | ------------------- | --------- |
| R1 | F | Users can report a lost item with its name, category, description, date, and location. | High | Submit a valid lost-item form and verify that the item is stored and displayed. | Kruthika |
| R2 | F | Users can report a found item with its details. | High | Submit a found-item form and verify that the item appears in the found-items list. | Kruthika |
| R3 | F | Users can search and filter items by category, date, and location. | High | Search with different filters and verify that matching results are displayed. | Rithika |
| R4 | F | Users can submit a claim for a found item. | High | Submit a claim and verify that it is stored with pending status. | Tobias |
| R5 | F | An administrator can review claims and approve or reject them. | High | Log in as an administrator and update a claim's status. | Tobias |
| R6 | F | An administrator can mark an item as returned. | Medium | Mark an item as returned and verify that the status is updated. | Tobias |
| R7 | F | Users can view the current status of reported items. | Medium | Verify that item status is displayed correctly. | Kruthika |
| R8 | NF | The application must be easy to navigate and understand. | High | Conduct usability testing with at least three users. | Kruthika |
| R9 | NF | The application must validate user input and prevent invalid records. | High | Submit missing or invalid data and verify that an appropriate error message appears. | Chantelle |
| R10 | NF | The application must protect administrative functions from unauthorized access. | High | Attempt to access admin functions without authentication and verify access is denied. | Tobias |
| R11 | NF | The application must store records consistently in the database. | High | Create, update, and retrieve records and verify data consistency. | Rithika |

- Stakeholders & what each wants:
  - Students: Easily report lost belongings and find items reported by others.
  - Campus staff: Manage lost-and-found records efficiently.
  - Administrators: Review claims, prevent fraudulent claims, and update item statuses.
  - University: Provide a reliable and user-friendly campus service.
  - Development team: Build a maintainable, testable, and functional application.

- Ambiguities / questions for the customer:
  - Should users be required to create an account?
  - Should users receive email notifications when a claim is approved?
  - Should item images be required or optional?
  - How long should returned or unclaimed items remain in the database?
  - Who will have administrator privileges?
  - Should the application support only UNT or multiple campuses?

- Requirements removed as unnecessary and why:
  - Real-time GPS tracking: Removed because campus location descriptions are sufficient for the initial version.
  - Online payment functionality: Removed because the application does not involve financial transactions.
  - AI-based image recognition: Removed from the initial version because it increases complexity and is not essential to the main functionality.
  - Live chat: Removed because users can communicate through the claim process.
  - Mobile application: Excluded because a responsive web application is sufficient for the project's initial scope.

- AI contribution note (what the AI drafted, what we changed):  
  ChatGPT and Claude were used as AI-assisted tools during project planning and development. AI suggestions helped explore possible features, requirements, and implementation approaches. The team reviewed the suggestions and selected features based on project scope and feasibility. Unnecessary features such as GPS tracking, payments, and live chat were excluded. Final requirements are subject to team review and instructor feedback.

## 2. Models (Ch 5)

- Context model (inside/outside the system): link  
  `docs/models/context-diagram.md`  
  The FindIt system interacts with students, campus staff, administrators, and the SQLite database.
  - Students report lost and found items, search listings, and submit claims.
  - Administrators review claims and update item statuses.
  - Campus staff may assist with item handling and verification.
  - The database stores item records, user information, and claim details.

- Use cases / sequence models: link  
  `docs/models/use-cases.md`  
  Main use cases:
  - Report a lost item.
  - Report a found item.
  - Search for items.
  - Submit an item claim.
  - Review claims.
  - Approve or reject claims.
  - Mark an item as returned.

- Class (structural) model: link  
  `docs/models/class-diagram.md`  
  Main classes:
  - User
  - Item
  - Claim
  - Admin
  - DatabaseManager

  Relationships:
  - A user can report multiple items.
  - An item can have multiple claims.
  - A claim belongs to one item and one claimant.
  - An administrator can review multiple claims.
  - DatabaseManager handles database operations.

- State (behavioral) model, if any: link  
  `docs/models/state-diagram.md`  
  Item states: Open → Claimed → Returned.  
  Claim states: Pending → Approved / Rejected.  
  The team will define valid state transitions to ensure that returned items cannot be claimed again.

- Inconsistencies found between models and requirements, and how resolved:  
  The models will be reviewed against the requirements to ensure that every use case is supported by a requirement. Any unnecessary functionality found in the models will be removed or documented as a future enhancement. Missing requirements will be added after team discussion and approval.

## 3. Architecture (Ch 6)

- Chosen pattern(s):  
  We will use a three-layer architecture:
  1. Presentation Layer: HTML, CSS, and JavaScript for the user interface.
  2. Application Layer: Python Flask routes and business logic.
  3. Data Layer: SQLite database for storing application records.

  We will also use an MVC-style separation of responsibilities and a repository-style approach for database operations.

- Which non-functional requirements drove it:  
  Maintainability, testability, simplicity, and security influenced the architecture. Separating the interface, business logic, and database makes the application easier to test, debug, and modify.

- Alternatives rejected and why:
  - Django: Rejected because Flask is simpler for the project's limited scope.
  - React: Rejected because a separate frontend framework is unnecessary for the initial application.
  - PostgreSQL: Rejected for the prototype because SQLite is easier to configure and sufficient for a small application.
  - Microservices: Rejected because the application does not require distributed services.

- Decisions log:

| # | Decision | Alternatives | Reason | Consequence |
|---|---|---|---|---|
| D1 | Use Flask | Django, FastAPI | Lightweight and easy to learn | Team must organize modules carefully |
| D2 | Use SQLite | PostgreSQL, MySQL | Simple setup and local storage | Limited scalability for larger deployments |
| D3 | Use three-layer architecture | Unstructured monolithic design | Improves maintainability and testing | Requires clear module boundaries |
| D4 | Use GitHub for version control | GitLab, Bitbucket | Familiar and supports collaboration | Team must follow branch and review rules |
| D5 | Exclude AI from runtime app functionality | AI image matching | Keeps initial scope manageable | Search is based on filters rather than AI matching |

- Where an AI model/service is used in the app (if at all), its failure fallback, and cost per use:  
  The initial FindIt application will not use an AI model or external AI service at runtime. ChatGPT and Claude are used as development-assistance tools for requirements drafting, code explanations, and test-case suggestions. If AI assistance is unavailable, the team will continue using project documentation, manual development, and testing. Runtime AI cost per use: $0.

## 4. Design & implementation (Ch 7)

- Modules and who owns each:

| Module | Responsibility | Owner |
|---|---|---|
| `app.py` | Flask application and route configuration | Tobias |
| `routes/items.py` | Lost and found item operations | Tobias |
| `routes/claims.py` | Claim submission and review | Tobias |
| `routes/admin.py` | Administrator functions | Tobias |
| `routes/auth.py` | User registration, login and authentication | Tobias |
| `models.py` | User, Item, and Claim data models | Rithika |
| `database.py` | Database connection and CRUD operations | Rithika |
| `templates/` | HTML pages | Kruthika |
| `static/` | CSS and JavaScript | Kruthika |
| `tests/` | Automated tests and quality checks | Chantelle |

- Patterns used and where:
  - MVC-style separation: Routes, models, and templates are separated.
  - Repository pattern: Used to organize database operations.
  - Input validation: Used for form submissions and user data.
  - Peer review: Used for changes submitted through GitHub pull requests.

- Reused code / libraries and their licenses:

| Library | Purpose | License |
|---|---|---|
| Flask | Web application framework | BSD-3-Clause |
| SQLite | Database | Public domain |
| pytest | Automated testing | MIT |
| Werkzeug | Flask utilities and security features | BSD-3-Clause |
| pytest-cov | Test coverage measurement | MIT |
| click | Command-line utilities | BSD-3-Clause |

- Branching & review rules (e.g., PR needs 1 approval, tests green):
  - The main branch must remain stable.
  - Each feature must be developed in a separate branch.
  - Pull requests must be reviewed by at least one team member.
  - Automated tests must pass before merging.
  - Commit messages must describe the changes.
  - No passwords, API keys, or confidential data may be committed.
  - GitHub Issues will be used to track bugs and development tasks.

- Technical debt we knowingly took on:
  - SQLite is suitable for the prototype but may need replacement for production deployment.
  - Email notifications are excluded from the first version.
  - The initial application uses basic search filters instead of advanced matching.
  - Deployment and large-scale performance testing may be limited.
  - The initial application may use a basic interface rather than a fully optimized mobile experience.

## 5. Testing (Ch 8)

| Requirement | Test (file::name) | Type (unit/component/system/user) | Passes? | Does it fail when code is broken? (tried it) |
|---|---|---|---|---|
| R1 | `test_items.py::test_create_lost_item` | Unit | Test implemented; execution not verified here | Not yet verified |
| R2 | `test_items.py::test_create_found_item` | Unit | Test implemented; execution not verified here | Not yet verified |
| R3 | `test_items.py::test_search_filter` | Component | Test implemented; execution not verified here | Not yet verified |
| R4 | `test_claims.py::test_submit_claim` | Component | Test implemented; execution not verified here | Not yet verified |
| R5 | `test_admin.py::test_review_claim`, `test_admin.py::test_reject_claim` | Integration | Test implemented; execution not verified here | Not yet verified |
| R6 | `test_items.py::test_mark_returned` | Integration | Test implemented; execution not verified here | Not yet verified |
| R7 | `test_items.py::test_item_status_display` | System | Test implemented; execution not verified here | Not yet verified |
| R8 | Usability testing with at least three students | User | Planned | Not yet verified |
| R9 | `test_validation.py::test_invalid_input`, `test_validation.py::test_validate_item_ok`, `test_validation.py::test_registration_rules`, `test_validation.py::test_csrf_required` | Unit | Test implemented; execution not verified here | Not yet verified |
| R10 | `test_admin.py::test_unauthorized_access` | Integration | Test implemented; execution not verified here | Not yet verified |
| R11 | `test_database.py::test_record_consistency` | Integration | Test implemented; execution not verified here | Not yet verified |

- Test command: `pytest -v`  
  Coverage / what is NOT tested:  
  The project includes 15 automated test cases across five test files. Testing focuses on item reporting, claim processing, input validation, database operations, and admin authorization. The application also tests password hashing, CSRF protection, and restrictions against claiming returned items. Large-scale performance, production deployment, and external email services are outside the initial test scope.

- User testing: who (outside team), what they struggled with:  
  Who (outside team): Campus students who are not members of the development team.  
  Planned testing: At least three students will be asked to report a lost item, search for a found item, and submit a claim.  
  What they struggled with: To be documented after actual user testing.  
  User feedback will be used to improve navigation, form clarity, and the overall user experience.

- Bugs found after "done" and their cause:  
  No post-completion bugs have been documented yet. Bugs discovered during development will be recorded with their cause, fix, and date.

## 6. Evolution & retrospective (Ch 9)

- Most likely future changes:
  - Email notifications for claim updates.
  - Image uploads for lost and found items.
  - Improved search and matching functionality.
  - Mobile-friendly interface improvements.
  - Support for multiple campus locations.
  - Better authentication and role management.
  - Improved database scalability.

- Change request carried out: what, impact analysis, files touched, how long it took:  
  Change request: Add a category filter to the item search page.  
  Status: Planned enhancement.  
  Impact analysis: The search route, database query, and user interface must support filtering by category. Existing item records will remain unchanged.  
  Files expected to be touched:
  - `routes/items.py`
  - `templates/search.html`
  - `tests/test_items.py`

  Estimated time: 2–4 hours.  
  Actual time: To be recorded after implementation.  
  Result: To be recorded after implementation and testing.

- What would have made the change easier:  
  Clear module separation, automated regression tests, a documented database structure, and early agreement on requirements would make future changes easier. Consistent GitHub Issues and pull request reviews will also help the team understand the impact of changes.

## 7. AI & prompt log

| Run # | Date | Prompts used | Model | Tokens / cost | What was useful | What was wrong / rejected |
|---|---|---|---|---|---|---|
| 1 | 2026-11-05 | "Suggest functional and non-functional requirements for a campus lost and found web application." | ChatGPT GPT-6 | Not available | Helped organize requirements and acceptance criteria. | Removed unnecessary features such as GPS and payment processing. |
| 2 | 2026-11-05 | "Suggest a simple Flask architecture for a lost and found application using SQLite." | ChatGPT GPT-6 | Not available | Suggested the separation of routes, models, and database operations. | Reviewed the architecture for project size and simplified it. |
| 3 | Actual date not recorded | "Suggest project features and implementation approaches for a campus lost and found application." | Claude (model/version not recorded) | Not available | Helped explore possible features and approaches. | Suggestions were reviewed for scope and feasibility. |
| 4 | 2026-11-05 | "Generate pytest test cases for lost item reporting and claim submission." | ChatGPT GPT-6 | Not available | Suggested useful positive and negative test cases. | Tests must be verified against actual application behavior. |

- Changes we made to our prompts after reviewing runs and why:  
  We improved prompts by providing the application context, specific module names, expected behavior, and project constraints. We asked AI to generate smaller, focused outputs rather than entire applications. We also requested test cases and explanations so that the team could verify suggestions. Prompts were revised when responses included unnecessary features or assumptions. AI tools were used to support development, but the team remains responsible for reviewing and validating all generated content.

## 8. Sprint retrospectives

| Sprint | Went well | Went badly | One improvement we will try |
|---|---|---|---|
| 1 – Planning & Requirements | The team selected the project topic, identified its main users, and defined the initial scope. | Some requirements and responsibilities may need further clarification. | Confirm acceptance criteria and task ownership before implementation. |
| 2 – Design & Database | The team planned a simple architecture and database structure. | Integration may require additional coordination between modules. | Agree on interfaces and data structures before coding. |
| 3 – Core Implementation | Development of core item reporting and search functionality has started. | Integration issues may occur between frontend and backend components. | Integrate features early and test continuously. |
| 4 – Claims & Testing | Claim management and admin functionality are included in the development plan. | Bugs may be discovered late in the development process. | Add automated tests during development instead of afterward. |
| 5 – Finalization | Final testing, documentation, and demo preparation are planned. | Last-minute changes may affect application stability. | Freeze features before the final demo and focus on bug fixes. |

## 9. Final demo checklist

☐ App runs from the README steps on a clean machine  
☐ Tests pass  
☐ Each requirement traced to a test  
☐ Every team member can explain the architecture  
☐ AI contribution notes complete  
☐ No secrets in the repo history



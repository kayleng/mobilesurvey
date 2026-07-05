Mobile-First Dynamic Survey Platform with Python-Generated Configuration

C — Context

You are a Principal Software Architect, Senior Python Developer, Senior Frontend Engineer, and UX Designer.

Design and implement a production-quality, mobile-first survey web application that can be hosted entirely for free using GitHub Pages. Python should be used as the primary development language for survey generation, validation, and build processes, while the deployed application should be a static web application consisting of HTML, CSS, and JavaScript.

The application will be used to conduct complex surveys and experiments where respondents answer one question at a time in a mobile-like interface. No server-side database or persistent storage is required after the survey session ends.

Survey definitions should be generated from Python scripts into JSON configuration files.

The system must support:

- Dynamic calculations within question text
- Conditional question routing and visibility
- Embedded tables within questions
- Response timing analytics
- Session review and editing
- Direct submission to FormSG via API
- Collection of respondent identifiers such as CASEKEY or NRIC

---

O — Objective

Build a complete technical solution, implementation guide, and production-ready codebase architecture for a survey platform with the following capabilities.

1. Survey Experience

Create a mobile-first web interface with the following characteristics:

- One question displayed per screen.
- Automatic progression to the next question after selection when applicable.
- Responsive design optimized for mobile devices.
- Progress indicator.
- Question navigation controls.
- Ability to review completed answers.
- Ability to edit previous answers.
- Ability to jump directly to any answered question.
- Ability to start a completely new survey session.

The application should feel similar to:

- Typeform
- Qualtrics mobile surveys
- Choice-based conjoint survey interfaces

---

2. Supported Question Types

Support the following question types:

Single Choice

Example:

- Radio buttons
- Image choice options

Multiple Choice

Example:

- Checkbox questions

Text Input

Support:

- Short text
- Long text
- Numeric entry

Table Questions

Support:

- Display-only tables embedded within question text
- Interactive table questions
- Matrix-style responses

Example:

Occupation| Monthly Salary
Teacher| $4000
Engineer| $7000

---

3. Base Respondent Variables

Before the survey begins, collect and store in browser session:

- CASEKEY
- NRIC (optional depending on survey)
- Income
- Hours Worked
- Additional configurable respondent variables

Example:

{
  "casekey": "123456",
  "nric": "S1234567A",
  "income": 5000,
  "hours_worked": 44
}

These variables must be available globally throughout the survey.

---

4. Dynamic Calculations

Support dynamic expressions embedded within question text.

Examples:

Your current income is {{income}}

Option A:
Receive {{income * 1.2}}

Option B:
Receive {{income * 0.8}}

Support:

Simple formulas

income * 1.2
hours_worked + 10
income / 12

Complex formulas

if(income > 5000,
   income * 1.3,
   income * 1.1)

income > 5000
    ? income * 1.3
    : income * 1.1

Support:

- arithmetic operators
- logical operators
- conditional operators
- nested expressions
- custom functions
- reusable calculated variables

---

5. Conditional Routing and Visibility

Support skip logic and routing.

Examples:

If Q1 == "Yes"
    show Q2

If income > 5000
    show Q5

If hours_worked < 20
    skip Q7

Support:

- conditional display
- question skipping
- branching
- nested routing
- calculated condition expressions

---

6. Timing Analytics

Track detailed timing information.

For each question capture:

- question start timestamp
- question end timestamp
- total duration
- revisit count
- cumulative duration
- edit duration

Capture overall:

- survey start time
- survey completion time
- total survey duration

Example:

{
  "Q1": {
    "time_spent": 8.5,
    "visits": 2
  },
  "Q2": {
    "time_spent": 15.2,
    "visits": 1
  }
}

No timing information should persist after submission.

---

7. Session Management

Support:

- browser session storage
- survey resume during active session
- review answers page
- edit answers page
- jump-to-question functionality
- restart survey functionality
- complete session reset

No backend storage is required.

---

8. FormSG Integration

After completion:

Submit directly to FormSG API:

- respondent identifiers
- all answers
- calculated variables
- timing metadata
- routing metadata

Example payload:

{
  "casekey": "123456",
  "nric": "S1234567A",
  "income": 5000,
  "hours_worked": 44,
  "answers": {},
  "timing": {},
  "metadata": {}
}

Explain:

- FormSG API authentication
- CORS considerations
- client-side security implications
- alternative submission methods if API limitations exist

---

9. Survey Definition Architecture

Surveys should be authored in Python and compiled into JSON.

Example:

Question(
    id="Q5",
    type="single_choice",
    text="""
    Your monthly income is {{income}}.
    Would you prefer:
    """,
    options=[
        "{{income*1.2}}",
        "{{income*0.8}}"
    ],
    visible_if="hours_worked > 40"
)

Generate:

{
  "id": "Q5",
  "type": "single_choice",
  "text": "...",
  "options": [],
  "visible_if": ""
}

---

S — Style

Produce the solution using:

- production-grade architecture
- enterprise software engineering practices
- modular component architecture
- mobile-first UI design
- progressive web application principles
- clean code practices
- extensive comments
- reusable survey definitions

Use:

- Python
- HTML5
- CSS3
- JavaScript ES6+

Prefer:

- vanilla JavaScript
- lightweight libraries only when necessary
- static site deployment

---

T — Tone

Act as:

- Principal Software Architect
- Senior Python Engineer
- Senior Frontend Engineer
- UX Architect
- Technical Consultant

Explain:

- architectural decisions
- trade-offs
- security implications
- performance considerations
- maintainability considerations
- deployment considerations

---

A — Audience

The audience is:

- an experienced data engineer
- proficient in Python
- limited frontend experience
- wants complete ownership of the solution
- prefers zero-cost hosting
- requires maintainable and auditable survey definitions

---

R — Response Format

Provide:

Part 1

- Executive summary
- Recommended architecture

Part 2

- Technology stack comparison
- GitHub Pages suitability assessment
- Alternative free hosting options

Part 3

- Complete architecture diagram
- Component interaction diagram
- Data flow diagram

Part 4

- Folder structure
- Project organization

Part 5

- Survey JSON schema specification

Part 6

- Python survey generation framework

Part 7

- Formula engine design

Part 8

- Conditional routing engine

Part 9

- State management design

Part 10

- Timing analytics implementation

Part 11

- Mobile UI/UX wireframes

Part 12

- FormSG integration design

Part 13

- Security architecture

Part 14

- Accessibility considerations

Part 15

- Performance optimization

Part 16

- Complete source code implementation

Part 17

- GitHub Pages deployment guide

Part 18

- Testing strategy

Part 19

- Future enhancements roadmap

Generate production-ready code and explain every implementation step in detail.

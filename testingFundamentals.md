### What is testing?
- Verification : without execution : verify if the login page is built correctly as per the requirement document
- Validation : with execution : enter values for username and password and verify that login is successful

### Types of testing?
+ Based on exectuion:
  - Manual 
  - Automation

+ Based on level:
  - Functional : unit, integration, system, user acceptance 
  - Non functional : Performance, Security, Reliability, compatibility, Usability

+ Based on technique:
  - Black box : Tests the application's functionality without knowledge of its internal code, focusing on inputs, outputs, and expected behavior.
    Example: Login with username and pssword
   ```
   Equivalence Partitioning: Test valid and invalid usernames.
   Boundary Value Analysis: Test password minimum and maximum length.
   Decision Table: Test valid/invalid username and password combinations.
   State Transition: Test account locking after multiple failed login attempts.
   Use Case Testing: Test the complete login process.
   Error Guessing: Try blank fields, special characters, spaces, and SQL-like input.
   ```

  - White box : Tests the application's internal code, logic, and structure with knowledge of its implementation.
    Example: Test every statement, condition, loop involved
    
  - Grey box : Tests the application with partial knowledge of its internal structure, combining elements of Black Box and White Box Testing.
    Example: Verify DB and API calls
    ```
    Regression
    Database
    API
    ```

### The 7 Core Principles of Software Testing
1. Testing shows the presence of defects, not their absence:
- The Concept: Testing can find bugs, but it can never prove that a system is 100% error-free.
- The Reality: Running a successful suite of tests only reduces the probability of remaining defects; it does not guarantee total correctness under all production environments.

2. Exhaustive testing is impossible:
- The Concept: Trying to test every single combination of inputs, preconditions, and user paths is structurally unachievable.
- The Reality: Except for trivial applications, the input permutations are infinite. Teams must rely on risk-based prioritization and equivalence partitioning to focus efforts where failure is most likely or most expensive.

3. Early testing saves time and money:
- The Concept: Often called "Shift-Left" testing, QA activities should begin as early as possible in the SDLC.
- The Reality: Finding a defect during requirement analysis or design reviews costs a fraction of what it costs to fix once the code is written, compiled, and deployed.

4. Defect clustering:
- The Concept: Bugs are not evenly distributed; instead, a small number of modules usually harbor the vast majority of application defects.
- The Reality: This heavily aligns with the Pareto Principle (the 80/20 rule), which states that roughly 80% of software bugs originate from 20% of the code modules.

5. Beware of the pesticide paradox:
- The Concept: If you repeatedly execute the exact same test cases, they will eventually stop finding new bugs.
- The Reality: Just as agricultural pests build up a resistance to a repeated pesticide, software changes render static test scripts blind to new errors. To counter this, tests must be continually reviewed, updated, and expanded.

6. Testing is context-dependent:
- The Concept: There is no universal "one size fits all" strategy for validating software.
- The Reality: A high-volume, safety-critical medical device or e-commerce checkout flow requires a completely different rigor, compliance checklist, and testing methodology than a basic informational landing page or personal blog.

7. Absence of errors fallacy:
- The Concept: Finding and fixing a high volume of bugs is irrelevant if the resulting system fails to meet user needs or business goals.
- The Reality: A piece of software can be 100% technically stable and clean, yet still be a failure if it provides a bad user experience or implements incorrect business requirements.


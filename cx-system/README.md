# CX System

CX refers to CI/CD, that is, Continuous Integration, Continuous Delivery,
Continuous Deployment

There are many services that provide some or all of these feature
1. Travis CI
2. Circle CI
3. GitLab CI/CD
4. GitHub Actions
5. Bamboo
6. Semaphore
7. GoCD
8. Drone CI

Things to discuss
1. Architecture of the system
2. How user interacts with the system
    - Input to run tasks like build, test, deploy
    - APIs for automation
3. Security
    - Assets
    - How to protect
4. Running different tasks
    - Showing logs
    - Handling failures
5. Handling scale
6. Storage
    - Artifacts
    - Logs
    - Expiry dates for data or archival strategies,
    to avoid accumulating lots of data.

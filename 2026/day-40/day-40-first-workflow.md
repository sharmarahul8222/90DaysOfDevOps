Task 1: Set Up
Create a new public GitHub repository called github-actions-practice?
- In the GitHub portal -> profile -> Repositories -> Click on New Button -> Enter the repository name and hit the create repository button.
  
Clone it locally?
- Clone repo using the git clone <repo url> command
  
Create the folder structure: .github/workflows/
- Go into repo with cd github-actions-practice
- mkdir -p .github/workflows


Task 2: Hello Workflow
Create .github/workflows/hello.yml with a workflow that:
Triggers on every push
Has one job called greet
Runs on ubuntu-latest
Has two steps:
Step 1: Check out the code using actions/checkout
Step 2: Print Hello from GitHub Actions!

- Created file .github/workflows/hello.yml
- name: Day 40 Task
  on:
    push:
  jobs:
    greet:
      runs-on: ubuntu-latest
      steps:
        - name: Checkout code
          run: echo "actions/checkout"
        - name: Say Hello
          run: echo "Hello from GitHub Actions!"

  Verify the running workflow <img width="1311" height="567" alt="image" src="https://github.com/user-attachments/assets/bcccf47a-38f4-4029-a090-b8b5b3f92a62" />


Task 3: Understand the Anatomy
Look at your workflow file and write in your notes what each key does:

- on: Defines the trigger event. In this case, the workflow runs every time there is a push to the repository.
- jobs: Defines one or more jobs that the workflow will execute. A workflow can have multiple jobs.
- runs-on: Specifies which virtual machine will run the job.
- steps: Defines a sequence of tasks inside a job. Steps run one by one in order or parallels.
- uses: Used to run a pre-built GitHub Action. This checks out the repository code onto the runner.
- run: Executes shell commands on the runner.
- name: (on a step) Gives a readable label to a step so it’s easier to understand in the Actions UI.


Task 4: Add More Steps
Update hello.yml to also:

Print the current date and time
Print the name of the branch that triggered the run (hint: GitHub provides this as a variable)
List the files in the repo
Print the runner's operating system
Push again — watch the new run.

- Updated Day 40 Task
  name: Hello Workflow
  on:
    push:
  jobs:
    greet:
      runs-on: ubuntu-latest
      steps:
        - name: Checkout code
          uses: actions/checkout@v4
        - name: Say Hello
          run: echo "Hello from GitHub Actions!"
        - name: Print date and time
          run: date
        - name: Print branch name
          run: echo "Branch: ${{ github.ref_name }}"
        - name: List files in repository
          run: ls -la
        - name: Print runner OS
          run: echo "Runner OS: $RUNNER_OS"


Task 5: Break It On Purpose
1. Add a step that runs a command that will fail (e.g., exit 1 or a misspelled command)?
    Added a failing step:
          - name: Break the pipeline
            run: exit 1
2. Push and observe what happens in the Actions tab
   After commiting the changes puipeline turned RED and the Job stopped immediately.

3. Fix it and push again
   As part of fixing removed the failing step and commit again. Now the pipeline turned geer again
   Screenshot: <img width="1311" height="567" alt="image" src="https://github.com/user-attachments/assets/bcccf47a-38f4-4029-a090-b8b5b3f92a62" />

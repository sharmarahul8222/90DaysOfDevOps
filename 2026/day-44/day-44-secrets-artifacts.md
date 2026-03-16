Task 1: GitHub Secrets
- Go to your repo → Settings → Secrets and Variables → Actions
- Create a secret called MY_SECRET_MESSAGE
- Create a workflow that reads it and prints: The secret is set: true (never print the actual value)
  #workflow
  name: Secrets Demo
  on:
      push:
          branches: [main]
  jobs: 
      Secrets-check:
          runs-on: ubuntu-latest
          steps:
              - name: Check if secrets exits
                run: echo "The secret is set true"
              - name: Printing Secrets Value
                run: echo "The secrets value is ${{ secrets.MY_SECRET_MESSAGE }}"
  
- Try to print ${{ secrets.MY_SECRET_MESSAGE }} directly — what does GitHub show?
  The secrets value is ***
  
- Write in your notes: Why should you never print secrets in CI logs?
  If a secret is printed in logs using ${{ secrets.SECRET_NAME }}, GitHub automatically masks the value and replaces it with *** to prevent exposure.
  Secrets should never be printed because:
  - Logs are visible to repository collaborators
  - Logs may be stored for a long time
  - Attackers could steal credentials
  - Secrets may contain sensitive data like:  API keys, Cloud credentials, Database passwords, Tokens

Task 1: Your First Playbook
- Create install-nginx.yml
- Run it: ansible-playbook install-nginx.yml
  <img width="1848" height="541" alt="image" src="https://github.com/user-attachments/assets/3ac01baf-5f3e-4ef5-8344-722f78e95b88" />


Task 2: Understand the Playbook Structure
- What is the difference between a play and a task?
  A play is a collection of tasks applied to a group of hosts.
  A task is a single unit of work executed using a module.
  
- Can you have multiple plays in one playbook?
  Yes, a playbook can contain multiple plays.
  
- What does become: true do at the play level vs the task level?
  At play level: All tasks run with elevated privileges (sudo)
  At task level: Only that specific task runs with elevated privileges
  
- What happens if a task fails -- do remaining tasks still run?
  If a task fails, Ansible stops executing remaining tasks for that host.


Task 3: Learn the Essential Modules
Practice each of these modules by writing a playbook called essential-modules.yml with multiple tasks:
- yum/apt -- Install and remove packages
- service -- Manage services
- copy -- Copy files from control node to managed nodes
- file -- Create directories and manage permissions
- command -- Run a command (no shell features)
- shell -- Run a command with shell features (pipes, redirects)
- lineinfile -- Add or modify a single line in a file
  <img width="1311" height="592" alt="image" src="https://github.com/user-attachments/assets/af7b504c-df93-4e46-8ca7-8e59ffb31152" />


Task 4: Handlers -- Restart Services Only When Needed
Handlers are tasks that run only when triggered by a notify. This avoids unnecessary service restarts.
- Create nginx-config.yml
- Create files/nginx.conf with a basic Nginx config.
- Run the playbook:
  - First run: handler triggers because the config file is new
  - Second run: handler does NOT trigger because nothing changed
  - Verify: Run it twice and compare the output. Does the handler run both times?
<img width="1850" height="572" alt="image" src="https://github.com/user-attachments/assets/71e27199-d785-4c08-861e-305dcd5f6bf7" />


Task 5: Dry Run, Diff, and Verbosity
Before running playbooks on production, always preview changes first.
- Dry run (check mode) -- shows what would change without changing anything:
  <img width="1327" height="528" alt="image" src="https://github.com/user-attachments/assets/5b0f577e-9f4b-498a-b8c8-6717eb3a81e6" />

- Diff mode -- shows the actual file differences:
  <img width="1326" height="515" alt="image" src="https://github.com/user-attachments/assets/6adfd772-f711-407b-9321-e03b873f696b" />

- Verbosity -- increase output detail for debugging:
  <img width="1147" height="257" alt="image" src="https://github.com/user-attachments/assets/31630564-7396-4cf6-b0dd-61a7104c02f0" />

- Limit to specific hosts:
  <img width="1317" height="507" alt="image" src="https://github.com/user-attachments/assets/7fbbfed9-ecaf-41ed-a63b-b2d1ea038413" />

- List what would be affected without running:
  <img width="1111" height="426" alt="image" src="https://github.com/user-attachments/assets/6dbe67a0-ff25-446f-a048-3a15b44f1e58" />


Task 6: Multiple Plays in One Playbook
- Write multi-play.yml with separate plays for each server group:
- Run it: ansible-playbook multi-play.yml
  <img width="1447" height="473" alt="image" src="https://github.com/user-attachments/assets/fc3085b4-165e-4772-8b40-40083b159258" />









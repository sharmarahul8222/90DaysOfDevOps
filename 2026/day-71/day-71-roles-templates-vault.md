Task 1: Jinja2 Templates
Templates let you generate config files dynamically using variables and facts.
- Create templates/nginx-vhost.conf.j2:
- Create a playbook template-demo.yml:
- Run it with --diff to see the rendered template: ansible-playbook template-demo.yml --diff
  <img width="1036" height="596" alt="image" src="https://github.com/user-attachments/assets/25ccc41e-f283-41a6-9a45-4164b0c35ea7" />

- Verify: SSH into the web server and read the generated config. Are the variables replaced with actual values?


Task 2: Understand the Role Structure
- An Ansible role has a fixed directory structure.
- Every directory contains a main.yml that Ansible loads automatically. You only create the directories you need.
- Generate a skeleton with: ansible-galaxy init roles/webserver
- Explore the generated directory. Read the README.md that Galaxy creates.
  <img width="928" height="61" alt="image" src="https://github.com/user-attachments/assets/38f43e93-1b15-4a66-b515-70bba5a999c0" />

- Document: What is the difference between vars/main.yml and defaults/main.yml?
  - The difference between vars/main.yml and defaults/main.yml is based on variable precedence.
  - defaults/main.yml contains default values for variables and has the lowest priority. These variables are designed to be easily overridden by users, playbooks, or inventory variables.
  - vars/main.yml contains variables with higher priority. These are typically used for internal role configuration and are harder to override.
  - In practice, defaults are used for configurable values, while vars are used for fixed values that should not change frequently.


Task 3: Build a Custom Webserver Role
- Build a complete webserver role from scratch:
  - roles/webserver/defaults/main.yml
  - roles/webserver/tasks/main.yml:
  - roles/webserver/handlers/main.yml
  - roles/webserver/templates/index.html.j2:
- Create the vhost.conf.j2 and nginx.conf.j2 templates yourself based on what you learned in Task 1.
- Now call the role from a playbook site.yml:
- Run it: ansible-playbook site.yml
  <img width="1345" height="490" alt="image" src="https://github.com/user-attachments/assets/b4434931-bec4-4901-aa93-753072fd6991" />

- Verify: Curl the web server. Does the custom page load?
    Yes, after running the playbook, the Nginx web server was successfully configured using the custom role. The application page loads correctly when accessed via the server’s public IP, confirming that templates, variables, and handlers are working as expected.

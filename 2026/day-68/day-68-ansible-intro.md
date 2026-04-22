Task 1: Understand Ansible
- What is configuration management? Why do we need it?
  Configuration management is the process of automating the setup, configuration, and maintenance of servers so they always stay in a desired state. Instead of manually installing software, editing files, and fixing issues on each machine, we define everything in code and let tools handle it.
  We need it because manual setup is slow, error-prone, and inconsistent. With configuration management, we get consistency across environments, faster deployments, easy scaling, and repeatability, which are critical in DevOps.
  
- How is Ansible different from Chef, Puppet, and Salt?
  Ansible is different because it is simple, agentless, and uses YAML-based playbooks, making it easier to learn and use. Tools like Chef and Puppet require agents to be installed on every server and use more complex languages (Ruby-based DSLs). Salt can work both agent-based and agentless but is more complex.
  
- What does "agentless" mean? How does Ansible connect to managed nodes?
  Agentless means you don’t need to install any software on the target servers. Ansible connects to managed nodes using SSH.
  It logs into the machine, runs tasks, and exits — no background agent required.

- Draw or describe the Ansible architecture:
  Control Node  --->  Managed Nodes
       |
       | uses
       v
   Inventory + Playbooks + Modules
  
  - Control Node -- the machine where Ansible runs (your laptop or a jump server)
  - Managed Nodes -- the servers Ansible configures (your EC2 instances)
  - Inventory -- the list of managed nodes
  - Modules -- units of work Ansible executes (install a package, copy a file, start a service)
  - Playbooks -- YAML files that define what to do on which hosts.
 

Task 2: Set Up Your Lab Environment
- Use Terraform (recommended -- you just learned this) Use your TerraWeek skills to provision 3 EC2 instances.
- Verify you can SSH into each one from your control node:
  - ssh -i ~/your-key.pem ec2-user@<public-ip-1>
  - ssh -i ~/your-key.pem ec2-user@<public-ip-2>
  - ssh -i ~/your-key.pem ec2-user@<public-ip-3>
  <img width="901" height="362" alt="image" src="https://github.com/user-attachments/assets/aaaccb4b-6c7e-4caa-8c9b-393ecd863f9b" />
  <img width="1125" height="530" alt="image" src="https://github.com/user-attachments/assets/7ba8a284-4d7a-4e60-9fd7-90b619407fbc" />


Task 3: Install Ansible
- Install Ansible on your control node (your laptop or one dedicated EC2 instance)
- Confirm the output shows the Ansible version, config file path, and Python version.
- Document: On which machine did you install Ansible? Why is it only needed on the control node?
  I installed Ansible on my control node, which is a dedicated Ubuntu EC2 instance (ansible-server). Ansible is only required on the control node because it         operates in an agentless manner. It connects to managed nodes over SSH and executes tasks remotely without requiring any software installation on those nodes.     This simplifies setup and reduces overhead compared to other configuration management tools.
  <img width="1387" height="265" alt="image" src="https://github.com/user-attachments/assets/741e51d5-ade2-4695-9cf2-0c252ced1514" />

Task 4: Create Your Inventory File
- The inventory tells Ansible which servers to manage. Create a project directory and your first inventory:
- mkdir ansible-practice && cd ansible-practice
- Create a file called inventory.ini:
- Verify Ansible can reach all hosts:
  <img width="1850" height="577" alt="image" src="https://github.com/user-attachments/assets/442c721e-b55b-49df-9d58-27f54a67efdc" />


Task 5: Run Ad-Hoc Commands
<img width="1845" height="686" alt="image" src="https://github.com/user-attachments/assets/3981449b-792b-49b1-9494-adfba493dfe6" />

Task 6: Explore Inventory Groups and Patterns
- Create a group of groups -- add this to your inventory.ini:
- Run commands against different groups
- Create an ansible.cfg to avoid typing -i inventory.ini every time:
  <img width="1833" height="767" alt="image" src="https://github.com/user-attachments/assets/2420d7f6-37db-43c9-a63a-9f2752f1ef0c" />

  <img width="1846" height="610" alt="image" src="https://github.com/user-attachments/assets/fe3618a3-11ed-4eff-a1a2-a371aeeda21d" />









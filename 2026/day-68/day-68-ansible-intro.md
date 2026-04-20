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
 


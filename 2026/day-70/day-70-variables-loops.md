Task 1: Variables in Playbooks
- Create variables-demo.yml:
- Run it and verify the variables resolve correctly.
- Now, override a variable from the command line:
  <img width="1297" height="565" alt="image" src="https://github.com/user-attachments/assets/0da25ea8-62af-40cd-baed-6b28f0ae84dd" />


Task 2: group_vars and host_vars
Variables should not live inside playbooks. Move them to dedicated files.
- Create this structure:
  - group_vars/all.yml -- applies to every host
  - group_vars/web.yml -- applies only to the web group
  - group_vars/db.yml -- applies only to the db group
  - host_vars/web-server.yml -- applies only to this specific host
- Write a playbook site.yml that uses these variables:
- Run it and observe which variables apply to which hosts.
  <img width="1293" height="432" alt="image" src="https://github.com/user-attachments/assets/8dc748e5-49d4-47d4-acaa-db14af9bb8fe" />

Document: What is the variable precedence? (hint: host_vars > group_vars > playbook vars, and -e overrides everything)
  - In this task, I moved variables out of the playbook into group_vars and host_vars directories, which is the recommended approach in Ansible for better organization and reusability.
  - Variables defined in group_vars/all.yml apply to all hosts, while group-specific variables (group_vars/web.yml, group_vars/db.yml) apply only to their respective groups. Host-specific variables in host_vars/web-server.yml override group-level variables when there is a conflict.
  - I observed that the max_connections value defined in host_vars (2000) overrides the value from group_vars (1000), demonstrating variable precedence.
  - The variable precedence order is: group_vars < playbook vars < host_vars < CLI variables (-e), with CLI variables having the highest priority.


Task 3: Ansible Facts -- Gathering System Information
Ansible automatically collects "facts" about each managed node -- OS, IP, memory, CPU, disks, and hundreds more.
- See all facts for a host: ansible web-server -m setup
- Filter specific facts: 
  -  ansible web-server -m setup -a "filter=ansible_os_family"
  - ansible web-server -m setup -a "filter=ansible_distribution*"
  - ansible web-server -m setup -a "filter=ansible_memtotal_mb"
  - ansible web-server -m setup -a "filter=ansible_default_ipv4"
- Use facts in a playbook -- create facts-demo.yml:
- Run it and observe the facts printed for each host.
<img width="1363" height="585" alt="image" src="https://github.com/user-attachments/assets/1710badc-f54e-49aa-ad6b-baffe236df1a" />

- Document: Name five facts you would use in real playbooks and why.
    Ansible facts are automatically gathered system information about managed nodes, including operating system details, memory, network interfaces, and hardware configuration. These facts allow playbooks to adapt dynamically based on the target system.
    Five useful facts in real-world playbooks are:
        1. ansible_os_family – Used to determine the operating system type (e.g., RedHat, Debian) to install the correct packages using yum or apt.
        2. ansible_distribution – Provides the exact OS name (e.g., Amazon Linux, Ubuntu), useful for OS-specific configurations.
        3. ansible_memtotal_mb – Helps decide resource allocation or whether a server meets minimum requirements.
        4. ansible_default_ipv4.address – Used to configure services or generate dynamic configuration files with the correct IP address.
        5. ansible_hostname – Useful for logging, monitoring, and creating host-specific configurations or identifiers.
    These facts enable writing flexible and portable automation that works across different environments.
    

Task 4: Conditionals with when
Tasks should not always run on every host. Use when to control execution.
- Create conditional-demo.yml
- Run it and observe which tasks are skipped on which hosts.
  <img width="1303" height="452" alt="image" src="https://github.com/user-attachments/assets/4aa486f7-71c7-493b-abb5-eb229d2dc645" />

- Verify: Are tasks correctly skipping on hosts that don't match the condition?
  - In this task, I used the "when" condition to control task execution based on host group, system facts, and variables. Tasks such as installing Nginx and MySQL were executed only on their respective server groups using group_names. System facts like ansible_memtotal_mb and ansible_distribution were used to apply logic based on memory and operating system.
  - I also implemented logical conditions using AND and OR operators to combine multiple checks. During execution, tasks that did not meet the conditions were skipped, demonstrating how Ansible ensures targeted and efficient automation.


Task 5: Loops
- Create loops-demo.yml
- Run it and observe the loop output -- each iteration is shown separately.
  <img width="1037" height="568" alt="image" src="https://github.com/user-attachments/assets/61a2a137-3306-4c7f-ad8e-3756dca333a7" />
  
- Document: What is the difference between loop and the older with_items? (hint: loop is the modern recommended syntax)
    - The loop keyword in Ansible is used to iterate over a list of items and execute a task multiple times. It is the modern and recommended syntax for looping in Ansible.
    - The older syntax, with_items, was previously used for iteration but is now considered deprecated. The loop keyword is more consistent, flexible, and works better with newer features like loop_control and advanced data structures.
    - In summary, loop is preferred over with_items because it provides cleaner syntax, better readability, and improved functionality.


Task 6: Register, Debug, and Combine Everything
- Build a real-world playbook server-report.yml that combines variables, facts, conditionals, and register:
- Run it and verify the report file is created on each server.
  <img width="1038" height="483" alt="image" src="https://github.com/user-attachments/assets/54b9d883-b2ff-4852-9472-e3fd725822e5" />

- Verify: SSH into a server and read /tmp/server-report-*.txt. Does it contain accurate information?
    - Yes, the report file is created successfully on each server under /tmp. It contains accurate system information including hostname, OS version, IP address, RAM, disk usage, and timestamp, confirming that the playbook correctly gathers and writes system data.



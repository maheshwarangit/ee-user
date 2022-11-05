---    
- name: Working with file modeules
  hosts: dbserver
  tasks:
   - name: Creating a directory
     ansible.builtin.file:
      path: /root/ans_dir/
      state: directory
      owner: student
      group: devops
      setype: samba_share_t
   - name: create a file
     ansible.builtin.file:
      path: /root/ans_dir/ans_file
      state: touch
   - name: Copy a content
     ansible.builtin.copy:
      content: "Workstation is a Control node"
      dest: /etc/issue
   - name: copy a file
     ansible.builtin.copy:
      src: ansible.cfg     # control node 
      dest: /root/ans_dir/ # managed node
   - name: fetch the file
     ansible.builtin.fetch:
      src: /etc/hostname   # managed node 
      dest: Host-name      # control node
   - name: Add Block of line in a file
     ansible.builtin.blockinfile:
      block: |
       Welcome to Red Hat Ansible Course
       This Course is Full of ansible basics
       Course code is RH294 and the Exam code EX294
      path: /root/ans_dir/ans_file
      state: present
   - name: Add a Line in file
     ansible.builtin.lineinfile:
      line: "Ansible is a Best Tool for Automation"
      path: /root/ans_dir/ans_file
   - name: Replace a line in a file
     ansible.builtin.lineinfile:
      line: This Course is provided by Red Hat
      regexp: '^This Course is Full of ansible basics'
      path: /root/ans_dir/ans_file
   - name: Retrive the information
     ansible.builtin.stat:
      path: /root/ans_dir/ans_file
      checksum_algorithm: md5
   - name: Sync the file content
     ansible.builtin.synchronize:
      src: inventory
      dest: /etc/redhat-release

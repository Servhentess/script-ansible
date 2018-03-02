---
- name: Copy d'un fichier fact vers remote
  hosts: all
  become: true

  tasks:

  - name: Create path to copy
    file:
      path: /etc/ansible/facts.d
      state: directory
      mode: 0755

  - name: Copy
    copy:
      src: /etc/ansible/mes_scripts/copy.fact
      dest: /etc/ansible/facts.d

  - name: do facts module to get latest information
    setup:

  - name: View
    debug: msg={{ ansible_local }}

  - name: Del fact file
    file:
      path: /etc/ansible/facts.d/copy.fact
      state: absent

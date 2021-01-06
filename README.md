## KU-Cybersecurity-Bootcamp
# Automated ELK Stack Deployment

This was the ELK Stack Deployment I built in Microsoft Azure during KU CyberSecurity Bootcamp.
The files in this repository were used to configure the network depicted below.

![Network](https://user-images.githubusercontent.com/70439871/103699510-ac3ffd80-4f68-11eb-8e6d-915bbad76936.png)

The following files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YAML file may be used to install only certain pieces of it, such as Filebeat.




```
# install_elk.yml
- name: Configure Elk VM with Docker
  hosts: elkserver
  remote_user: bradyw
  become: true
  tasks:
    # Use apt module
    - name: Install docker.io
      apt:
        update_cache: yes
        name: docker.io
        state: present

      # Use apt module
    - name: Install pip3
      apt:
        force_apt_get: yes
        name: python3-pip
        state: present

      # Use pip module
    - name: Install Docker python module
      pip:
        name: docker
        state: present

      # Use command module
    - name: Increase virtual memory
      command: sysctl -w vm.max_map_count=262144

      # Use sysctl module
    - name: Use more memory
      sysctl:
        name: vm.max_map_count
        value: "262144"
        state: present
        reload: yes

      # Use docker_container module
    - name: download and launch a docker elk container
      docker_container:
        name: elk
        image: sebp/elk:761
        state: started
        restart_policy: always
        published_ports:
          - 5601:5601
          - 9200:9200
          - 5044:5044
  ```
    

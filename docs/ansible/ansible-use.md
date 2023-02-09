# Use a Ansible-playbook

![ansible](../img/ansible.png)

??? example "Find the right folder"

    ### Find the right folder
    This will be the "root" folder for Ansible.
    ```
    cd /etc/ansible
    ```

??? warning "Use SSH without having to type in the password"

    ### Use SSH without having to type in the password
    First "Read" your SSH key.
    ```
    eval `ssh-agent`
    ```
    and then "Load" your SSH key with your password.
    ```
    ssh-add
    ```

??? success "Use your playbooks"

    ### Use your playbooks 
    First make sure you are in the same folder as the playbook you want to use.

    Then write:
    ```
    ansible-playbook Win-Test-Env.yaml
    ```


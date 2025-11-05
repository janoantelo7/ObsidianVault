---
tags:
  - automatización
  - ansible
---
# Qué é?
Os playbooks de [[Apuntes/Ansible/01 - Introducción#Qué é?|Ansible]] son arquivos YAML que describen as tarefas que se deben executar nos hosts xestionados. Permiten automatizar configuracións e implementacións de maneira eficiente e reproducible.

Un exemplo de playbook básico é o seguinte:
```yaml
---
- name: Config apache
  hosts: test
  gather_facts: true
  remote_user: jano
  become: true

  tasks:
    - name: install apache
      ansible.builtin.dnf:
        name: httpd
        state: latest
    
```

Para aplicar o seguinte playbook debemos utilizar o seguinte comando
```bash
ansible-playbook playbook.yml -K
```
O parámetro `-K`  indica que pregunte pola contraseña de become.

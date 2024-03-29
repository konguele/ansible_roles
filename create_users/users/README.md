Role Name
=========

Creación y modificación de usuarios

el funcionamiento es sencillo, creamos los usuarios en el fichero users.yml y ejecutamos el comando ansible-playbook -i ../inventario/inv1 users.yml

las caracteristicas que pueden tener los usuarios son las siguientes:

vars:
    users:
      - username: root
        home: /root
        group: root
        authorized_keys:
          - "{{ lookup('file', 'tests/id_rsa.pub') }}"
        user_create: no
      - username: foobar
        name: Foo Bar 1
      - username: foobar_authorized_keys
        authorized_keys:
          - "{{ lookup('file', 'tests/id_rsa.pub') }}"
        home_create: yes
      - username: foobar_nohome
        home_create: no
      - username: foobar_groups
        groups:
          - users
        append: yes
      - username: foobar_groups_reset
        groups: []
        group: foobar_groups_reset
      - username: foobar_home_mode
        home_mode: "0750"
      - username: foobar_key
        ssh_key: "{{ lookup('file', 'tests/id_rsa') }}"
      - username: foobar_keys
        ssh_keys:
          id_rsa_1: "{{ lookup('file', 'tests/id_rsa') }}"
          id_rsa_2: "{{ lookup('file', 'tests/id_rsa') }}"
      - username: foobar_key_generate
        ssh_key_generate: yes
        ssh_key_password: secret
      - username: foobar_system
        system: yes
      - username: foobar_file
        home_files:
          - "tests/.bashrc"
    users_group: staff
    users_groups:
      - www-data
    users_authorized_keys_exclusive: yes
    users_remove:
    - foobar
    - { username: foobar_key, remove: no }
    - { username: foobar_authorized_keys, remove: yes }

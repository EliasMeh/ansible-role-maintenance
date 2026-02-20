ansible-role-maintenance
========================

Déploie une page de maintenance dynamique via NGINX sur des serveurs Ubuntu/Debian et Rocky Linux/RedHat.

Le rôle installe et démarre NGINX, supprime la page par défaut, puis génère une page de maintenance HTML personnalisée à partir d'un template Jinja2 contenant le nom de l'application, la date de fin de maintenance et un email de contact.

Requirements
------------

- Ansible 2.9+
- Accès `become` (sudo) sur les machines cibles
- Pas de prérequis supplémentaire : NGINX est installé par le rôle

Role Variables
--------------

Variables définies dans `vars/main.yml` (surchargeables) :

| Variable         | Valeur par défaut                  | Description                          |
|------------------|------------------------------------|--------------------------------------|
| `nom_app`        | `"Quiz Ansible"`                   | Nom de l'application en maintenance  |
| `fin_maintenance`| `"20 février 2026 à 08h00"`        | Date/heure de fin de maintenance     |
| `email_contact`  | `"admin@quiz-ansible.lab"`         | Email de contact affiché sur la page |

Variables Ansible utilisées automatiquement :

- `ansible_hostname` — nom de la machine affiché sur la page
- `ansible_distribution` — distribution Linux
- `ansible_date_time.date` — date du déploiement
- `ansible_os_family` — détermine apt/dnf et la gestion de NGINX

Dependencies
------------

Aucune dépendance externe.

Example Playbook
----------------

```yaml
- hosts: all
  become: true
  roles:
    - role: EliasMeh.maintenance

# Surcharger les variables :
- hosts: all
  become: true
  roles:
    - role: EliasMeh.maintenance
      vars:
        nom_app: "Mon Application"
        fin_maintenance: "25 février 2026 à 10h00"
        email_contact: "support@example.com"
```

Compatibilité
-------------

| OS               | Testé |
|------------------|-------|
| Ubuntu 22.04     | ✅    |
| Ubuntu 24.04     | ✅    |
| Rocky Linux 9    | ✅    |

> **Note :** Sur Rocky Linux en conteneur Docker (sans systemd), NGINX est démarré directement via la commande `nginx` au lieu du service systemd.

License
-------

MIT

Author Information
------------------

EliasMeh — [github.com/EliasMeh](https://github.com/EliasMeh)

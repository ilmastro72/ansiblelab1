# Lab 1 — Primi playbook

**Corso GitOps / Ansible — Prima sessione**

## Obiettivo

Configurare un webserver nginx su una VM Linux usando Ansible:
- Installare e avviare nginx
- Deployare una pagina HTML generata da template Jinja2
- Gestire variabili con `group_vars` e segreti con `ansible-vault`

## Prerequisiti

- Ansible >= 2.14 installato sul control node
- `ansible-lint` installato (`pip install ansible-lint`)
- VM Linux raggiungibile via SSH
- Chiave SSH configurata in `~/.ssh/id_rsa`

## Setup rapido

```bash
# 1. Clona il repo
git clone <url-repo>
cd lab1/

# 2. Configura l'IP della tua VM
vim inventory/hosts.ini   # sostituisci <IP_VM>

# 3. Verifica connessione
ansible all -m ping

# 4. Crea il vault (Task 5)
ansible-vault create group_vars/all/vault.yml
# Inserisci: vault_db_password: "SuperSecret123"

# 5. Decommenta la riga db_password in group_vars/all/vars.yml
```

## Esecuzione

```bash
# Run completo
ansible-playbook playbook.yml --ask-vault-pass

# Dry run (senza modifiche)
ansible-playbook playbook.yml --check --diff

# Solo task di deploy
ansible-playbook playbook.yml --tags deploy --ask-vault-pass

# Lint
ansible-lint playbook.yml
```

## Struttura

```
lab1/
├── ansible.cfg                  # configurazione progetto
├── inventory/
│   └── hosts.ini                # inventario VM
├── group_vars/
│   └── all/
│       ├── vars.yml             # variabili in chiaro
│       └── vault.yml            # segreti cifrati (da creare)
├── templates/
│   └── index.html.j2            # template pagina HTML
├── playbook.yml                 # playbook principale
├── .ansible-lint                # configurazione lint
├── .gitignore
└── README.md
```

## Branch

| Branch     | Descrizione                              |
|------------|------------------------------------------|
| `main`     | Struttura iniziale (punto di partenza)   |
| `solution` | Soluzione completa (non aprire prima!)   |

## Documentazione

- [Ansible docs](https://docs.ansible.com)
- [Moduli builtin](https://docs.ansible.com/ansible/latest/collections/ansible/builtin)
- [Ansible Vault](https://docs.ansible.com/ansible/latest/vault_guide)

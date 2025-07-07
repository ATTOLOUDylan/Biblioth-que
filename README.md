# 📚 Bibliothèque Console (Python + SQLite)

Une application Python simple en mode **console** pour gérer une petite bibliothèque.  
Elle permet d’ajouter des livres, d’emprunter et de rendre, de créer des comptes utilisateurs, et dispose d’un **compte administrateur unique** pour la gestion des livres.

---

## 🚀 Fonctionnalités

- 📘 Ajouter un livre *(admin uniquement)*
- 📖 Lister les livres disponibles
- 🔍 Rechercher un livre par titre ou auteur
- 🧑‍💻 Créer un compte utilisateur
- 🔐 Se connecter
- 📥 Emprunter un livre
- 📤 Rendre un livre
- 🔁 Changer son mot de passe
- 🔑 Gestion d’un seul compte administrateur
- 💾 Données stockées en base **SQLite (bibliotheque.db)**

---

## 🛠️ Technologies utilisées

- Python 3.x
- SQLite (intégré via le module `sqlite3`)
- `getpass` pour sécuriser la saisie des mots de passe
- Aucune bibliothèque externe

---

## 📁 Arborescence du projet

```plaintext
bibliotheque/
├── Bibliothèque.py         # Menu principal
├── db.py                   # Création de la base de données
├── livre.py                # Gestion des livres
├── utilisateur.py          # Gestion des utilisateurs
├── compte.py               # Menu utilisateur connecté
├── admin_creator.py        # Script pour créer/modifier le compte admin
├── bibliotheque.db         # Fichier SQLite (généré automatiquement)
└── README.md               # Documentation du projet

```

---

## ▶️ Comment exécuter l'application

1. Ouvre un terminal.
2. Va dans le dossier du projet avec :
```bash
   cd chemin/vers/le/dossier/bibliotheque 
    
   python3 bibliothèque.py
   
   EX: dylan@dylan-Latitude-E5540:~$ cd bibliothèque
       dylan@dylan-Latitude-E5540:~/bibliothèque$ python3 bibliothèque.py
   📝 Assure-toi d’avoir Python 3.x installé sur ton ordinateur
  ---
```
## 👤 Compte Administrateur

Par défaut, l’application fonctionne avec **un seul compte admin**.  
Ce compte est **le seul autorisé à ajouter des livres**.

---

### 🔐 Informations par défaut

| Email           | Mot de passe | Rôle  |
|----------------|--------------|-------|
| `admin@bib.bj` | `admin2005`  | Admin |

---

### 🛠️ Modifier ou recréer le compte admin

Si tu veux **changer l'email ou le mot de passe** de l’admin, utilise le fichier :

📄 `admin_creator.py`

```python
import sqlite3

def creer_admin():
    conn = sqlite3.connect("bibliotheque.db")
    cur = conn.cursor()

    # Supprime l’ancien compte admin s’il existe
    cur.execute("DELETE FROM utilisateurs WHERE email = 'admin@bib.bj'")

    # Crée un nouveau compte admin (modifiable ici)
    cur.execute("""
        INSERT INTO utilisateurs (nom, email, mot_de_passe, is_admin)
        VALUES (?, ?, ?, 1)
    """, ("Administrateur", "admin@bib.bj", "admin2005"))

    conn.commit()
    conn.close()
    print("✅ Admin mis à jour avec succès.")

if __name__ == "__main__":
    creer_admin()
```
---

### 💡 Modifier l’email ou le mot de passe

Change simplement l’adresse email ou le mot de passe directement dans le fichier `admin_creator.py` :

```python
# Exemple à modifier :
cur.execute("""
    INSERT INTO utilisateurs (nom, email, mot_de_passe, is_admin)
    VALUES (?, ?, ?, 1)
""", ("Administrateur", "admin@bib.bj", "admin2005"))
```
## 👤 Auteur

- **Dylan** – Développeur du projet

---

## 📜 Licence

Ce projet est sous licence MIT.  
📄 [Voir la licence complète ici](./LICENCE)


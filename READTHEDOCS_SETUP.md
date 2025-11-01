# 📚 Configuration Read the Docs

## Étapes pour publier la documentation

### 1. Créer un compte Read the Docs

1. Allez sur https://readthedocs.org/
2. Cliquez sur "Sign Up"
3. Connectez-vous avec votre compte GitHub

### 2. Importer le projet

1. Une fois connecté, cliquez sur "Import a Project"
2. Sélectionnez le repo **pixcorndoc** dans la liste
3. Cliquez sur le bouton "+" à côté du repo

### 3. Configuration du projet

**Nom du projet**: `pixcorn-api-docs`

**Repository URL**: `https://github.com/maliciouuus/pixcorndoc`

**Default branch**: `main`

Cliquez sur "Next"

### 4. Configuration avancée (optionnel)

Dans les paramètres du projet (Admin → Advanced Settings):

- **Programming Language**: Python
- **Python Interpreter**: CPython 3.11
- **Requirements file**: `requirements.txt`
- **Documentation type**: Sphinx Html

### 5. Build automatique

Read the Docs va automatiquement:
- Détecter le fichier `.readthedocs.yaml`
- Installer les dépendances depuis `requirements.txt`
- Builder la documentation avec Sphinx
- Publier sur `https://pixcorn-api-docs.readthedocs.io/`

### 6. Domaine personnalisé (optionnel)

Pour utiliser `docs.pixcorn.com`:

1. Dans Read the Docs: Admin → Domains → Add Domain
2. Ajoutez `docs.pixcorn.com`
3. Configurez le DNS:
   ```
   CNAME docs.pixcorn.com → pixcorn-api-docs.readthedocs.io
   ```

### 7. Badge (optionnel)

Ajoutez un badge dans le README principal:

```markdown
[![Documentation Status](https://readthedocs.org/projects/pixcorn-api-docs/badge/?version=latest)](https://pixcorn-api-docs.readthedocs.io/)
```

## 🔄 Mises à jour automatiques

Chaque push sur `main` déclenchera automatiquement un rebuild de la documentation sur Read the Docs!

## 🌐 URL de la documentation

Une fois configuré, votre documentation sera disponible sur:

**https://pixcorn-api-docs.readthedocs.io/**

## 📝 Modifier la documentation

1. Modifiez les fichiers `.rst` dans le repo
2. Commit et push
3. Read the Docs rebuild automatiquement
4. La doc est mise à jour en ~2 minutes

## ✅ C'est tout!

Votre documentation API est maintenant publique et professionnelle! 🚀


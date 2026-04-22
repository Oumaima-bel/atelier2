# Atelier 2 : Gestion et récupération de données

Réalisé par: Oumaima Belhaddad et Kaka Fatima Zahra

Ce tp est une application web développée avec **Django** dans le cadre du module *Développement Web Python*.
L’objectif est de manipuler les **modèles**, **relations**, **vues**, et **templates** afin de gérer des produits et leurs catégories. 

---

## Objectifs du TP

* Comprendre le fonctionnement de l’ORM Django
* Créer et manipuler des modèles (`Product`, `Category`)
* Gérer les relations entre modèles (ForeignKey)
* Implémenter des vues et routes
* Créer des templates pour l’affichage des données
* Gérer l’upload d’images avec Pillow

---

## Structure du projet

```bash
ecommerce/
│
├── ecommerce/        # Configuration principale (settings, urls...)
├── products/         # Application principale
│   ├── models.py
│   ├── views.py
│   ├── urls.py
│   ├── templates/
│   │   └── products/
│   │       ├── product_list.html
│   │       ├── product_detail.html
│   │       ├── category_list.html
│   │       └── category_detail.html
│
├── images/
│   └── products/     # Images uploadées
│
└── db.sqlite3
```

---

## Modèles

### Product

* name : CharField
* description : TextField
* price : DecimalField
* image : ImageField
* category : ForeignKey (Category)

### Category

* name : CharField
* description : TextField

Relation : **une catégorie → plusieurs produits** (ForeignKey) 

---

## Migrations

```bash
python manage.py makemigrations
python manage.py migrate
```

---

## Lancer le serveur

```bash
python manage.py runserver
```

Puis ouvrir :

```
http://127.0.0.1:8000/products/
```

---

## Gestion des images

Dans `settings.py` :

```python
MEDIA_ROOT = BASE_DIR / 'images'
MEDIA_URL = '/media/'
```

Dans `urls.py` principal :

```python
from django.conf import settings
from django.conf.urls.static import static

urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
```

---

## Routes principales

* `/products/` → liste des produits
* `/products/<id>/` → détail produit
* `/categories/` → liste des catégories
* `/categories/<id>/` → détail catégorie

---

## Base de données 

Par défaut : **SQLite**

Pour utiliser **MySQL** :

1. Créer une base `db_ecommerce`
2. Installer :

```bash
pip install mysqlclient
```

3. Modifier `DATABASES` dans `settings.py`


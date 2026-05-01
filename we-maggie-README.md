# 🎂 WE Maggie — Application d'organisation de séjour

Application web mono-page créée pour organiser le **weekend d'anniversaire de Maggie à Jaujac (Ardèche), du 7 au 10 mai 2026**. L'app est partagée entre toutes les participantes et synchronise les données en temps réel via **Firebase Realtime Database**.

---

## 🎯 Contexte du projet

12 amies se retrouvent pour fêter l'anniversaire de Maggie dans un gîte en Ardèche. L'application centralise tout ce dont elles ont besoin : renseigner leurs infos de participation, consulter le programme, suivre les finances, et s'organiser pour le ménage du départ.

---

## ✨ Fonctionnalités

| Onglet | Description |
|---|---|
| 👩 **Participantes** | Fiche individuelle dépliable par personne (arrivée, transport, activités, massage, départ, notes) |
| 📅 **Programme** | Agenda complet du weekend (jeudi → dimanche) avec horaires et adresses |
| 💰 **Finances** | Tableau récapitulatif des montants dus par personne, avec suivi des paiements cellule par cellule |
| 🍽️ **Menu Resto** | Carte complète du Bistrot du Jardin pour le dîner du vendredi |
| 📍 **Infos pratiques** | Contacts, adresses, répartition des chambres, zone de notes libres |
| 🧹 **Ménage** | Inscriptions pour le ménage du gîte le dimanche, avec récapitulatif |
| 🎒 **À emporter** | Checklist de bagages à cocher avant le départ |

**Fonctionnalités techniques :**
- 🔄 Synchronisation en temps réel via **Firebase Realtime Database**
- 💾 Sauvegarde automatique avec debounce (600ms après la dernière modification)
- 📱 Interface responsive, navigation par onglets scrollable sur mobile
- 🔔 Toast de confirmation à chaque sauvegarde

---

## 🗂️ Structure du projet

```
we-maggie/
└── index.html   # Fichier unique — HTML, CSS et JS intégrés
```

Projet **mono-fichier** pour faciliter le partage et le déploiement.

---

## 🛠️ Configuration Firebase

L'application utilise Firebase Realtime Database. La configuration est en haut du script JS :

```javascript
const FB_URL = 'https://we-maggie-default-rtdb.europe-west1.firebasedatabase.app/state.json';
```

> ⚠️ Pour réutiliser ce projet pour un autre événement, créer une nouvelle base Firebase et remplacer cette URL.

### Règles Firebase recommandées

Pour autoriser la lecture/écriture sans authentification (adapté à un groupe de confiance) :

```json
{
  "rules": {
    ".read": true,
    ".write": true
  }
}
```

---

## 🚀 Utilisation

### Ouvrir localement
```bash
git clone https://github.com/votre-utilisateur/we-maggie.git
open we-maggie/index.html
```

> ℹ️ Firebase nécessite une connexion internet. Sans réseau, l'app se charge avec les valeurs par défaut.

### Déployer en ligne
- **GitHub Pages** — activer dans Settings → Pages
- **Netlify / Vercel** — glisser-déposer le fichier

Partager simplement l'URL avec les participantes — tout le monde voit les mêmes données en temps réel.

---

## 🛠️ Personnalisation

Toutes les modifications se font dans `index.html`.

### Changer les participantes
Modifier le tableau `PARTICIPANTES_INIT` dans le JS :

```javascript
const PARTICIPANTES_INIT = [
  {id:'prenom',  nom:'Prénom',  tel:'06 XX XX XX XX', chambre:'Chambre X', maggie:false},
  // ...
  {id:'anniversaire', nom:'Prénom 🎂', tel:'...', chambre:'...', maggie:true}, // la fêtée
];
```

### Changer les tarifs
Les montants sont codés en dur dans `renderFinances()` et `calcTotal()` :

```javascript
if (pr.resto) t += 29;        // Prix du restaurant
if (pr.davidrachel) t += 50;  // Prix de la journée chez D&R
// Mob : 80€, Vélo : 60€ (voir mobCost())
// Massage : 37.5€ ou 75€ (valeurs dans pForm())
```

### Changer la checklist "À emporter"
Modifier le tableau `CHECKLIST_ITEMS` :

```javascript
const CHECKLIST_ITEMS = [
  'Maillot de bain',
  'Crème solaire',
  // ...
];
```

### Réinitialiser la base Firebase
Pour repartir d'un état vide, envoyer `null` à la base via la console Firebase ou :

```bash
curl -X PUT https://your-db.firebasedatabase.app/state.json -d 'null'
```

---

## 🧰 Technologies

| Technologie | Usage |
|---|---|
| HTML5 / CSS3 | Structure et mise en page |
| JavaScript Vanilla | Toute la logique applicative (état, rendu, events) |
| Firebase Realtime Database | Persistance et synchronisation des données |
| Google Fonts | Playfair Display + DM Sans |
| `fetch` API | Communication avec Firebase (GET/PUT) |

**Aucun framework, aucune bibliothèque JS externe — zéro dépendance front.**

---

## 📄 Licence

Projet réalisé pour usage privé — Weekend anniversaire Maggie, 2026.

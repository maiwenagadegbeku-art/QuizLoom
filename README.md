# ⚡ QuizLoom

**Générateur de QCM pour Pronote — à partir de tes séances Lesson Loom**

Outil standalone pour enseignants d'anglais LV1 (collège / lycée). QuizLoom transforme le contenu d'une séance en prompt Claude.ai, puis convertit la réponse en fichier XML importable dans Pronote — sans serveur, sans installation, sans clé API.

---

## Prérequis

- Un navigateur moderne (Chrome, Firefox, Edge)
- Un compte Claude.ai (abonnement existant suffisant)
- Lesson Loom (pour exporter le contenu des séances)

Aucune installation. Double-clic sur `quizloom.html` pour ouvrir.

---

## Workflow en 3 étapes

```
QuizLoom          →   Claude.ai            →   QuizLoom          →   Pronote
Génère le prompt      Colle · Envoie           Colle la réponse      Importe le .xml
                      Copie la réponse          Télécharge le XML
```

### Étape 1 — Configurer et générer le prompt

**Apporter le contenu de la séance** — deux modes au choix :

- **Coller du texte** : dans Lesson Loom, ouvre une séance → menu Exporter → ⚡ Copier pour QuizLoom → un sélecteur permet de choisir 1, 2 ou plusieurs séances → colle ici
- **Importer un RTF** : importe directement le fichier `.rtf` exporté par Lesson Loom

**Configurer le QCM** :

| Option | Valeurs disponibles |
|--------|-------------------|
| Nombre de questions | 3, 4, 5, 6, 8, 10, 12, 15, 20, 25, 30 |
| Niveau CECRL | A1, A1+, A2, A2+, B1, B1+, B2, B2+, C1, C1+ |
| Type | Mixte, Compréhension littérale, Inférence, Vocabulaire, Lexique en contexte, Grammaire, Connecteurs logiques, Civilisation / culture, Vrai / Faux justifié |

Clique sur **⚡ Générer le prompt** → copie le prompt → ouvre [claude.ai](https://claude.ai) → colle et envoie.

---

### Étape 2 — Convertir en XML Pronote

Une fois Claude.ai a répondu, copie sa réponse et colle-la dans la zone de l'étape 2.

**Format attendu** — Claude génère automatiquement le bon format (les consignes sont incluses dans le prompt) :

```
What is the capital of the UK?
V=London
Paris
Dublin
Edinburgh

Who wrote "Romeo and Juliet"?
Charles Dickens
V=William Shakespeare
Jane Austen
Oscar Wilde
```

Chaque bonne réponse commence par `V=`. Les blocs sont séparés par une ligne vide.

**Remplis les métadonnées** :
- Nom du QCM (ex : `Séance 3 — Maleficent`)
- Classe / Niveau (ex : `2NDE 3`)
- Matière (pré-remplie : `Anglais`)

Coche **Mélanger l'ordre des réponses** (recommandé) → clique **🧩 Générer le fichier XML Pronote** → **⬇️ Télécharger le .xml**.

---

### Étape 3 — Import dans Pronote

Dans Pronote : **Outils pédagogiques → QCM → Importer des QCM → depuis des fichiers XML**

Sélectionne le fichier `.xml` téléchargé. Relis toujours le QCM avant de le diffuser.

---

## Fonctionnalités

- **Détection automatique** du format V= — avertissements si une question est mal formée
- **Comptage en direct** des questions pendant la saisie
- **Mélange des réponses** pour éviter les patterns (optionnel)
- **Bouton Effacer** sur chaque zone de saisie
- **✦ Nouveau QCM** — remet tout à zéro en un clic après génération
- **Guide & Démo** — tour interactif en 9 étapes + séance démo Fairy Tales (2NDE B1+)
- **RTF stripping** — le fichier RTF Lesson Loom est nettoyé automatiquement avant envoi
- **Dark mode** automatique (suit les préférences système)

---

## Compatibilité Pronote

Le XML généré est compatible avec le format d'import Pronote (questions à choix multiples, fraction de points proportionnelle au nombre de bonnes réponses, encodage UTF-8).

---

## Lien avec Lesson Loom

Dans Lesson Loom, le menu **Exporter → ⚡ Copier pour QuizLoom** ouvre un sélecteur permettant de cocher 1, plusieurs ou toutes les séances d'une séquence. Le texte est copié dans le presse-papier, prêt à être collé dans QuizLoom.

---

## Limites

- Le contenu de la séance est tronqué à 3 000 caractères dans le prompt (suffisant pour une séance complète)
- La qualité du QCM dépend du contenu fourni — plus la séance est détaillée, meilleures sont les questions
- Toujours relire et valider les questions avant diffusion aux élèves

---

## Licence et auteure

**GNU Affero General Public License v3 (AGPLv3)** — © Juin 2026 Maïwena Gadegbeku

Vous êtes libre d'utiliser, d'étudier, de modifier et de redistribuer cet outil. En contrepartie, toute version modifiée qui est redistribuée **ou mise à disposition sur un serveur** doit être publiée sous cette même licence, code source compris.

Voir le fichier [LICENSE](LICENSE) pour le texte complet, et <https://www.gnu.org/licenses/agpl-3.0.html> pour la licence officielle.

🪄 **QuizLoom** — Développé pour les enseignants d'anglais LV1 dans le secondaire français.
Compagnon de **Lesson Loom** — inspiré de [l'interface Gemini QCM](https://interface-gemini-3377c4.forge.apps.education.fr/#/qcm).

Contact : [contact@lessonloom.fr](mailto:contact@lessonloom.fr)

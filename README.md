# ⚡ QuizLoom

**Générateur de QCM pour Pronote et de quiz web — à partir de tes séances Lesson Loom**

Outil standalone pour enseignants d'anglais LV1 (collège / lycée). QuizLoom transforme le contenu d'une séance en prompt Claude.ai, puis convertit la réponse en **fichier XML importable dans Pronote** ou en **quiz web interactif** à intégrer sur un site — sans serveur, sans installation, sans clé API.

---

## Prérequis

- Un navigateur moderne (Chrome, Firefox, Edge)
- Un compte Claude.ai (abonnement existant suffisant)
- Lesson Loom (pour exporter le contenu des séances)

Aucune installation. Double-clic sur `quizloom.html` pour ouvrir.

> ### Où va le contenu
>
> QuizLoom ne communique avec aucun service : il fabrique un texte, vous le copiez, et **c'est vous qui décidez où le coller**. Le contenu de votre séance part donc chez l'assistant conversationnel que vous choisissez — vous voyez exactement ce que vous envoyez.
>
> Les consignes de format sont du texte ordinaire : elles fonctionnent avec Claude, mais aussi avec un autre assistant. Le bouton mène à Claude.ai parce que c'est celui que j'utilise ; rien ne vous y oblige.

---

## Workflow

```
QuizLoom          →   Claude.ai            →   QuizLoom          →   Pronote
Génère le prompt      Colle · Envoie           Colle la réponse      Importe le .xml
                      Copie la réponse                ↓
                                                  ou quiz web
                                                  fichier HTML autonome
```

### Étape 1 — Configurer et générer le prompt

**Apporter le contenu de la séance** — deux modes au choix :

- **Coller du texte** : dans Lesson Loom, ouvre une séance → menu Exporter → ⚡ Copier pour QuizLoom → un sélecteur permet de choisir 1, 2 ou plusieurs séances → colle ici
- **Importer un RTF** : importe directement le fichier `.rtf` exporté par Lesson Loom

Les deux modes donnent le même résultat.

**Configurer le QCM** :

| Réglage | Valeurs disponibles |
|--------|-------------------|
| Nombre de questions | 3, 4, 5, 6, 8, 10, 12, 15, 20, 25, 30 |
| Niveau CECRL | A1, A1+, A2, A2+, B1, B1+, B2, B2+, C1, C1+ |
| **Formats de question** *(cases à cocher)* | QCM, Vrai / Faux — coche les deux pour les mélanger |
| **Angle de contenu** *(optionnel)* | **Compréhension** : littérale, inférence · **Langue** : vocabulaire, grammaire, connecteurs logiques · **Autre** : civilisation / culture · ou *Tout — mélange équilibré* |

Clique sur **⚡ Générer le prompt** → copie le prompt → ouvre [claude.ai](https://claude.ai) → colle et envoie.

---

### Étape 2 — Convertir en XML Pronote

Une fois que Claude.ai a répondu, copie sa réponse et colle-la dans la zone de l'étape 2.

**Format attendu** — les consignes sont déjà incluses dans le prompt, la réponse arrive donc au bon format :

```
[QCM]
C=Choose the correct answer.
What is the capital of the UK?
V=London
Paris
Dublin
E=The document states that London is the capital of the United Kingdom.

[VF]
C=True or false?
Shakespeare wrote "Romeo and Juliet".
V=True
E=The text names Shakespeare as the author of the play.
```

Chaque bloc commence par son tag — `[QCM]` ou `[VF]` — sur sa propre ligne, et les blocs
sont séparés par une ligne vide. Dans chaque bloc : `C=` la consigne adressée à l'élève,
`V=` la ou les bonnes réponses, `E=` l'explication. Les autres propositions n'ont pas de
préfixe.

Un format plus simple, sans tag ni `C=` ni `E=`, reste accepté : QuizLoom traite alors le
bloc comme un QCM. Mais l'explication `E=` alimente le quiz web, et sans elle les élèves
n'ont aucun retour après leur réponse.

QuizLoom compte les questions en direct et vérifie le format. **Si un bloc est mal repéré, un encadré orange apparaît** — pendant la saisie, puis de nouveau après la génération — nommant chaque bloc en cause, avec un menu qui permet de corriger son format sur place, sans repasser par Claude.

> ⚠️ **Un bloc sans `V=`.** Si l'assistant oublie de marquer la bonne réponse, QuizLoom **retient la première proposition** pour ne pas perdre la question, et le signale en orange. Cette réponse par défaut a toutes les chances d'être fausse : vérifiez-la avant d'importer dans Pronote.

**Remplis les métadonnées** :
- Nom du QCM (ex : `Séance 3 — Vocab`)
- Classe / Niveau (ex : `3E`, `2NDE`…)
- Matière (pré-remplie : `Anglais`)

Coche **Mélanger l'ordre des réponses** (recommandé) → clique **🧩 Générer le fichier XML Pronote** → **⬇️ Télécharger le .xml**.

---

### Étape 3 — Exporter un quiz web interactif

La même réponse peut aussi devenir un **quiz jouable dans le navigateur** : un fichier HTML autonome, à mettre en ligne ou à intégrer en iframe sur n'importe quel site.

1. Donne un titre au quiz — c'est celui que verront les élèves
2. Clique **🌐 Export web quiz**
3. **⬇️ Download HTML** pour récupérer le fichier

**Réglage à faire une seule fois** — le bouton **⚙ Settings**, tout en bas de la page, sous le XML : indique l'adresse de base de ton site, par exemple `https://mon-site.fr/quiz/`. QuizLoom construit alors l'adresse complète de chaque quiz exporté, que tu peux copier d'un clic (**📋 Copy URL**) pour la donner à tes élèves.

Sans cette adresse de base, le bouton **📋 Copy URL** ne copie que le **nom du fichier**, pas une adresse : renseigne-la avant de partager un lien.

Le fichier obtenu ne dépend d'aucun serveur : il se joue tel quel.

---

### Étape 4 — Import dans Pronote

Dans Pronote : **Outils pédagogiques → QCM → Importer des QCM → depuis des fichiers XML**

Sélectionne le fichier `.xml` téléchargé. Relis toujours le QCM avant de le diffuser.

---

## Fonctionnalités

- **Deux sorties** à partir d'une seule réponse : XML Pronote et quiz web interactif
- **Détection automatique** du format `V=` — un bandeau signale les blocs mal formés, avec correction sur place
- **Comptage en direct** des questions pendant la saisie
- **Mélange des réponses** pour éviter les patterns (optionnel)
- **Bouton Effacer** sur chaque zone de saisie
- **Guide & Démo** — tour interactif en 10 étapes + séance démo Fairy Tales (2NDE B1+)
- **Copier ces consignes seules** — pour réutiliser le format sans le contenu de la séance
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
- Les libellés de l'étape 3 sont en anglais : ⚙ Settings, 🌐 Export web quiz, 📋 Copy URL, ⬇️ Download HTML, ainsi que le réglage « Base URL for web export »
- Toujours relire et valider les questions avant diffusion aux élèves

---

## Licence et auteure

**GNU Affero General Public License v3 (AGPLv3)** — © Juin 2026 Maïwena Gadegbeku

Vous êtes libre d'utiliser, d'étudier, de modifier et de redistribuer cet outil. En contrepartie, toute version modifiée qui est redistribuée **ou mise à disposition sur un serveur** doit être publiée sous cette même licence, code source compris.

**Crédit obligatoire.** Le fichier [LICENSE](LICENSE) porte une condition
supplémentaire, au titre de l'article 7(b) de l'AGPLv3 : toute version modifiée
diffusée publiquement ou mise à disposition sur un serveur doit créditer
visiblement l'autrice originale, dans son interface ou dans sa documentation. Ce
crédit ne peut être ni retiré, ni dissimulé aux utilisateurs.

Voir le fichier [LICENSE](LICENSE) pour le texte complet, et <https://www.gnu.org/licenses/agpl-3.0.html> pour la licence officielle.

🪄 **QuizLoom** — Développé pour les enseignants d'anglais LV1 dans le secondaire français.
Compagnon de **Lesson Loom** — inspiré de [l'interface Gemini QCM](https://interface-gemini-3377c4.forge.apps.education.fr/#/qcm).

Contact : [contact@lessonloom.fr](mailto:contact@lessonloom.fr)

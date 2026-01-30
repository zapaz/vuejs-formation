# Formation Vue.js accélérée — Prompts pour Claude Code

> Guide complet pour apprendre Vue.js 3 avec Claude Code
> Parcours en 5 modules progressifs avec mini-projets pratiques

---

## 📋 Table des matières

- [Module 1 : Fondamentaux](#module-1--fondamentaux)
- [Module 2 : Composants & Communication](#module-2--composants--communication)
- [Module 3 : Composition API avancée](#module-3--composition-api-avancée)
- [Module 4 : Routing & State Management](#module-4--routing--state-management)
- [Module 5 : Intégration Backend](#module-5--intégration-backend)
- [Bonus](#prompts-bonus)
- [Conseils d'utilisation](#conseils-dutilisation)

---

## Module 1 : Fondamentaux

**Durée estimée : 1-2h**

### Prompt 1.1 — Initialisation du projet

```
Créons une formation Vue.js ensemble. Je suis développeur expérimenté (Python, blockchain) mais nouveau sur Vue.

1. Initialise un projet Vue 3 avec Vite dans un dossier "vue-formation"
2. Utilise TypeScript
3. Explique-moi brièvement la structure des fichiers générés
4. Lance le serveur de dev pour vérifier que tout fonctionne
```

### Prompt 1.2 — Premier composant et réactivité

```
Maintenant, explique-moi la réactivité Vue 3 en pratique :

1. Crée un composant Counter.vue avec :
   - Un compteur utilisant ref()
   - Des boutons +1 et -1
   - Un affichage du double du compteur avec computed()

2. Explique la différence entre ref() et reactive()
3. Montre-moi comment le DOM se met à jour automatiquement
```

### Prompt 1.3 — Directives essentielles

```
Passons aux directives Vue. Crée un composant TaskList.vue qui démontre :

1. v-for : afficher une liste de tâches
2. v-if / v-else : afficher "Liste vide" si aucune tâche
3. v-bind : lier une classe CSS conditionnelle (tâche complétée = barrée)
4. v-on (@click) : toggle le statut d'une tâche
5. v-model : input pour ajouter une nouvelle tâche

Explique chaque directive au fur et à mesure.
```

### Prompt 1.4 — Mini-projet Todo List

```
Consolidons avec une Todo List complète. Crée un composant TodoApp.vue avec :

1. Ajouter une tâche (input + bouton)
2. Lister les tâches
3. Marquer comme complétée (checkbox)
4. Supprimer une tâche
5. Filtres : Toutes / Actives / Complétées
6. Compteur de tâches restantes

Style-le proprement avec du CSS scoped. Explique les choix d'architecture.
```

---

## Module 2 : Composants & Communication

**Durée estimée : 1-2h**

### Prompt 2.1 — Props (parent → enfant)

```
Apprenons la communication entre composants.

1. Crée un composant parent UserList.vue avec un tableau d'utilisateurs
2. Crée un composant enfant UserCard.vue qui reçoit un user en prop
3. Montre-moi :
   - Comment définir les props avec TypeScript (defineProps)
   - La validation des props
   - Les valeurs par défaut

Explique le flux de données unidirectionnel.
```

### Prompt 2.2 — Emit (enfant → parent)

```
Maintenant la communication inverse avec emit :

1. Dans UserCard.vue, ajoute un bouton "Supprimer"
2. Quand on clique, émets un événement vers le parent
3. Le parent supprime l'utilisateur de sa liste

Montre-moi :
- defineEmits avec TypeScript
- Comment typer les payloads des événements
```

### Prompt 2.3 — Slots

```
Explique-moi les slots Vue avec un exemple pratique :

1. Crée un composant Card.vue générique avec :
   - Un slot par défaut pour le contenu
   - Un slot nommé "header"
   - Un slot nommé "footer"
   - Un scoped slot qui expose des données

2. Utilise ce composant Card de plusieurs façons différentes pour montrer la flexibilité
```

### Prompt 2.4 — Mini-projet Profil réutilisable

```
Mini-projet : système de cartes de profil réutilisables

1. Crée ProfileCard.vue (props: user, variant: 'compact' | 'full')
2. Crée ProfileList.vue (affiche plusieurs profils)
3. Ajoute des actions : "Suivre", "Message" (emit vers parent)
4. Utilise des slots pour personnaliser certaines sections
5. Ajoute des transitions CSS quand on suit/unfollow

Structure bien le code en plusieurs fichiers.
```

---

## Module 3 : Composition API avancée

**Durée estimée : 2h**

### Prompt 3.1 — Computed et Watch

```
Approfondissons la réactivité avancée :

1. Crée un composant SearchFilter.vue avec :
   - Un input de recherche
   - Une liste d'items filtrée avec computed()
   - Un watch() qui log chaque changement de recherche
   - Un watchEffect() pour une side-effect automatique

2. Explique les différences entre watch et watchEffect
3. Montre les options de watch (immediate, deep)
```

### Prompt 3.2 — Lifecycle Hooks

```
Montre-moi les lifecycle hooks Vue 3 :

1. Crée un composant Timer.vue avec :
   - onMounted : démarre un setInterval
   - onUnmounted : nettoie l'interval (éviter memory leaks)
   - onUpdated : log quand le composant se met à jour

2. Crée un composant qui fetch des données au mount
3. Explique le cycle de vie complet d'un composant Vue
```

### Prompt 3.3 — Composables

```
Les composables sont essentiels en Vue 3. Crée :

1. useCounter.ts : logique de compteur réutilisable
2. useFetch.ts : wrapper générique pour les appels API avec :
   - État loading, error, data
   - Fonction refetch
   - Support TypeScript générique

3. useLocalStorage.ts : ref synchronisée avec localStorage

Montre comment les utiliser dans des composants.
```

### Prompt 3.4 — Mini-projet Recherche API

```
Mini-projet : recherche d'utilisateurs GitHub avec debounce

1. Crée useDebounce.ts (composable)
2. Crée useFetch.ts si pas déjà fait
3. Crée GitHubSearch.vue :
   - Input de recherche avec debounce 500ms
   - Appel API GitHub (https://api.github.com/search/users?q=xxx)
   - Affichage des résultats avec loading state
   - Gestion des erreurs
   - Cache simple des résultats déjà cherchés

4. Bonus : pagination des résultats
```

---

## Module 4 : Routing & State Management

**Durée estimée : 2h**

### Prompt 4.1 — Vue Router basics

```
Configurons Vue Router :

1. Installe et configure vue-router
2. Crée les pages : Home.vue, About.vue, Users.vue, UserDetail.vue
3. Configure les routes avec :
   - Route statique (/about)
   - Route dynamique (/users/:id)
   - Route imbriquée (nested)
   - Route 404 catch-all

4. Crée un composant NavBar avec router-link
5. Explique router-view et la navigation programmatique
```

### Prompt 4.2 — Navigation Guards

```
Ajoutons de la sécurité avec les navigation guards :

1. Crée une page Login.vue simple (juste un bouton qui simule login)
2. Crée une page Dashboard.vue protégée
3. Implémente :
   - beforeEach global : vérifie si authentifié
   - beforeEnter sur route : protection spécifique
   - Redirection vers login si non auth
   - Stockage de la route demandée pour redirect après login

4. Simule l'état d'authentification avec un simple ref ou localStorage
```

### Prompt 4.3 — Pinia basics

```
Passons à Pinia pour le state management :

1. Installe et configure Pinia
2. Crée un store auth.ts avec :
   - State : user, isAuthenticated
   - Getters : userFullName, isAdmin
   - Actions : login(), logout()

3. Crée un store counter.ts (plus simple, pour comparer)
4. Utilise ces stores dans des composants
5. Explique les avantages de Pinia vs Vuex
```

### Prompt 4.4 — Mini-projet App multi-pages

```
Mini-projet : application multi-pages avec auth

1. Pages : Login, Register, Dashboard, Profile, Settings
2. Layout avec sidebar (visible seulement si connecté)
3. Store Pinia pour :
   - Auth (user, token simulé)
   - Theme (dark/light mode persisté)
   - Notifications (toast messages)

4. Navigation guards pour protéger les routes
5. Transitions entre les pages
6. Persistance du state dans localStorage (plugin Pinia)

Structure le projet proprement (dossiers views/, stores/, composables/, components/).
```

---

## Module 5 : Intégration Backend

**Durée estimée : 2h**

### Prompt 5.1 — API calls structurés

```
Organisons les appels API proprement :

1. Crée un dossier api/ avec :
   - client.ts : instance Axios configurée (baseURL, interceptors)
   - users.ts : fonctions getUsers(), getUser(id), createUser()
   - auth.ts : login(), logout(), refreshToken()

2. Crée un composable useApi.ts générique avec :
   - Gestion loading/error/data
   - Abort controller pour cancel
   - Retry automatique

3. Montre l'utilisation dans un composant
4. Ajoute un interceptor pour gérer les erreurs 401 (token expiré)
```

### Prompt 5.2 — Loading states et error handling

```
Améliorons l'UX avec une bonne gestion des états :

1. Crée un composant LoadingSpinner.vue
2. Crée un composant ErrorMessage.vue (avec retry)
3. Crée un composant Skeleton.vue pour le loading progressif
4. Crée un composable useAsyncState.ts qui gère :
   - idle, loading, success, error states
   - Type-safe avec TypeScript

5. Démontre dans une page qui fetch une liste avec :
   - Skeleton pendant le chargement initial
   - Spinner pour les actions
   - Toast pour les erreurs
```

### Prompt 5.3 — WebSockets et temps réel

```
Intégrons du temps réel (lien avec mes connaissances Redis Pub/Sub) :

1. Crée un composable useWebSocket.ts avec :
   - Connexion/déconnexion automatique
   - Reconnexion automatique si déconnecté
   - État de connexion réactif
   - Méthodes send() et subscribe()

2. Crée un composant NotificationCenter.vue qui :
   - Se connecte au WebSocket au mount
   - Affiche les notifications en temps réel
   - Gère la déconnexion proprement

3. Simule un serveur WebSocket simple avec un script Node (ou explique comment le faire avec Python/FastAPI)
```

### Prompt 5.4 — Mini-projet Dashboard temps réel

```
Mini-projet final : Dashboard temps réel

1. Simule un backend (fichier mock ou json-server)
2. Dashboard avec :
   - Stats en temps réel (compteurs animés)
   - Graphique qui se met à jour (utilise Chart.js ou une lib Vue)
   - Liste d'événements live (nouveaux en haut avec animation)
   - Indicateur de connexion WebSocket

3. Utilise tout ce qu'on a appris :
   - Composables pour la logique
   - Pinia pour le state global
   - Vue Router pour navigation
   - Composants réutilisables

4. Architecture production-ready avec bonne séparation des responsabilités
```

---

## Prompts Bonus

### Bonus — Tests unitaires

```
Ajoutons des tests à notre projet :

1. Configure Vitest
2. Écris des tests pour :
   - Un composant simple (Counter)
   - Un composable (useCounter)
   - Un store Pinia
   - Un composant avec props et emit

3. Montre comment mocker les appels API
4. Explique les bonnes pratiques de test Vue
```

### Bonus — Build et déploiement

```
Préparons le projet pour la production :

1. Explique la config Vite pour la prod
2. Configure les variables d'environnement (.env)
3. Optimise le bundle (code splitting, lazy loading des routes)
4. Crée un Dockerfile pour containeriser l'app
5. Montre comment déployer sur Vercel ou Netlify
```

---

## Conseils d'utilisation

### Pendant la formation

À chaque étape avec Claude Code, n'hésite pas à ajouter :

- *"Explique-moi pourquoi tu fais ce choix"*
- *"Quelle est la best practice ici ?"*
- *"Comment ça se compare à React/Svelte ?"*
- *"Montre-moi une alternative"*

### Ordre recommandé

1. Suis les modules dans l'ordre (1 → 5)
2. Ne passe pas au module suivant sans avoir compris le précédent
3. Fais les mini-projets, ils consolident les apprentissages
4. Expérimente et modifie le code pour bien comprendre

### Ressources complémentaires

- Documentation officielle Vue.js : https://vuejs.org/
- Vue Router : https://router.vuejs.org/
- Pinia : https://pinia.vuejs.org/
- VueUse (composables utiles) : https://vueuse.org/
- Awesome Vue : https://github.com/vuejs/awesome-vue

---

## Progression suggérée

| Module | Durée | Objectif |
|--------|-------|----------|
| 1. Fondamentaux | 1-2h | Comprendre la réactivité et les directives |
| 2. Composants | 1-2h | Maîtriser la communication entre composants |
| 3. Composition API | 2h | Créer des composables réutilisables |
| 4. Routing & State | 2h | Construire une SPA complète |
| 5. Backend | 2h | Intégrer avec des APIs et WebSockets |

**Total : ~10h pour une maîtrise solide de Vue.js 3**

---

Bonne formation ! 🚀

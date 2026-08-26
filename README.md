# Clone fonctionnel de guizzi.fr

Recréation des fonctionnalités du site (accueil, planning, config CS2/communauté, profil)
avec un vrai backend : Node/Express + base JSON (lowdb) + OAuth2 Discord/Twitch.

## Structure

```
backend/    API Express (auth, giveaway, planning, candidatures, profil, communauté)
frontend/   React + Vite + Tailwind
```

## Pages recréées

- **/** — avatar (hover), réseaux, giveaway du mois, teaser planning, dernières vidéos YouTube
- **/planning** — planning hebdo, bannière "tournage ouvert" → candidature, giveaway
- **/site** — Point Shop, config PC, settings CS2 (crosshair/résolution/viewmodel/autoexec copiables), extensions Faceit, stats communauté (niveau moyen, distribution, top niveaux)
- **/profil** — connexion Discord (obligatoire), mes candidatures, vérification Faceit, vérification CSStats (Elo Premier auto), infos perso, connexion Twitch + Point Shop

## Démarrage rapide

### 1. Backend

```bash
cd backend
cp .env.example .env
npm install
npm run dev
```

Le site fonctionne dès le démarrage avec des données de démo (giveaway, config CS2).
Sans clés API, les fonctionnalités suivantes s'affichent en mode "non configuré" au lieu de planter :
- connexion Discord / Twitch (nécessite une app OAuth2 sur chaque plateforme)
- vérification Faceit (nécessite une clé sur developers.faceit.com)
- vidéos YouTube (nécessite une clé YouTube Data API v3)

### 2. Frontend

```bash
cd frontend
npm install
npm run dev
```

Ouvre http://localhost:5173

### 3. Personnalisation

- `frontend/src/siteConfig.js` : nom, avatar, liens de réseaux sociaux
- `backend/data/db.json` (généré au 1er lancement) : giveaway, planning, config CS2, extensions
- `backend/.env` : toutes les clés API (voir `.env.example` pour la liste complète et où les obtenir)

## Ce qui nécessite tes propres identifiants pour fonctionner "à l'identique"

| Fonctionnalité | Ce qu'il faut |
|---|---|
| Connexion Discord | App OAuth2 sur discord.com/developers |
| Connexion Twitch + Point Shop | App sur dev.twitch.tv, scope `channel_points_read`, EventSub à brancher si tu veux les rewards en temps réel |
| Vérification Faceit | Clé API sur developers.faceit.com |
| Elo CSStats.gg | Pas d'API officielle — la route fait un scraping best-effort de la page publique, à surveiller si CSStats change son HTML |
| Vidéos YouTube | Clé YouTube Data API v3 + ID de chaîne |

Le reste (planning, candidatures, giveaway, config CS2, stats de communauté) tourne
directement avec la base JSON fournie, sans clé externe.

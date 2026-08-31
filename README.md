---

## 📝 SYNTHÈSE COMPLÈTE : Extraction de la version originale de Portal depuis le Steam2 Teraleak

### 🔗 Liens importants
- **Site principal du leak** : https://steam2.download/
- **Liste des Depot IDs** : https://raw.githubusercontent.com/dr3murr/steam2-winfsp/refs/heads/main/data/depot_labels.tsv
- **SteamDB (pour vérifier les versions)** : https://steamdb.info/depot/401/

---

### 1️⃣ CONTEXTE DU PROJET

**Source** : Leak des anciens serveurs de contenu Steam2 de Valve (2003-2013), totalisant ~13 To de données.

**Objectif** : Extraire la toute première version (v0) du jeu *Portal* (sorti en 2007).

**Contrainte technique** : Steam2 stockait les mises à jour sous forme de "deltas" (seules les modifications). Pour une version N, il faut généralement la version 0 + tous les deltas jusqu'à N. *Exception* : si le dépôt a subi un "reset", on peut extraire une version spécifique directement avec son CRC. Heureusement, la version 0 est la base complète, aucun delta précédent n'est requis.

---

### 2️⃣ COMMENT TROUVER LES FICHIERS

#### 📍 Où chercher :
1. **Page principale** : https://steam2.download/
   - Affiche l'index à la racine avec les dossiers `/blobs/`, `/dats/`, `/extractor/`

2. **Pour connaître les Depot IDs** :
   - **Méthode 1** : Télécharger le fichier TSV : https://raw.githubusercontent.com/dr3murr/steam2-winfsp/refs/heads/main/data/depot_labels.tsv
     - Contient la liste de tous les depot IDs et leurs noms de jeux
     - Exemple : `401` = Portal Windows
   
   - **Méthode 2** : Consulter SteamDB
     - Aller sur https://steamdb.info/app/400/depots/ pour Portal
     - Trouver le Depot ID (401 pour Windows)

3. **Navigation dans les dossiers** :
   - `/dats/` → Contient tous les fichiers `.dat` (données)
   - `/blobs/` → Contient tous les fichiers `.blob` (métadonnées)
   - `/extractor/` → Contient l'outil d'extraction

#### 🔍 Comment identifier les bons fichiers :
Les fichiers sont nommés : `[depot_id]_[version]_[hash]...`

**Exemple pour Portal v0** :
- Chercher les fichiers commençant par `401_0_`
- Le premier chiffre = depot ID (401)
- Le deuxième chiffre = version (0)

---

### 3️⃣ QUOI TÉLÉCHARGER (EXEMPLE PORTAL)

#### 📋 Checklist pour Portal version 0 :

**Depuis https://steam2.download/ :**

1. **Dans `/dats/`** :
   - Trouver le fichier `401_0_...` (ex: `401_0_bcb11162_f5059dfe87dc14053794298725525f582d0ab13a6517a5631f6bbbe69bb1545d`)
   - Taille : ~530 Mo
   - Date : 2009-Sep-18

2. **Dans `/blobs/`** :
   - Trouver le fichier `401_0_...` correspondant (ex: `401_0_1e950c7c_0628c7af6849c61e635f115ccb2a2360a23324193f77d049075e7617fcbcd0ac`)
   - Taille : ~356 Ko
   - Date : 2007-Sep-28

3. **Dans `/extractor/`** :
   - Télécharger `extract.exe` (1.8 Mo)
   - Optionnel : `src.zip` (code source, 142 Ko)

---

### 4️⃣ COMMENT TÉLÉCHARGER

#### Méthode 1 : Navigation web directe
1. Aller sur https://steam2.download/
2. Cliquer sur `/dats/` pour entrer dans le dossier
3. Chercher le fichier souhaité (utiliser Ctrl+F pour rechercher `401_0`)
4. Cliquer sur le nom du fichier pour le télécharger
5. Répéter pour `/blobs/` et `/extractor/`

#### Méthode 2 : Téléchargement direct (si liens connus)
- Construire l'URL : `https://steam2.download/dats/[nom_du_fichier]`
- Exemple : `https://steam2.download/dats/401_0_bcb11162_...`

#### Méthode 3 : Via torrent (recommandé pour gros volumes)
- Le site mentionne un seed WebTorrent
- Utiliser un client torrent compatible WebTorrent

---

### 5️⃣ PROCÉDURE D'EXTRACTION (WINDOWS)

L'extracteur attend des **dossiers**, pas des fichiers directs.

#### 📁 Structure requise :
```
C:\Users\Antoine\Downloads\test steam2 LEAK\
├── extract.exe
├── blobs\
│   └── 401_0_1e950c7c_....blob
└── dats\
    └── 401_0_bcb11162_....dat
```

#### 💻 Commandes à exécuter :
```cmd
:: 1. Créer les dossiers requis
mkdir blobs dats

:: 2. Déplacer les fichiers téléchargés dans leurs dossiers respectifs
move 401_0_1e950c7c_....blob blobs\
move 401_0_bcb11162_....dat dats\

:: 3. Lancer l'extraction
:: Syntaxe : extract.exe <dossier_blob> <dossier_dat> <depot_id> <version>
extract.exe blobs dats 401 0
```

####  Résultat :
Un dossier de sortie (souvent `out/` ou `401_0/`) contenant les fichiers extraits.

---

### 6️⃣ CE QUI EST EXTRAIT (ET CE QUI NE L'EST PAS)

#### ✅ Ce que tu obtiens :
- **maps/** → Niveaux du jeu (.bsp)
- **models/** → Modèles 3D (personnages, objets)
- **materials/** → Textures
- **sound/** → Fichiers audio
- **scripts/** → Scripts de configuration
- **resource/** → UI, polices, localisation
- **scenes/** → Cinématiques
- **particles/** → Effets visuels
- **cfg/** → Configurations
- **GameInfo.txt**, **steam.inf** → Métadonnées

#### ❌ Ce que tu n'as PAS :
- Le code source C++ du jeu
- L'exécutable jouable (`portal.exe`)
- Le moteur Source compilé

#### 🎮 Usage possible :
- Archivage et préservation historique
- Exploration des assets originaux
- Modding avec Source SDK (disponible sur Steam)
- Décompilation de maps avec BSPSource
- Extraction de modèles/textures avec Crowbar ou GCFScape

**Note importante** : Ces fichiers ne permettent pas de jouer directement. Pour jouer à Portal, il faut l'acheter sur Steam (~10€).

---

### 📚 RÉCAPITULATIF DES LIENS UTILES

| Ressource | Lien |
|-----------|------|
| **Site du leak** | https://steam2.download/ |
| **Liste des Depot IDs** | https://raw.githubusercontent.com/dr3murr/steam2-winfsp/refs/heads/main/data/depot_labels.tsv |
| **SteamDB - Portal Depots** | https://steamdb.info/app/400/depots/ |
| **SteamDB - Depot 401** | https://steamdb.info/depot/401/manifests/ |
| **GitHub - Extracteur** | https://github.com/extremebleem/steam2_downloader |
| **Acheter Portal** | https://store.steampowered.com/app/400/Portal/ |

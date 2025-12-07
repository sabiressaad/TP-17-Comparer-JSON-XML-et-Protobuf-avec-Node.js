# TP 17 : Comparer JSON, XML et Protobuf avec Node.js

**Cours** : Architecture Microservices - Conception, Déploiement et Orchestration

## 📋 Aperçu

Ce lab montre comment :

- Créer une petite liste d'employés en JavaScript
- Sérialiser cette liste en **JSON**, **XML** et **Protobuf**
- Sauvegarder chaque format dans un fichier
- Comparer la **taille** des fichiers pour comprendre l'intérêt de Protobuf
- Mesurer les **temps d'encodage/décodage** de chaque format

À la fin, il devient clair pourquoi **gRPC** préfère **Protocol Buffers** à JSON ou XML.

---

## 🎯 Objectifs pédagogiques

À la fin du lab, l'étudiant est capable de :

- ✅ Créer un projet Node.js minimal pour des tests de sérialisation
- ✅ Utiliser `JSON.stringify` pour générer un fichier JSON
- ✅ Utiliser `xml-js` pour créer un fichier XML à partir d'un objet JavaScript
- ✅ Définir un schéma Protobuf dans un fichier `.proto`
- ✅ Utiliser `protobufjs` pour encoder des données en binaire Protobuf
- ✅ Comparer la taille de fichiers JSON, XML et Protobuf
- ✅ Mesurer et comparer les performances d'encodage/décodage

---

## 📦 Prérequis

- **Node.js** installé (v14+ recommandé)
- Connaissances de base :
  - JavaScript côté serveur (Node)
  - Notion d'objet JSON
- Un éditeur de code (VS Code, WebStorm, etc.)

---

## 🚀 Installation

### 1. Cloner le projet

```bash
git clone https://github.com/sabiressaad/TP-17-Comparer-JSON-XML-et-Protobuf-avec-Node.js.git
cd TP-17-Comparer-JSON-XML-et-Protobuf-avec-Node.js
```

### 2. Installer les dépendances

```bash
npm install
```

Cela installera :
- `xml-js` : conversion JSON ↔ XML
- `protobufjs` : utilisation de Protobuf dans Node.js

---

## 📁 Structure du projet

```
.
├── index.js           # Script principal
├── employee.proto     # Schéma Protobuf
├── package.json       # Configuration du projet
├── data.json          # Fichier généré (JSON)
├── data.xml           # Fichier généré (XML)
├── data.proto         # Fichier généré (Protobuf binaire)
└── README.md          # Documentation
```

---

## 🔧 Utilisation

### Exécuter le script

```bash
node index.js
```

### Résultat attendu

Le script va :
1. Créer une liste de 3 employés
2. Sérialiser en JSON, XML et Protobuf
3. Écrire les fichiers `data.json`, `data.xml`, `data.proto`
4. Afficher les tailles des fichiers
5. Afficher les temps d'encodage/décodage

**Exemple de sortie :**

```
Fichiers générés avec succès.

RÉSULTATS DE COMPARAISON
Taille JSON  : 127 octets
Taille XML   : 224 octets
Taille Proto : 41 octets

Protobuf est environ 67.72% plus léger que JSON sur cet exemple.

=== TEMPS D'ENCODAGE/DÉCODAGE ===
JSON encode: 0.123ms
JSON decode: 0.045ms
XML encode: 1.234ms
XML decode: 0.987ms
Protobuf encode: 0.567ms
Protobuf decode: 0.234ms
```

---

## 📊 Analyse des résultats

### Comparaison des tailles

| Format   | Taille (octets) | Verbosité |
|----------|-----------------|-----------|
| XML      | ~224            | ⚠️ Très verbeux (balises ouvrantes/fermantes) |
| JSON     | ~127            | ✅ Plus compact qu'XML |
| Protobuf | ~41             | 🎯 **Le plus compact** (format binaire) |

### Pourquoi Protobuf est-il si compact ?

- **Format binaire** : pas de texte lisible
- **Numéros de champs** : utilise des numéros (1, 2, 3) au lieu de noms répétés
- **Encodage optimisé** : compression native des entiers et autres types

### Performances

Protobuf offre généralement :
- ⚡ **Encodage plus rapide** que XML
- ⚡ **Décodage plus rapide** que XML
- 🤝 **Comparable à JSON** pour les petites structures
- 🚀 **Nettement plus rapide** pour les grandes structures

---

## 🧪 Schéma Protobuf (employee.proto)

```protobuf
syntax = "proto3";

message Employee {
  int32 id = 1;
  string name = 2;
  int32 salary = 3;
}

message Employees {
  repeated Employee employee = 1;
}
```

**Explication :**
- `syntax = "proto3"` : version moderne de Protobuf
- `message Employee` : définit la structure d'un employé
- `repeated` : équivalent d'un tableau
- `= 1`, `= 2`, `= 3` : numéros de champs (utilisés dans le binaire)

---

## 💡 Cas d'usage de Protobuf

Protobuf est particulièrement adapté pour :

- 🌐 **gRPC** : communication entre microservices
- 📡 **APIs à haute performance** : faible latence requise
- 💾 **Stockage de données** : économie d'espace disque
- 📱 **Applications mobiles** : réduction de la bande passante
- 🔄 **Streaming de données** : flux en temps réel

---

## 🔍 Extensions possibles

Pour aller plus loin :

1. **Ajouter plus de champs** dans `Employee` (email, date d'embauche, etc.)
2. **Augmenter le nombre d'employés** (100, 1000, 10000) et observer l'impact
3. **Tester avec indentation** : `JSON.stringify(obj, null, 2)` et comparer
4. **Décoder les fichiers** : lire `data.proto` et reconstruire l'objet
5. **Intégrer dans gRPC** : utiliser ce schéma pour un service gRPC complet

---

## 📚 Ressources

- [Protocol Buffers Documentation](https://developers.google.com/protocol-buffers)
- [protobufjs sur npm](https://www.npmjs.com/package/protobufjs)
- [xml-js sur npm](https://www.npmjs.com/package/xml-js)
- [gRPC Official Site](https://grpc.io/)

---

## 👨‍💻 Auteur

Lab réalisé dans le cadre du cours d'Architecture Microservices

---

## 📄 Licence

ISC

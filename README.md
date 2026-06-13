# LAB : Agents avec Langchain (SMA & IAD - Master IICCBD)

**Étudiant :** HYNDI ELMEHDI

Ce dépôt contient l'ensemble des travaux pratiques (TP) pour le module **Systèmes Multi-Agents (SMA) et Intelligence Artificielle Distribuée (IAD)** du Master IICCBD, encadré par **Prof. RETAL SARA**.

---

## Présentation du TP
L'objectif de ce TP est de concevoir et d'expérimenter différents types d'agents intelligents autonomes en s'appuyant le framework **LangChain / LangGraph** et en utilisant un modèle de langage local via **Ollama** (`llama3.2:3b`).

Il couvre la création d'agents simples jusqu'à l'implémentation d'un agent intelligent complexe doté d'outils externes (outils de recherche web) et d'un mécanisme de mémoire persistant.

---

## Prérequis et Installation

### 1. Modèle de Langage Local (Ollama)
Pour exécuter les agents localement, vous devez avoir **Ollama** installé sur votre machine avec le modèle `llama3.2:3b` :
```bash
# Vérifier la présence d'Ollama et du modèle
ollama list

# Si le modèle n'est pas présent, le télécharger
ollama pull llama3.2:3b
```

### 2. Variables d'Environnement
Créez un fichier `.env` à la racine du projet pour configurer vos clés d'API (notamment pour l'outil de recherche web Tavily) :
```env
TAVILY_API_KEY=votre_cle_tavily
GROQ_API_KEY=votre_cle_groq
OPENAI_API_KEY=votre_cle_openai
```

### 3. Installation des Dépendances Python
Installez les bibliothèques requises pour le projet :
```bash
pip install langchain langchain-core langchain-ollama langchain-groq langchain-openai langgraph langgraph-checkpoint tavily-python python-dotenv ipykernel nbclient nbformat
```

---

## Contenu des Exercices

Le TP est découpé en plusieurs parties progressives :

### 1. Création d’un nouvel agent sans System Message
Initialisation d'un agent ReAct basique sans message de contrôle. On lui pose une question absurde ("Quelle est la capitale de la lune ?") pour analyser son comportement par défaut.

### 2. Agent avec System Message
Ajout d'un message système global pour orienter le comportement de l'agent. Par exemple, le transformer en auteur de science-fiction devant inventer des capitales fictives pour l'utilisateur.

### 3. Agent avec Few-shot learning
Entraînement de l'agent en lui fournissant quelques exemples de requêtes/réponses dans le message système ("Mars -> Marsialis", "Vénus -> Venusovia") afin qu'il généralise le style de réponse attendu.

### 4. Agent avec réponse structurée (Format texte)
Forcer l'agent à structurer ses réponses sous un format textuel rigide (Nom, Localisation, Ambiance, Économie).

### 5. Agent avec réponse structurée en utilisant BaseModel (Pydantic)
Utilisation d'un schéma de données **Pydantic** (`BaseModel`) pour extraire automatiquement des réponses structurées sous forme d'objets JSON valides, prêts à être consommés par un programme tiers.

### 6. Les Tools (Outils) & Intégration
*   **Création d'un outil personnalisé** (`meteo_capitale`) pour simuler la récupération de données météo.
*   **Liaison de l'outil à l'agent** : L'agent apprend à appeler cet outil de manière autonome pour répondre aux questions relatives à la météo lunaire.

### 7. Outils de Recherche Web (Tavily)
*   **Agent sans outil** : Constat de la limitation des connaissances internes du modèle.
*   **Agent avec Web Search Tool** : Intégration de l'API Tavily permettant à l'agent d'effectuer des recherches sur le Web pour répondre à des questions d'actualité en temps réel ("Qui est le Président de commune actuel de Marrakech ?").

### 8. Gestion de la Mémoire de l'Agent
*   **Agent sans mémoire** : L'agent oublie les interactions précédentes à chaque nouvelle requête.
*   **Agent avec mémoire** : Intégration d'un checkpointer en mémoire (`InMemorySaver`) lié à un `thread_id` unique pour préserver l'historique des conversations et se souvenir des détails fournis par l'utilisateur.

---

## TP Principal : Le Chef Personnel Intelligent

L'exercice de synthèse consiste à implémenter un agent jouant le rôle d'un **Chef Cuisinier Personnel**.

### Fonctionnalités de l'Agent Chef :
1.  **Gestion des Ingrédients** : Reçoit et liste les ingrédients disponibles dans le réfrigérateur de l'utilisateur.
2.  **Mémoire des Préférences** : Se souvient à travers les sessions des préférences culinaires, aversions, ou restrictions alimentaires de l'utilisateur (ex. végétarien, n'aime pas le piment).
3.  **Recherche Web** : Utilise l'outil `web_search` de Tavily pour trouver de nouvelles idées de recettes or des techniques culinaires.
4.  **Recommandations sur-mesure** : Propose des recettes adaptées aux ingrédients disponibles tout en respectant strictement les contraintes alimentaires de l'utilisateur.

---

## Comment Exécuter le Projet ?

### Via Jupyter Notebook
Ouvrez le fichier de TP interactif :
```bash
jupyter notebook tp_agents_langchain.ipynb
```

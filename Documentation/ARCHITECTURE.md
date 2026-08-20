# 🏗️ Architecture du Projet PetCrossing3D

## Vue d'ensemble

PetCrossing3D est conçu pour être modulaire, scalable et maintenable. L'architecture suit un pattern MVC adapté aux jeux 3D.

## 📦 Modules Principaux

### 1. **Système d'Animaux de Compagnie** (`Scripts/Animals/`)
Gère la logique des animaux de compagnie et leur comportement.

```
Animals/
├── AnimalBase.cs          # Classe de base pour tous les animaux
├── AnimalBehavior.cs      # Système de comportement IA
├── AnimalState.cs         # États des animaux (Heureux, Triste, Fatigué, etc.)
├── AnimalAnimator.cs      # Gestion des animations
└── AnimalData.cs          # Données sérialisées des animaux
```

**Responsabilités :**
- Initialiser et mettre à jour l'état des animaux
- Gérer les besoins (Faim, Énergie, Bonheur)
- Déclencher les animations appropriées
- Sauvegarder/charger les données des animaux

### 2. **Système de Joueur** (`Scripts/Player/`)
Gère le contrôle du joueur et les interactions.

```
Player/
├── PlayerController.cs    # Contrôle du mouvement
├── PlayerInteraction.cs   # Système d'interaction avec le monde
├── PlayerInventory.cs     # Gestion de l'inventaire
└── PlayerCamera.cs        # Contrôle de la caméra
```

### 3. **Système d'Interface** (`Scripts/UI/`)
Toute l'interface utilisateur.

```
UI/
├── MainMenuUI.cs          # Menu principal
├── GameHUD.cs             # HUD en jeu
├── PetStatusPanel.cs      # Panneau de statut de l'animal
├── InventoryUI.cs         # Interface d'inventaire
└── SettingsUI.cs          # Paramètres
```

### 4. **Système de Jeu** (`Scripts/Gameplay/`)
Logique générale du jeu.

```
Gameplay/
├── GameManager.cs         # Gestionnaire principal du jeu
├── TimeManager.cs         # Cycle jour/nuit et saisons
├── SaveManager.cs         # Système de sauvegarde/chargement
├── EventSystem.cs         # Système d'événements
└── QuestManager.cs        # Gestion des quêtes
```

### 5. **Système Audio** (`Scripts/Audio/`)
Gestion des sons et musiques.

```
Audio/
├── AudioManager.cs        # Gestionnaire audio central
├── SoundEffect.cs         # Effets sonores
└── MusicManager.cs        # Gestion des musiques
```

## 🔄 Flux de Données

```
┌─────────────────────────────────────────┐
│         GameManager (Principal)          │
└─────────────────────────────────────────┘
         │              │              │
         ▼              ▼              ▼
┌──────────────┐ ┌──────────────┐ ┌──────────────┐
│   TimeManager│ │  SaveManager │ │EventSystem   │
└──────────────┘ └──────────────┘ └──────────────┘
         │              │              │
         ▼              ▼              ▼
┌──────────────┐ ┌──────────────┐ ┌──────────────┐
│PlayerController│AnimalManager│ QuestManager│
└──────────────┘ └──────────────┘ └──────────────┘
         │              │              │
         ▼              ▼              ▼
┌──────────────┐ ┌──────────────┐ ┌──────────────┐
│   PlayerUI   │ │   AnimalUI   │ │  GameUI      │
└──────────────┘ └──────────────┘ └──────────────┘
```

## 🎮 Cycle de Jeu Principal

```csharp
// Pseudo-code du cycle principal
while (GameRunning)
{
    // 1. Entrée utilisateur
    PlayerController.HandleInput();
    
    // 2. Mise à jour du jeu
    TimeManager.UpdateTime();
    AnimalManager.UpdateAnimals();
    QuestManager.UpdateQuests();
    
    // 3. Interactions
    PlayerInteraction.ProcessInteractions();
    
    // 4. Rendu
    RenderScene();
    
    // 5. Audio
    AudioManager.Update();
}
```

## 📊 État d'un Animal

```csharp
public class AnimalState
{
    public float Hunger { get; set; }      // 0-100
    public float Energy { get; set; }      // 0-100
    public float Happiness { get; set; }   // 0-100
    public float Health { get; set; }      // 0-100
    
    public AnimalMood CurrentMood
    {
        get
        {
            if (Health < 30) return AnimalMood.Sick;
            if (Energy < 20) return AnimalMood.Tired;
            if (Happiness < 30) return AnimalMood.Sad;
            if (Hunger > 80) return AnimalMood.Hungry;
            return AnimalMood.Happy;
        }
    }
}

public enum AnimalMood
{
    Happy,
    Sad,
    Hungry,
    Tired,
    Sick,
    Excited
}
```

## 🎨 Système d'Animations

Les animations sont triées par catégorie :

- **Idle** - Repos/inactivité
- **Walk** - Marche normale
- **Run** - Course rapide
- **Eat** - Manger
- **Sleep** - Dormir
- **Play** - Jouer
- **React** - Réactions aux événements

## 💾 Système de Sauvegarde

Structure JSON des données sauvegardées :

```json
{
  "version": "1.0",
  "player": {
    "name": "Joueur",
    "level": 10,
    "inventory": []
  },
  "animals": [
    {
      "id": 1,
      "name": "Fluffy",
      "species": "Lapin",
      "happiness": 85,
      "hunger": 30,
      "energy": 70,
      "health": 100
    }
  ],
  "gameTime": "2024-01-15T14:30:00Z",
  "quests": []
}
```

## 🔌 Pattern d'Événements

Le système utilise un Event Bus pour découpler les systèmes :

```csharp
// Publier un événement
EventSystem.Publish(new AnimalFedEvent { AnimalId = animalId });

// S'abonner à un événement
EventSystem.Subscribe<AnimalFedEvent>(OnAnimalFed);

private void OnAnimalFed(AnimalFedEvent evt)
{
    // Réagir à l'événement
}
```

## 🚀 Points d'Extension

- **Nouveaux types d'animaux** - Créer une classe dérivée de `AnimalBase`
- **Nouveaux UI** - Étendre la classe `UIBase`
- **Nouveaux événements** - Ajouter des événements dans `EventSystem`
- **Nouveau contenu** - Ajouter des assets dans les dossiers correspondants

## 📚 Références

- **Pattern MVC** - Séparation des responsabilités
- **Event-Driven Architecture** - Couplage faible entre systèmes
- **Scriptable Objects** (Unity) - Stockage des données sans code
- **Dependency Injection** - Injection des dépendances au démarrage

---

*Architecture v1.0 - Sujet à évolution*
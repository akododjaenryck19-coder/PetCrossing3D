# 🤝 Guide de Contribution

Merci d'être intéressé par la contribution à **PetCrossing3D** ! Ce document fournit des directives pour contribuer au projet.

## 📝 Comment Contribuer

### 1. Fork et Clone
```bash
git clone https://github.com/votre-username/PetCrossing3D.git
cd PetCrossing3D
```

### 2. Créer une Branche de Feature
```bash
git checkout -b feature/nom-de-votre-feature
```

Les noms de branches doivent suivre ce format :
- `feature/description` - Pour les nouvelles fonctionnalités
- `bugfix/description` - Pour les corrections de bugs
- `docs/description` - Pour la documentation

### 3. Committer vos Changements
```bash
git commit -m "Description claire et concise des changements"
```

**Format des messages de commit :**
```
[TYPE] Description courte

Description plus détaillée si nécessaire.

Fixes #123
```

Types acceptés :
- `feat:` - Nouvelle fonctionnalité
- `fix:` - Correction de bug
- `docs:` - Documentation
- `style:` - Formatage du code
- `refactor:` - Refactorisation
- `test:` - Ajout/modification de tests
- `chore:` - Tâches de maintenance

### 4. Push et Pull Request
```bash
git push origin feature/nom-de-votre-feature
```

Créez une Pull Request avec une description claire des changements.

## 🎨 Conventions de Code

### C# (Unity)
- Utilisez PascalCase pour les noms de classes et méthodes publiques
- Utilisez camelCase pour les variables locales
- Commentez le code complexe en français

```csharp
public class AnimalPet : MonoBehaviour
{
    private string petName;
    private float happiness;

    public void Feed()
    {
        // Logique pour nourrir l'animal
    }
}
```

### C++ (Unreal)
- Suivez les conventions d'Unreal Engine
- Préfixez les variables membres avec `m_`
- Utilisez des commentaires en français

```cpp
class AAnimalPet : public APawn
{
private:
    FString m_PetName;
    float m_Happiness;

public:
    void Feed();
};
```

## 🎯 Standards de Qualité

- ✅ Le code doit être testé
- ✅ Les commits doivent être atomiques (une seule fonction par commit si possible)
- ✅ Pas de code mort ou de fichiers inutilisés
- ✅ La documentation doit être à jour
- ✅ Les images/assets doivent être optimisées

## 🐛 Signaler un Bug

Si vous trouvez un bug :
1. Vérifiez qu'il n'existe pas déjà une issue pour ce bug
2. Créez une nouvelle issue avec :
   - Un titre clair et descriptif
   - Une description détaillée du bug
   - Les étapes pour reproduire
   - Le comportement attendu vs actuel
   - Des captures d'écran si applicable

## 💡 Suggestions de Features

Pour proposer une nouvelle feature :
1. Ouvrez une issue avec le label `enhancement`
2. Décrivez le cas d'usage
3. Expliquez pourquoi cette feature serait utile
4. Incluez des mockups/schémas si possible

## 📚 Documentation

- Mettez à jour la documentation pour toute nouvelle fonctionnalité
- Incluez des exemples d'utilisation
- Documentez les changements API publiques

## ✨ Bonnes Pratiques

1. **Petit et Focalisé** - Les PRs petites et ciblées sont plus faciles à revoir
2. **Testez localement** - Assurez-vous que vos changements fonctionnent avant de pusher
3. **Rebase avant merge** - Gardez l'historique propre
4. **Communiquez** - Posez des questions si vous êtes bloqué

## 🏆 Merci !

Votre contribution aide à faire de PetCrossing3D un projet incroyable. Merci pour votre soutien ! 🎮✨
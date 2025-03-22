# Joint Energy-Based Model

JEM (*Joint Energy-Based Model*) est un modèle basé sur l’énergie (EBM) qui combine **classification** et **génération d’images**. Il apprend simultanément la probabilité d’une image $p_{\theta}(x)$ et la probabilité conditionnelle d’une classe $p_{\theta}(y | x)$, permettant ainsi de classer des images tout en générant de nouvelles données.  

JEM repose sur un **réseau de neurones convolutif** qui extrait des caractéristiques des images et produit deux sorties principales :  

- **L'énergie** : $E_{\theta}(x)$ mesure la plausibilité de l’image dans l’espace appris par le modèle.
- **Les logits de classification** : $f_{\theta}(x)$ utilisés pour prédire la classe de l’image.  


L'entraînement de JEM repose sur plusieurs objectifs :  
1. **Classification supervisée** : Une perte de classification standard, comme l'entropie croisée, pour associer une image à un label.  
2. **Divergence contrastive** : Une régularisation qui aide à différencier les vraies images des échantillons générés.  
3. **Régularisation de l’énergie** : Une contrainte sur $E_{\theta}(x)$ pour améliorer la stabilité et la robustesse du modèle.  

JEM génère des images en utilisant une approche basée sur la **dynamique de Langevin** :
1. **Initialisation** : On commence avec une image contenant uniquement du bruit aléatoire.  
2. **Affinement progressif** : Un algorithme de type **MCMC (Monte Carlo Markov Chain)** modifie progressivement l’image pour la rendre plus réaliste. À chaque itération, l’image est ajustée en réduisant son énergie, de manière à se rapprocher d’un échantillon plausible du modèle.  
3. **Diversification** : Un **buffer de rééchantillonnage** est utilisé pour éviter de générer toujours les mêmes images et garantir une plus grande variété dans les échantillons produits.
Grâce à cette approche, JEM permet d’unifier **classification** et **génération**, exploitant ainsi pleinement les propriétés des modèles basés sur l’énergie.  

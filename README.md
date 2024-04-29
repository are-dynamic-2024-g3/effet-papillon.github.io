# L'EFFET PAPILLON DANS TOUTE SA SPLENDEUR
 
    Designed by the magnificients Suvana, Madina, Sathursjan

    
Liens vers les titres :
**|[Les bases de la théorie de l'attracteur de Lorenz](#introduction)|**
**[Les Equations et éléments à prendre en compte](#équations)|**
**[Comment modéliser le phénomène étudié](#modélisation)|**
**[Dépendance des paramètres du système/des conditions initiales ](#animation)|**
**[Bibiliographie](#ressources)|**
**[Tableau de bord](#calendrier)|**

L'effet papillon, ou aussi appelé attracteur de Lorenz, a été decouvert par Edward Lorenz, météorologue et mathématicien. En 1963, il développait une simulation des conditions atmosphériques avec 12 variables, et il remarque que la plus minuscule des différences dans les conditions initiales changeaient grandement les résultats. 

Il simplifia alors sa simulation pour n'avoir que 3 varibales tout en conservant cette dépendance sensible aux conditions initiales. Ce modèle simplifié décrit les cycles de convection dans l'atmosphère, qui est désormait plus connu sous le nom de *Système de Lorenz*. 

Ses recherches sont basées sur un principe fondamental, la dépendance sensible aux conditions initiales dans un système dynamique non linéaire.

<img width="680" alt="Capture d'écran 2024-03-08 093158" src="https://github.com/are-dynamic-2024-g3/effet-papillon.github.io/assets/160217704/ece84bb6-992d-44f9-a504-b22166f5597d">

# <a name="introduction"></a> Les bases de la théorie de l'attracteur de Lorenz   

Pour commencer, vous devez connaître ce qu'est le concept du théorie du chaos et la dépendence des conditions initial. 


Il y a trois points qui expliquent clairement les bases qui ont permis à la théorie de l’attracteur de Lorenz d’exister :

- La dépendance sensible aux conditions initiales
- La conséquence des changements des états initiaux : entraîner de grandes différences dans un état ultérieur
- Principalement tirée de la théorie du chaos, crée également par Edward Lorenz

Explication plus précise :

L’attracteur de Lorenz est la théorie qu’une simple action, qui paraît être un détail futile, peut avoir de conséquences hors-norme sur le système. Prenons un exemple :

On est ici dans un système dit chaotique, et vous allez comprendre pourquoi. Prenons un ensemble de boules de billard,et que l’on vient frapper une seule de ces boules, même en étant extrêmement précis, il est impossible que la boule de billard tape exactement au même endroit avec la même force deux fois de suite.
Ainsi, la conséquence qui va s’en suivre, c’est qu’il n’y aura jamais deux parties qui se ressembleront.

 ![billard](
 https://github.com/are-dynamic-2024-g3/effet-papillon.github.io/assets/160217704/d2a946f3-61cc-41fe-bf37-532a94e387ea)

Comme il n’a suffi que d’un tout petit écart au moment de la frappe pour obtenir un résultat totalement différent, on dit que le jeu du billard est un système chaotique.

En résumé, si deux états presque identiques, ils évolueront vers des états radicelement différent après les avoirs itérés à travers une fonction chaotique. 
 
Ici, on a un exemple assez générale de l’attracteur de Lorenz, passons maintenant à une explication plus « scientifique ».

# <a name="équations"></a>  Les Equations et éléments à prendre en compte

<img width="273" alt="Capture d'écran 2024-03-08 094334" src="https://github.com/are-dynamic-2024-g3/effet-papillon.github.io/assets/160217704/f453ed7e-c933-479c-b1d9-5f996019c8a0">

x, y, z :, x, y et z sont 3 variables, x représente l'écoulement convectif sur l'espace étudié, y et z sont les varation de température horizontal et vertical.  
σ, ρ, β : Ces éléments numériques sont les paramètre de l'attracteur de Lorenz, modulant les trajectoires et influençant la sensibilité aux conditions initiales. σ représents [le nombre de Pandtl](https://fr.wikipedia.org/wiki/Nombre_de_Prandtl). ρ représente la différence de témpérature entre le point le plus haut et le plus bas de l'atmosphère et β represente le rapport de la largeur à la hauteur du plan de l'atmosphère étudiés. 

- Ici, ce qu'il faut comprendre, c'est que les équations données représentent une forme géometrique complexe de l'attracteur de lorenz, ou plus précisément le comportement "chaotique" d'un système dynamique en trois dimensions.
- Les variables x, y, z, représentent un point d'intérêt dans l'espace en question, décrivant la position de ce point à un moment donné.
- σ, ρ, β, représentent les trajectoires et influencent la sensibilité aux conditions initiales, ce sont donc ces éléments là qui vont nous interesser car c'est selon ces variables , que les conditions initiales se définissent, et font qu'on obtienne des resultats totalement différents à la fin. 

Pour vous expliquer cette partie un peu plus en detail, nous allons la modeliser.


#  <a name="modélisation"></a> Comment modéliser le phénomène étudié 

Voici les étapes clés qui vont nous permettre de modéliser l'attracteur de lorenz, elles vous permettront de mieux cerner les paramètres.
### Les bibiliothèques utilisées:

```py
import numpy as np
import matplotlib.pyplot as plt
from scipy.integrate import odeint
```


### Définir les Équations du Système Dynamique:

- Établir les équations fondamentales de Lorenz.
- Description de la dynamique tridimensionnelle du système.

```py
sigma = 10
rho = 28
beta = 2.667
def lorenz(x, y, z, sigma, rho, beta):
    deriv_x = sigma*(y - x)
    deriv_y = rho*x - y - x*z
    deriv_z = x*y - beta*z
    return deriv_x, deriv_y, deriv_z
```
     

### Définir les Valeurs Initiales:

- Préciser les conditions de départ pour x, y, et z.
- Préciser le temps entre chaque pas. 
- Définir un tableau "t" qui représente les instants de temps auxquels le système de Lorenz est évalué.
- rôle majeur dans la trajectoire globale de l'Attracteur.
```py
dt = 0.009999
t = np.arange(0, dt*2000, dt) 
etat_initial = [0.0, 2.0, 6.0]
```


### Résolution de l'équation différentielle du système de Lorenz:

- Utiliser la fonction "odeint" pour pouvoir intégrer et ainsi résoudre l'équation différentielle du système.

- Obtenir les tableaux de x,y,z contenant les valeurs des variables x, y et z du système de Lorenz à différents instants de temps, ce qui nous permet ensuite de visualiser et d'analyser l'évolution de ces variables au fil du temps.

```py
solution = odeint(lorenz, etat_initial, t, args=(sigma, rho, beta))

x = solution[:, 0]
y = solution[:, 1]
z = solution[:, 2]
```

### Procéder au Plot:

- Transposer les résultats dans un graphique.
- Observer et analyser la forme résultante de l'Attracteur de Lorenz.
- Observer l'évolution des conditions initiales x,y,z en fonction du temps.
  
```py
ax = plt.figure().add_subplot(projection='3d')
ax.scatter(x, y, z,s = 2)
ax.plot(x, y, z, color = 'r')
ax.set_xlabel("X Axis")
ax.set_ylabel("Y Axis")
ax.set_zlabel("Z Axis")
ax.set_title("Lorenz Attractor")

plt.show()
```

![Capture d’écran_14-4-2024_131036_localhost](https://github.com/are-dynamic-2024-g3/effet-papillon.github.io/assets/160217704/6d5ae939-d231-4c2d-b3bc-3405a3f40a79)

```py
fig, ax = plt.subplots(1, 3, figsize=(10, 3))

ax[0].plot(t,x, color='r', alpha=1, linewidth=0.6)
ax[0].set_xlabel("TIME Axis")
ax[0].set_ylabel("X Axis")

ax[1].plot(t,y, color='b', alpha=1, linewidth=0.6)
ax[1].set_xlabel("TIME Axis")
ax[1].set_ylabel("Y Axis")


ax[2].plot(t,z, color='g', alpha=1, linewidth=0.6)
ax[2].set_xlabel("TIME Axis")
ax[2].set_ylabel("Z Axis")

plt.show()
```


![Capture d’écran_26-4-2024_10339_localhost](https://github.com/are-dynamic-2024-g3/effet-papillon.github.io/assets/160217704/a72b304b-5716-4e13-8ff5-baf5d0cdb4b9)


# <a name="animation"></a> Dépendance des paramètres du système/des conditions initiales 

Ici on retrouve les sliders effectués qui permettent de modifier les paramètres du systèmes de Lorenz ainsi que les conditions initiales manuellement pour mieux voir la différence dans la trajectoire de l'attracteur de lorenz.
nous avons réalisé une capture vidéo, il suffit de cliquer sur ce fichier.

##### **beta slider** 
[![](beta slider png.png)]( https://github.com/are-dynamic-2024-g3/effet-papillon.github.io/assets/160218534/bfac7989-f715-4363-b5ee-5d940a32acca)

##### **rho slider** 
[![](rho slider png.png)](https://github.com/are-dynamic-2024-g3/effet-papillon.github.io/assets/160218534/1224b559-0817-4ea0-b12b-bd570d5aa1b9)

##### **sigma slider** 
[![](sigma slider png.png)](https://github.com/are-dynamic-2024-g3/effet-papillon.github.io/assets/160218534/8bec67b9-86d6-4b76-8d34-5cce2c719ca5)


 
###  <a name="ressources"></a> Bibiliographie : 

[Comprendre la théorie](https://couleur-science.eu/?d=717abd--cest-quoi-un-attracteur-de-lorenzun-systeme-chaotique)

[Comprendre la théorie en détail](https://links.uwaterloo.ca/pmath370w14/PMATH370/lorenz%20Latex.pdf) 

[Visualisation des changements des paramètres en fonction du temps](https://tng-daryl.medium.com/visualizing-the-lorenz-attractor-in-julia-c9417f219e9b)

[Sliders](https://www.geeksforgeeks.org/matplotlib-slider-widget/amp/)

[Couleurs_matplotlib](https://matplotlib.org/stable/users/explain/colors/colormaps.html)

[Spicy.integrate](https://cpge.frama.io/fiches-cpge/Python/%C3%89quation%20diff%C3%A9rentielle/0-Equation%20diff%C3%A9rentielle/)

[Animation]( https://resteche.github.io/REsteche_blog/chaos%20theory/butterfly%20effect/python%20animation/2021/10/20/Lorenz_animation.html)

[Création_gif](https://www.developpez.net/forums/d1453508/autres-langages/python/calcul-scientifique/creer-gif-annime-pil/)

###  <a name="calendrier"></a> Tableau de bord : 

* SEANCE 1 : Nous avons rassemblé les informations sur l’attracteur de lorenz, réparti les tâches, et avons essayé de se familiariser avec github . 

* SEANCE 2 : Après avoir acquis les bases, nous avons fait la mise en page du site web, introduit l’attracteur de lorenz, sans codage, seulement du texte dans le readme. Cela nous a permis d’organiser le site et d’avoir un aperçu de ce qu’on pouvait faire ou non. Nous nous sommes basés sur le diaporama fait pour présenter notre projet, pour pouvoir agencer notre site.

* SEANCE 3 : Durant cette séance, nous nous sommes focalisés sur la modélisation et l’animation de l’attracteur de lorenz, l’idée était de pouvoir voir l’attracteur de lorenz sous ses différentes formes lorsque les conditions initiales sont modifiées. 

* SEANCE 4 : Nous nous sommes répartis les tâches qui nous restaient, améliorer la mise en page du readme, et avons travaillé sur les sliders de nos modélisations.

* SEANCE 5 : Nous avons importé des sliders interactifs avec matplotlib et %matplotlib notebook, nous sommes sur le peaufinement des modélisations, pour pouvoir les importer sur notre readme comme nous le souhaitions. Le principal problème était que nous ne pouvions pas faire de modèle interactifs avec l’utilisateur du site. Nous avons également exporté notre readme vers un site.

* SEANCE 6 : Nous avons rajouter des liens de racourcis dans le site pour accéder aux paragraphes plus rapidement, nous avons fait une recherche par rapport aux thèmes qu’on peut utiliser pour le site, et tester differents thèmes.

* SEANCE 7 :  Nous avons rajouté des liens de racourcis dans le site pour accéder à ces derniers plus rapidement, et avons rajouté un fichier mp4 pour la vidéo sur les sliders.
  
* SEANCE 8 : Nous avons fait des recherches plus détaillée sur les paramètres du système de Lorenz afin de bien expliquer le comportement de ces derniers lors du changement en fonction du temps et leurs influences sur la trajectoire. Nous avons rajouté un code pour les graphiques qui représentent les conditions initiales en focntion du temps.



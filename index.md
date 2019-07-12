# Python pour les SVT

## Exploiter une base de données

[Créer un DataFrame à partir d'un dictionnaire](#creatdf1)

## Etudier des séquences biologiques


## Faire un graphique

[Faire un graphique "simple" avec une seule courbe](#simplegraph)
[Annoter un graphique](#annotegraph)





# .
# .
# .






# Faire un graphique avec matplotlib.pyplot

<a name="simplegraph"></a>
## Un graphique "simple" avec une seule courbe.

### Importer les modules numpy et matplotlib.pyplot.

Par conventions, on les importe toujours de la manière suivante:

	import numpy as np
	import matplotlib.pyplot as plt

### Créer des listes de données.

On peut utiliser des listes "classiques":

	x = [0,1,2,3,4]
	y = [23,31,45,78]

Les deux listes doivent évidemment être de même longueur !

On peut aussi utiliser des array à une dimension avec numpy:

	x = np.arange(10) 
		
	y = 2*x + 5 

### Fermer les objets plt éventuellement existants.

	plt.close() 

### Réaliser le plot.

	plt.plot(x, y, "-*b", markersize=8, label="nom de la courbe")

Vous disposez alors d’un objet "plt" qui vous permet d’agir sur votre plot (y compris dans le shell après l’affichage du plot)

De nombreuses options sont possibles pour les "marker":

Options de ligne: "-" continue, "--" tirets 

Options de marker: *, +, o, ^

Options de couleur : b: bleu, k: noir, r: rouge, g: vert...

Pour faire un nuage de points (donc sans ligne), n’utilisez pas d’option de ligne, exemple: "+r"

### Utiliser l’objet `plt` .

<a name="annotegraph"></a>

#### Ajouter un titre aux axes:

	plt.xlabel("titre des abscisses", fontsize=8)
	plt.ylabel("titre des ordonnées", fontsize=8)

#### Afficher la legende (label de la courbe):

	plt.legend(loc='best', fontsize=8)

L’argument `loc="best"` permet de placer automatiquement la légende au meilleur endroit (c’est à dire là où elle ne va pas chevaucher une courbe)

#### Afficher le titre du graphique:

	plt.title("titre du graphique", fontsize=8)

#### Ajouter du texte sur le graphique:

	plt.text(2,8,"j'ecris ici si je veux !", fontsize=8) 

Le texte serra ajouté aux coordonnées x=2 ,  y=8

#### Modifier les limites des axes:

	plt.xlim(0,10)
	plt.ylim(0,25)

Ou équivalent :

	plt.axis([0,10,0,25])

#### Afficher le graphique:

	plt.show()

Même après avoir affiché le graphique, l’objet plt est toujours actif, il est encore possible de modifier le graphique (y compris dans le shell), pour voir les modifications apportées, il faut ré afficher le graphique `plt.show()`

#### Sauvegarder le graphique:

	plt.savefig("mon_graphique.png")
	
Le format par défaut est .png, mais il est possible de choisir un autre format de sauvegarde:

	plt.savefig("mon_graphique.pdf", format = "pdf")

#### Le code complet (sans la modification des axes), et le graphique correspondant:

	import numpy as np
	import matplotlib.pyplot as plt
	
	x = np.arange(10) 
	
	y = 2*x + 5 
	
	plt.close()
	
	plt.plot(x, y, "-*b", markersize=8, label="nom de la courbe")
	
	plt.xlabel("titre des abscisses", fontsize=8)
	plt.ylabel("titre des ordonnées", fontsize=8)
	
	plt.legend(loc='best', fontsize=8)
	
	plt.title("titre du graphique", fontsize=8)
	
	plt.text(2,8,"j'ecris ici si je veux !", fontsize=8) 
	
	plt.show()

![](https://gist.github.com/YannBouyeron/c0684bf235f2f2835369dffabf67d5c4/raw/IMG_1970.PNG)

## Un graphique avec plusieurs courbes.

	import numpy as np
	import matplotlib.pyplot as plt
	
	x = np.arange(10)
	
	plt.close() 
	
	plt.plot(x, 2*x, "-*b", markersize=8, label="nom de la courbe 1")
	
	plt.plot(x, 2*x + 5, "-ok", markersize=8, label="nom de la courbe 2")
	
	plt.plot(x, x**2, "-+r", markersize=8, label="nom de la courbe 3")
	
	plt.xlabel("titre des abscisses", fontsize=8)
	plt.ylabel("titre des ordonnées", fontsize=8)
	plt.legend(loc='best', fontsize=8)
	plt.title("titre du graphique", fontsize=8)
	plt.show()

![](https://gist.github.com/YannBouyeron/c0684bf235f2f2835369dffabf67d5c4/raw/IMG_1968.PNG)

## Un subplot (plusieurs graphiques sur la même figure)

	import numpy as np
	import matplotlib.pyplot as plt
	
	x = np.arange(10)
		
	y1 = 2*x
		
	y2 = x**2
		
	y3 = x**3
	
	y4 = 3*x + 6
	
	y5 = x**0.5
	
	
	plt.close()
	
	plt.figure(1)
	
	g1 = plt.subplot(221)
	plt.plot(x, y1, '-^k', label='courbe1', markersize=5)
	plt.title('titre 1', fontsize=10)
	plt.xlabel("X",fontsize=10)
	plt.ylabel("Y1",fontsize=10)
	plt.legend(fontsize=10)
	
	g2 = plt.subplot(222)
	plt.plot(x, y2, '-*b', label='courbe2', markersize=5)
	plt.title('titre 2', fontsize=10)
	plt.xlabel("X",fontsize=10)
	plt.ylabel("Y2",fontsize=10)
	plt.legend(fontsize=10)
	
	g3 = plt.subplot(223)
	plt.plot(x, y3, '--or', label='courbe3', markersize=5)
	plt.title('titre 3', fontsize=10)
	plt.xlabel("X",fontsize=10)
	plt.ylabel("Y3",fontsize=10)
	plt.legend(fontsize=10)
	
	g4 = plt.subplot(224)
	plt.plot(x, y4, '-+g', label='courbe4', markersize=5)
	plt.plot(x, y5, '--^y', label='courbe5', markersize=5)
	plt.title('titre 4', fontsize=10)
	plt.xlabel("X",fontsize=10)
	plt.ylabel("Y4",fontsize=10)
	plt.legend(fontsize=10)
	
	plt.tight_layout() 
	plt.show()



![](https://gist.github.com/YannBouyeron/c0684bf235f2f2835369dffabf67d5c4/raw/IMG_1967.PNG)

Chaque subplot possède une position exemple 223, ce qui correspond au 3° graphique dans une figure de 2 lignes et 2 colonnes.

Pour faire 2 graphiques superposés, utilisez les positions 211 (2 lignes, 1 colonne, graphique 1) et 212 (2 lignes, 1 colonne, graphique 2)

Pour faire 2 graphiques alignés, utilisez les positions 121 et 122

Après l’affichage, on conserve un accès sur chaque plt.subplot que l’on peut modifier, exemple:

	g1.xlim(0,20)

Il faut ensuite re afficher le graphique `plt.show()` pour voir les modifications.

## Utiliser matplotlib.plt sans interface graphique !

Si vous êtes un Ayatollah de la console GNU Linux et que vous n’avez pas d’interface graphique (sans dekstop), vous allez générer une belle erreur en tentant de créer un objet plt !

Pour éviter cela, il faut importer matplotlib de la manière suivante:

	import matplotlib
	matplotlib.use('Agg') 
	
	import matplotlib.pyplot as plt

Évidement vous ne pourrez pas faire de `plt.show()`, mais vous pourrez tout de même sauvegarder votre graphique avec `plt.savefig("mon_graphique.png")`


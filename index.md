# Python pour les SVT

## Sommaire des tutoriels.

## Exploiter une base de données.

[Créer un DataFrame à partir d'un dictionnaire](#creatdf1)

## Etudier des séquences biologiques.


## Faire un graphique.

[Faire un graphique "simple" avec une seule courbe](#simplegraph)




</br></br></br></br>

<a name="simplegraph"></a>
### Faire un graphique "simple" avec une seule courbe.

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

</br></br></br>

<a name="creatdf1"></a>
#### Créer un DataFrame à partir d'un dictionnaire

	>>> d = {"nom":("Diatta", "Sane", "Diouf"), "prenom":("Robert", "Jean", "Albert")}
	
	>>> df = pd.DataFrame(d)
	
	>>> df
	              nom  prenom
	        0  Diatta  Robert
	        1    Sane    Jean
		2   Diouf  Albert


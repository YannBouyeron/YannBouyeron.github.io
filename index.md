# Python pour les SVT

## Sommaire des tutoriels

## Exploiter une base de données

[Créer un DataFrame à partir d'un dictionnaire](#creatdf1)

## Etudier des séquences biologiques


## Faire un graphique


<a name="creatdf1"></a>
#### Créer un DataFrame à partir d'un dictionnaire

	>>> d = {"nom":("Diatta", "Sane", "Diouf"), "prenom":("Robert", "Jean", "Albert")}
	
	>>> df = pd.DataFrame(d)
	
	>>> df
	              nom  prenom
	        0  Diatta  Robert
	        1    Sane    Jean
		2   Diouf  Albert


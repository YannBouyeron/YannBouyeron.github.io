### Créer un DataFrame à partir d’un dictionnaire de tuples:

	>>> d = {"nom":("Diatta", "Sane", "Diouf"), "prenom":("Robert", "Jean", "Albert")}
	
	>>> df = pd.DataFrame(d)
	
	>>> df
	        nom  prenom
		0  Diatta  Robert
		1    Sane    Jean
		2   Diouf  Albert

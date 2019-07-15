# Python pour les SVT

## Exploiter une base de données avec Pandas

[Importer une base de données au format SQL](#importsql)

[Importer une base de données au format CSV](#importcsv)

[Importer une base de données au format xlsx](#importxlsx)

[Créer une base de données au format SQL](#creatsql)

[Créer une base de données au format CSV](#creatcsv)

[Créer une base de données au format xlsx](#creatxlsx)

[Modifier une base de données au format SQL](#setsql)

[Modifier une base de données au format CSV](#setcsv)

[Modifier une base de données au format xlsx](#setxlsx)



#### Utiliser un DataFrame (tableau 2D) avec Pandas

[Créer un DataFrame à partir d'un dictionnaire](#creatdfdico)

[Créer un DataFrame à partir d'une liste](#creatdfliste)

[Afficher un aperçu des premières lignes d'un DataFrame](#headdf)

[Sélectionner une colonne par son nom](#selcollabel)

[Sélectionner un élément à partir de l'index de sa ligne et du nom de sa colonne](#selel)

[Sélectionner des lignes et des colonnes](#selrawcol)

[Ajouter des titres / labels aux colonnes et aux lignes](#addlabel)

[Ajouter des colonnes](#addcol)

[Ajouter des lignes](#addraw)

[Supprimer des colonnes](#delcol)

[Supprimer des lignes](#delraw)

## Etudier des séquences biologiques avec [Genopy](https://gist.github.com/YannBouyeron/3eb3aa7a79fadb3350096dec0bb5b004)

[Créer des séquences](#creatseq)

[Créer des fichiers fasta](#creatfasta)

[Convertir des fichiers .edi (anagene) en fichiers fasta](#convedi)

[Rechercher et afficher des séquences](#openseq)

[Transcrire](#transc)

[Traduire](#transl)

[Rétro-Transcrire](#rt)

[Comparer des séquences: alignement par paires](#needlewater)

[Comparer des séquences: alignement multiple (clustal)](#clustal)

[Afficher et sauvegarder une matrice de distances](#matrix)

[Tracer un arbre phylogénétique à partir d'une matrice de distances](#phylomatrix)

[Tracer un arbre phylogénétique à partir d'une liste de séquences](#phyloseq)

## Faire un graphique

#### Avec matplotlib.pyplot

[Faire un graphique "simple" avec une seule courbe](#simplegraph)

[Faire un graphique avec plusieurs courbes](#multigraph)

[Légender un graphique](#annotegraph)

[Sauvegarder un graphique](#savegraph)

[Mise en page de plusieurs graphiques: réaliser un subplot](#subplot)

#### Avec Pandas

...

## Tutoriel Python3

[Les variables](https://gist.github.com/YannBouyeron/18aca47587fe3e153e1e630af7640674#variable)

[Les entrées et les sorties](https://gist.github.com/YannBouyeron/18aca47587fe3e153e1e630af7640674#intout)

[Les booléens](https://gist.github.com/YannBouyeron/18aca47587fe3e153e1e630af7640674#bool)

[Les structures conditionnelles if elif else](https://gist.github.com/YannBouyeron/18aca47587fe3e153e1e630af7640674#ifelse)

[La boucle while](https://gist.github.com/YannBouyeron/18aca47587fe3e153e1e630af7640674#while)

[Les listes](https://gist.github.com/YannBouyeron/18aca47587fe3e153e1e630af7640674#listes)

[Les dictionnaires](https://gist.github.com/YannBouyeron/18aca47587fe3e153e1e630af7640674#dico)

[Manipuler les chaines de caractères str](https://gist.github.com/YannBouyeron/18aca47587fe3e153e1e630af7640674#str)

[Les fonctions](https://gist.github.com/YannBouyeron/d11d025a5c1460f1a201fea08df36f78)

## Python compléments

[Utiliser le module time de python](https://gist.github.com/YannBouyeron/1083709633f78e6804602a7ac6ae4bfa)

[Les modules os, glob, shutil et subprocess](https://gist.github.com/YannBouyeron/941817d79b83a4b87c5a63580229cbbd)

[Les listes en compréhension](https://gist.github.com/YannBouyeron/4ebc800d28e1d035025faf5811812a01)

[Introduction à Numpy](https://gist.github.com/YannBouyeron/784af9b808c2accb42de45d1ddbfab0b)

[Utiliser le module json de python](https://gist.github.com/YannBouyeron/39fafc26b94dfc459589c8d9e82637b6)

[Lire et ecrire un fichier avec python](https://gist.github.com/YannBouyeron/6d32a8ba6bd782106c02c08dfad54ca3)


______________________________________________________________________________________________________________________________
------------------------------------------------------------------------------------------------------------------------------


______________________________________________________________________________________________________________________________
------------------------------------------------------------------------------------------------------------------------------

# Génopy

### Installation

<a name="creatseq"></a>

### Créer des séquences

Le module genopy dépend de biopython, on peut créer des sequences sous deux types d'objets différents: les objets Seq et SeqRecord. 

Créer un objet Seq

    >>> from genopy import *
       
    >>> s1 = Seq("ATTCGCTCGTAATAGATGGCTCTATATAGATAGGCGCATAGCATCGATGTAGCTTAGCCGT") 
    >>> s1
    Seq('ATTCGCTCGTAATAGATGGCTCTATATAGATAGGCGCATAGCATCGATGTAGCT...CGT')
    
La fonction toSeq de genopy permet de créer plus facilement des objets Seq. Elle ajoute automatiquement le type.
 
    >>> s2 = toSeq("ATTCGCTCGTAATAGATGGCTCTATATAGATAGGCGAATAGCATCGATGTAGCTTACCCGT")
    >>> s2
    Seq('ATTCGCTCGTAATAGATGGCTCTATATAGATAGGCGAATAGCATCGATGTAGCT...CGT', IUPACUnambiguousDNA()) 
    
Les objets SeqRecord contiennent davantage d'informations:

    >>> sr1 = SeqRecord(s1, id="sequence1", name="sequence1", description="une sequence")
    >>> sr1
    SeqRecord(seq=Seq('ATTCGCTCGTAATAGATGGCTCTATATAGATAGGCGCATAGCATCGATGTAGCT...CGT'), id='sequence1', name='sequence1',      description='une sequence', dbxrefs=[])
    
    >>> sr2 = SeqRecord(s2, id="sequence2", name="sequence2", description="une autre sequence")
    >>> sr2
    SeqRecord(seq=Seq('ATTCGCTCGTAATAGATGGCTCTATATAGATAGGCGAATAGCATCGATGTAGCT...CGT', IUPACUnambiguousDNA()), id='sequence2', name='sequence2', description='une sequence', dbxrefs=[])

<a name="creatfasta"></a>

### Sauvegarder un ou plusieurs SeqRecord dans un ou plusieurs fichiers fasta

Créer un fasta contenant un seul SeqRecord. Le fichier fasta serra enregistré dans le repertoire courant et portera le nom du SeqRecord avec l'extension .fas

    >>> mkfas(sr1)

    
Créer plusieurs fichiers fasta mono séquence:
    
    >>> mkfas(sr1, sr2)

Créer un fasta multisequence contenant plusieurs SeqRecord. Le fichier fasta serra enregistré dans le path indiqué en argument:

    >>> mkfasx("myfasta.fas", sr1, sr2)



<a name="convedi"></a>

### Convertir des fichiers anagène avec l'extension .edi en fichiers fasta

On commence par importer les modules genopy et os:

    >>> from genopy import *
    >>> import os

On liste les fichiers du repertoire dans lequel on se trouve (ou un autre repertoire si on indique son path en argument de listdir):

    >>> ld = os.listdir()
    >>> 
    >>> ld
    ['__pycache__', 'genes-Opsines.edi', 'emb.aln', 'comp.aln', 'primates.fas', 'allelesFamillechoree.edi', 'genopy.py', 'tyrfamille4.fas', 'globines-beta-vertebres.fas', 'comp.dnd', 'myfasta.fas']

On remarque ici deux fichiers en .edi
On utilise une boucle for pour selectionner les fichiers .edi et les convertir en .fas grace à la fonction edi2fasta. Cette fonction attend 2 arguments: edi2fasta(file_name.edi, file_name.fas):

    >>> for i in ld:
    ...     if i[len(i)-4:] == ".edi":
    ...             edi2fasta(i, i[:len(i)-4]+".fas")
    ... 
    >>> 

On liste à nouveau les fichiers du repertoire:

    >>> os.listdir()
    ['__pycache__', 'genes-Opsines.edi', 'allelesFamillechoree.fas', 'emb.aln', 'comp.aln', 'primates.fas', 'allelesFamillechoree.edi', 'genopy.py', 'genes-Opsines.fas', 'tyrfamille4.fas', 'globines-beta-vertebres.fas', 'comp.dnd', 'myfasta.fas']
    

<a name="openseq"></a>

### Ouvrir des séquences

Les séquences doivent être hébergées localement.

On commence par rechercher les séquences avec la fonction 'search()' :

    >>> q = search("Opsine")
    >>> 
    >>> q
    [SeqRecord(seq=Seq('ATGGCCCAGCAGTGGAGCCTCCAAAGGCTCGCAGGCCGCCATCCGCAGGACAGC...TGA', SingleLetterAlphabet()), id='gene_opsine_rouge', name='gene_opsine_rouge', description='gene_opsine_rouge red opsin Homo sapiens opsin 1 (cone pigments), mRNA', dbxrefs=[]), SeqRecord(seq=Seq('ATGGCCCAGCAGTGGAGCCTCCAAAGGCTCGCAGGCCGCCATCCGCAGGACAGC...TGA', SingleLetterAlphabet()), id='gene_opsine_verte', name='gene_opsine_verte', description='gene_opsine_verte red opsin Homo sapiens opsin 1 (cone pigments), mRNA', dbxrefs=[]), SeqRecord(seq=Seq('ATGAGAAAAATGTCGGAGGAAGAGTTTTATCTGTTCAAAAATATCTCTTCAGTG...TGA', SingleLetterAlphabet()), id='gene_opsine_bleue', name='gene_opsine_bleue', description='gene_opsine_bleue Blue opsin Homo sapiens opsin 1 (cone pigments), mRNA', dbxrefs=[])]

On obtient une liste de SeqRecord correspondant à notre recherche.

    >>> len(q)
    3
    >>> 
    >>> for i, j in enumerate(q):
    ...     print(str(i) + " " + j.name)
    ... 
    0 gene_opsine_rouge
    1 gene_opsine_verte
    2 gene_opsine_bleue

On peut alors afficher la séquence du gène de l'opsine verte dont l'indice dans la liste est 1 avec la fonction 'show()':

    >>> show(q[1])


          ATGGCCCAGCAGTGGAGCCTCCAAAGGCTCGCAGGCCGCCATCCGCAGGACAGCTATGAG
          ----:----|----:----|----:----|----:----|----:----|----:----|
                   10        20        30        40        50        60

          GACAGCACCCAGTCCAGCATCTTCACCTACACCAACAGCAACTCCACCAGAGGCCCCTTC
          ----:----|----:----|----:----|----:----|----:----|----:----|
                   70        80        90        100       110       120

          GAAGGCCCGAATTACCACATCGCTCCCAGATGGGTGTACCACCTCACCAGTGTCTGGATG
          ----:----|----:----|----:----|----:----|----:----|----:----|
                   130       140       150       160       170       180

          ATCTTTGTGGTCATTGCATCCGTTTTCACAAATGGGCTTGTGCTGGCGGCCACCATGAAG
          ----:----|----:----|----:----|----:----|----:----|----:----|
                   190       200       210       220       230       240

          TTCAAGAAGCTGCGCCACCCGCTGAACTGGATCCTGGTGAACCTGGCGGTCGCTGACCTG
          ----:----|----:----|----:----|----:----|----:----|----:----|
                   250       260       270       280       290       300

          GCAGAGACCGTCATCGCCAGCACTATCAGCGTTGTGAACCAGGTCTATGGCTACTTCGTG
          ----:----|----:----|----:----|----:----|----:----|----:----|
                   310       320       330       340       350       360



(la séquence n'est pas représentée entierement dans ce tutoriel)



### Transcrire, Traduire, Rétro-transcrire

<a name="transc"></a>

    >>> dna = q[0]
    >>> 
    >>> dna
    SeqRecord(seq=Seq('ATGGCCCAGCAGTGGAGCCTCCAAAGGCTCGCAGGCCGCCATCCGCAGGACAGC...TGA', SingleLetterAlphabet()), id='gene_opsine_rouge', name='gene_opsine_rouge', description='gene_opsine_rouge red opsin Homo sapiens opsin 1 (cone pigments), mRNA', dbxrefs=[])

#### Transcrire

    >>> rna = transcribe(dna)
    >>> rna
    SeqRecord(seq=Seq('AUGGCCCAGCAGUGGAGCCUCCAAAGGCUCGCAGGCCGCCAUCCGCAGGACAGC...UGA', RNAAlphabet()), id='gene_opsine_rouge.rna', name='gene_opsine_rouge.rna', description='transcription de [gene_opsine_rouge red opsin Homo sapiens opsin 1 (cone pigments), mRNA]', dbxrefs=[])


<a name="transl"></a>

#### Traduire

    >>> help(translate)
    Help on function translate in module genopy:

    translate(*seq, table_id=1, to_stop=True, stop_symbol=' ', cds=True, out=False)
    Traduction d'un ou plusieurs dna ou rna SeqRecord. Si out == True, chaque proteine est sauvegardée dans un fasta. Return proteine SeqRecord ou une liste de proteines SeqRecord
 
> ORF: open reading frame ou phase ouverte de lecture, c'est la séquence du brin non transcrit (brin codant) de l'adn (ou de l'arn pré-messager) située entre le premier codon initiateur jusqu'au premier codon stop 
> 
> CDS: coding sequence ou séquence codante, c'est l'ORF sans les introns

Il est possible de choisir la table du code génétique utilisée (par défaut c'est le code standard)

L'argument to_stop = True permet d'arreter la traduction au codon stop

L'argument stop_symbol permet de spécifier la représentation de l'arret de la traduction

L'argument cds = True implique que la traduction commencera au premier codon initiateur rencontré et se terminera au premier codon stop rencontré sur le cadre de lecture. La majorité des séquences importées depuis anangene sont déjà des CDS, donc ca change rien; mais ce n'est pas le cas des fasta téléchargés depuis les banques de séquences. 

    >>> pep = translate(rna)
    >>> pep
    SeqRecord(seq=Seq('MAQQWSLQRLAGRHPQDSYEDSTQSSIFTYTNSNSTRGPFEGPNYHIAPRWVYH...SPA', ExtendedIUPACProtein()), id='gene_opsine_rouge.rna.prot', name='gene_opsine_rouge.rna.prot', description='traduction de [transcription de [gene_opsine_rouge red opsin Homo sapiens opsin 1 (cone pigments), mRNA]]', dbxrefs=[])

    >>> show(pep)


          MetAlaGlnGlnTrpSerLeuGlnArgLeuAlaGlyArgHisProGlnAspSerTyrGluAspSerThrGlnSerSerIlePheThrTyr
           -  -  -  -  :  -  -  -  -  |  -  -  -  -  :  -  -  -  -  |  -  -  -  -  :  -  -  -  -  | 
                                      10                            20                            30

          ThrAsnSerAsnSerThrArgGlyProPheGluGlyProAsnTyrHisIleAlaProArgTrpValTyrHisLeuThrSerValTrpMet
           -  -  -  -  :  -  -  -  -  |  -  -  -  -  :  -  -  -  -  |  -  -  -  -  :  -  -  -  -  | 
                                      40                            50                            60

          IlePheValValThrAlaSerValPheThrAsnGlyLeuValLeuAlaAlaThrMetLysPheLysLysLeuArgHisProLeuAsnTrp
           -  -  -  -  :  -  -  -  -  |  -  -  -  -  :  -  -  -  -  |  -  -  -  -  :  -  -  -  -  | 
                                      70                            80                            90

          IleLeuValAsnLeuAlaValAlaAspLeuAlaGluThrValIleAlaSerThrIleSerIleValAsnGlnValSerGlyTyrPheVal
           -  -  -  -  :  -  -  -  -  |  -  -  -  -  :  -  -  -  -  |  -  -  -  -  :  -  -  -  -  | 
                                      100                           110                           120

          LeuGlyHisProMetCysValLeuGluGlyTyrThrValSerLeuCysGlyIleThrGlyLeuTrpSerLeuAlaIleIleSerTrpGlu
           -  -  -  -  :  -  -  -  -  |  -  -  -  -  :  -  -  -  -  |  -  -  -  -  :  -  -  -  -  | 
                                      130                  

<a name="rt"></a>

#### Rétro transcrire

    >>> rna
    SeqRecord(seq=Seq('AUGGCCCAGCAGUGGAGCCUCCAAAGGCUCGCAGGCCGCCAUCCGCAGGACAGC...UGA', RNAAlphabet()), id='gene_opsine_rouge.rna', name='gene_opsine_rouge.rna', description='transcription de [gene_opsine_rouge red opsin Homo sapiens opsin 1 (cone pigments), mRNA]', dbxrefs=[])
    
    >>> help(retro_transcribe)
    Help on function retro_transcribe in module genopy:

    retro_transcribe(*seq, out=False)
    Retro transcription d'un ou plusieurs rna SeqRecord. Si out == True, chaque dna est sauvegardé dans un fasta. Return dna SeqRecord ou une liste de dna SeqRecord


    >>> dna_c = retro_transcribe(rna)
    >>> dna_c
    SeqRecord(seq=Seq('ATGGCCCAGCAGTGGAGCCTCCAAAGGCTCGCAGGCCGCCATCCGCAGGACAGC...TGA', DNAAlphabet()), id='gene_opsine_rouge.rna.dnac', name='gene_opsine_rouge.rna.dnac', description='retro transcription de [transcription de [gene_opsine_rouge red opsin Homo sapiens opsin 1 (cone pigments), mRNA]]', dbxrefs=[])
    >>> 
    >>> dna.seq == dna_c.seq
    True


<a name="needlewater"></a>

### Comparer deux séquences: alignement par Needle ou Water

On commence par rechercher des séquences:

    >>> q = search("primates")
    >>> 
    >>> len(q)
    7
    >>> 
    >>> q[0]
    SeqRecord(seq=Seq('TTCTTTCATGGGGAAGCAGATTTGGGTGCCACCCAAGTATTGACTCACCCATCA...CAT', SingleLetterAlphabet()), id='Refhumaine.adn', name='Refhumaine.adn', description=' Refhumaine.adn', dbxrefs=[])

On va ensuite comparer les séquences 2 à 2. 

Il est possible de faire un alignement global (needle) ou local (water)

    >>> help(needle)
    Help on function needle in module genopy:

    needle(*seq, gapopen=10, gapextend=0.5, out='emb.aln')
         Alignement global par la methode de Needleman
    
    arguments:
            
            seq: couple de 2 SeqRecord à aligner
            gapopen: pénalité de gap
            gapextend: pénalité d'expansion
            out: nom du fichier emboss créé
            
    return: un objet align

L'alignement est enregistré par défaut dans le fichier emb.aln (qui serra écrasé au prochain alignement réalisé)

Dans les 2 cas on peut eventuellement modifier les pénalités pour les ouvertures ou les extensions de gap.


    >>> n = needle(q[0], q[1])
    >>> 
    >>> w = water(q[0], q[1])
    >>> 
    >>> n
    <<class 'Bio.Align.MultipleSeqAlignment'> instance (2 records of length 365, SingleLetterAlphabet()) at 70615df0>
    >>> w
    <<class 'Bio.Align.MultipleSeqAlignment'> instance (2 records of length 361, SingleLetterAlphabet()) at 7061def0>


On obtient des objets "align" que l'on peut alors exploiter de différentes façons:

Obtenir des informations de base sur l'alignement:

    >>> print(n)
    SingleLetterAlphabet() alignment with 2 rows and 365 columns
    TTCTTTCATGGGGAAGCAGATTTGGGTGCCACCCAAGTATTGAC...--- Refhumaine.adn
    TTCTTTCATGGGGGATCAGATTTGGGTACCACCCCAGT----AC...GGA Orangoutan.adn
    
    >>> n.
    n.add_sequence(          n.append(                n.extend(                n.get_alignment_length(  
    n.annotations            n.column_annotations     n.format(                n.sort(                  
    
    >>> n.get_alignment_length()
    365
    
    >>> len(n)
    2
    
    >>> n[0]
    SeqRecord(seq=Seq('TTCTTTCATGGGGAAGCAGATTTGGGTGCCACCCAAGTATTGACTCACCCATCA...---', SingleLetterAlphabet()), id='Refhumaine.adn', name='<unknown name>', description='Refhumaine.adn', dbxrefs=[])
 


Afficher l'alignement avec les fonctions shogenix(), showanag(), (ou showgenix3() pour les séquences peptidiques avec acides aminés représentés à trois lettres)

L'affichage via showgenix représente toutes les séquences. Les similitudes sont symbolisées par une * et les délétions par des - . 

    >>> showgenix(n)


                          ************* * *********** ****** ***    **  ******   ** * 
    Refhumaine.adn        TTCTTTCATGGGGAAGCAGATTTGGGTGCCACCCAAGTATTGACTCACCCATCAACAACC
    Orangoutan.adn        TTCTTTCATGGGGGATCAGATTTGGGTACCACCCCAGT----ACCGACCCATTTCCAGCG

                          ----:----|----:----|----:----|----:----|----:----|----:----|
                                   10        20        30        40        50        60



                          * ****************** ********** *********   **   ** **  *** 
    Refhumaine.adn        G-CTATGTATTTCGTACATTACTGCCAGCCACCATGAATATTGTACGGTAC-CATAAAT-
    Orangoutan.adn        GCCTATGTATTTCGTACATTCCTGCCAGCCAACATGAATAT--CACCCAACACAACAATC

                          ----:----|----:----|----:----|----:----|----:----|----:----|
                                   70        80        90        100       110       120


L'affichage via showanag utilise le même mode de symbolisation que le logiciel anagene.

    >>> showanag(n)


                          ************* * *********** ****** ***    **  ******   ** * 
    Refhumaine.adn        TTCTTTCATGGGGAAGCAGATTTGGGTGCCACCCAAGTATTGACTCACCCATCAACAACC
    Orangoutan.adn        -------------G-T-----------A------C---____--CG------TTC--G-G

                          ----:----|----:----|----:----|----:----|----:----|----:----|
                                   10        20        30        40        50        60



                          * ****************** ********** *********   **   ** **  *** 
    Refhumaine.adn        G_CTATGTATTTCGTACATTACTGCCAGCCACCATGAATATTGTACGGTAC_CATAAAT_
    Orangoutan.adn        -C------------------C----------A---------__C--CCA--A--AC---C

                          ----:----|----:----|----:----|----:----|----:----|----:----|
                                   70        80        90        100       110       120
                                                                  




Il est aussi possible de lire l'alignement enregistré dans le fichier emb.aln avec la fonction reademboss() 


    >>> help(reademboss)
    Help on function reademboss in module genopy:

    reademboss(path='emb.aln')
        Cette fonction affiche le contenu de l'alignement emboss contenu dans le fichier à l'adresse "path", et return un objet align


    >>> n = needle(q[0], q[1])

    >>> reademboss("emb.aln") 

    ########################################
    # Program: needle
    # Rundate: Sun 14 Jul 2019 11:13:59
    # Commandline: needle
    #    -outfile emb.aln
    #    -asequence seqa.fas
    #    -bsequence seqb.fas
    #    -gapopen 10
    #    -gapextend 0.5
    # Align_format: srspair
    # Report_file: emb.aln
    ########################################

    #=======================================
    #
    # Aligned_sequences: 2
    # 1: Refhumaine.adn
    # 2: Orangoutan.adn
    # Matrix: EDNAFULL
    # Gap_penalty: 10.0
    # Extend_penalty: 0.5
    #
    # Length: 365
    # Identity:     255/365 (69.9%)
    # Similarity:   255/365 (69.9%)
    # Gaps:          40/365 (11.0%)
    # Score: 824.5
    # 
    #
    #=======================================

    Refhumaine.ad      1 TTCTTTCATGGGGAAGCAGATTTGGGTGCCACCCAAGTATTGACTCACCC     50
                         |||||||||||||.|.|||||||||||.||||||.|||    ||..||||
    Orangoutan.ad      1 TTCTTTCATGGGGGATCAGATTTGGGTACCACCCCAGT----ACCGACCC     46

    Refhumaine.ad     51 ATCAACAACCG-CTATGTATTTCGTACATTACTGCCAGCCACCATGAATA     99
                         ||...||.|.| ||||||||||||||||||.||||||||||.||||||||
    Orangoutan.ad     47 ATTTCCAGCGGCCTATGTATTTCGTACATTCCTGCCAGCCAACATGAATA     96


    #---------------------------------------
    #---------------------------------------

    <<class 'Bio.Align.MultipleSeqAlignment'> instance (2 records of length 365, SingleLetterAlphabet()) at 70603ab0>


(Les alignements ne sont pas représentés en entier dans ce tutoriel)

Il est possible d'afficher le % de similitudes ou de différences en utilisant la fonction reademboss (comme ci dessous) ou en affichant la matrice de distance avec la fonction matrix()

    >>> m = matrix(n)
    >>> print(m)
    Refhumaine.adn  0
    rangoutan.adn   0.3013698630136986      0
                    Refhumaine.adn          Orangoutan.adn

<a name="clustal"></a>

### Comparaison multiple de séquences avec Clustal

On commence par importer des séquences:

    >>> q = search("tyr")
    >>> 
    >>> len(q)
    25
    >>> 
    >>> q[0]
    SeqRecord(seq=Seq('ATGCTCCTGGCTGTTTTGTACTGCCTGCTGTGGAGTTTCCAGACCTCCGCTGGC...TAA', SingleLetterAlphabet()), id='Tyrcod2', name='Tyrcod2', description="Tyrcod2  Partie strictement codante d'un allele du gene de la tyrosinase (ref erence 2).", dbxrefs=[])

Puis on utilise la fonction clustal:

    >>> help(clustal)
    Help on function clustal in module genopy:

    clustal(*seq, out='comp.aln', std=False)
        Alginement multiple ClustalW
    
    arguments:
            
            seq: liste des SeqRecord à aligner
            out: path du fichier contenant l'alignement créé
            std: bool, si True, return align et stdout , defaut = False
            
    Return: l'objet align



    >>> c = clustal(*q[5:9])
    >>> c
    <<class 'Bio.Align.MultipleSeqAlignment'> instance (4 records of length 1590, SingleLetterAlphabet()) at 704f06f0>
    
Affichage simple: 

    >>> print(c)
    SingleLetterAlphabet() alignment with 4 rows and 1590 columns
    ATGCTCCTGGCTGTTTTGTACTGCCTGCTGTGGAGTTTCCAGAC...TAA F4_I2all1
    ATGCTCCTGGCTGTTTTGTACTGCCTGCTGTGGAGTTTCCAGAC...TAA F4_I2all2
    ATGCTCCTGGCTGTTTTGTACTGCCTGCTGTGGAGTTTCCAGAC...TAA F4_I1all2
    ATGCTCCTGGCTGTTTTGTACTGCCTGCTGTGGAGTTTCCAGAC...TAA F4_I1all1
    >>> 

Méthodes applicables à l'ojet align:

    >>> c.
    c.add_sequence(          c.append(                c.extend(                c.get_alignment_length(  
    c.annotations            c.column_annotations     c.format(                c.sort(                  
    
    
Affichage au format clustal:

    >>> print(c.format("clustal"))
    CLUSTAL 2.1 multiple sequence alignment

   
    F4_I2all1     ATGCTCCTGGCTGTTTTGTACTGCCTGCTGTGGAGTTTCCAGACCTCCGC
    F4_I2all2     ATGCTCCTGGCTGTTTTGTACTGCCTGCTGTGGAGTTTCCAGACCTCCGC
    F4_I1all2     ATGCTCCTGGCTGTTTTGTACTGCCTGCTGTGGAGTTTCCAGACCTCCGC
    F4_I1all1     ATGCTCCTGGCTGTTTTGTACTGCCTGCTGTGGAGTTTCCAGACCTCCGC
                  **************************************************


Affichage au format phylip:

    >>> print(c.format("phylip"))
    4 1590
    F4_I2all1  ATGCTCCTGG CTGTTTTGTA CTGCCTGCTG TGGAGTTTCC AGACCTCCGC
    F4_I2all2  ATGCTCCTGG CTGTTTTGTA CTGCCTGCTG TGGAGTTTCC AGACCTCCGC
    F4_I1all2  ATGCTCCTGG CTGTTTTGTA CTGCCTGCTG TGGAGTTTCC AGACCTCCGC
    F4_I1all1  ATGCTCCTGG CTGTTTTGTA CTGCCTGCTG TGGAGTTTCC AGACCTCCGC

               TGGCCATTTC CCTAGAGCCT GTGTCTCCTC TAAGAACCTG ATGGAGAAGG
               TGGCCATTTC CCTAGAGCCT GTGTCTCCTC TAAGAACCTG ATGGAGAAGG
               TGGCCATTTC CCTAGAGCCT GTGTCTCCTC TAAGAACCTG ATGGAGAAGG
               TGGCCATTTC CCTAGAGCCT GTGTCTCCTC TAAGAACCTG ATGGAGAAGG


Affichage au format genix:

    >>> showgenix(c)


                     ************************************************************
    F4_I2all1        ATGCTCCTGGCTGTTTTGTACTGCCTGCTGTGGAGTTTCCAGACCTCCGCTGGCCATTTC
    F4_I2all2        ATGCTCCTGGCTGTTTTGTACTGCCTGCTGTGGAGTTTCCAGACCTCCGCTGGCCATTTC
    F4_I1all2        ATGCTCCTGGCTGTTTTGTACTGCCTGCTGTGGAGTTTCCAGACCTCCGCTGGCCATTTC
    F4_I1all1        ATGCTCCTGGCTGTTTTGTACTGCCTGCTGTGGAGTTTCCAGACCTCCGCTGGCCATTTC

                     ----:----|----:----|----:----|----:----|----:----|----:----|
                              10        20        30        40        50        60

Il est aussi possible de faire un affichage de l'alignement au format anagene avec la fonction showanag().

<a name="matrix"></a>

#### Afficher une matrice de distances:

La fonction matrix attend un alignement (needle, water ou clustal) en argument obligatoire:

    >>> m = matrix(c)
    >>> print(m)
    F4_I2all1       0
    F4_I2all2       0.0006289308176100628   0
    F4_I1all2       0.0012578616352201255   0.0006289308176100628   0
    F4_I1all1       0.0012578616352201255   0.0006289308176100628   0.0012578616352201255   0
                    F4_I2all1                F4_I2all2               F4_I1all2              F4_I1all1

La matrice peut être convertie en table HTML et déployée sur [IPFS](https://gist.github.com/YannBouyeron/53e6d67782dcff5995754b0a7333fa0b) avec la fonction matrix2ipfs:

    >>> matrix2ipfs(m)
    'QmcMhGpqsiCoyoPmbUf4xuX7ayMNiVHEkU44t4XMyWm2AK'

On obtient le hash du fichier HTML, consultable sur votre noeud ipfs ou via ipfs.io: https://ipfs.io/ipfs/<hash>:
	
	https://ipfs.io/ipfs/QmcMhGpqsiCoyoPmbUf4xuX7ayMNiVHEkU44t4XMyWm2AK

La matrice peut aussi être sauvegardée sous forme d'image png qui serra enregistrée localement:

    >>> help(matrix2png)
    Help on function matrix2png in module genopy:

    matrix2png(matrix, path='', scale=0.6, cmap='YlGnBu')
        Transforme une matrice de distance en image png
    
    arguments:
            matrix: pd.DataFrame ou distance matrice retournee par la fonction matrix
            path (otpionnel): path en .png de l'image
            scale (optionnel) [defaut=0.6] : taille du texte (légendes, titres, cellules)
            cmap (optionnel) [defaut="YlGnBu"] : palette de couleurs
            
    return: objet heatmap


    >>> matrix2png(m, path="mamatrice.png")
    <matplotlib.axes._subplots.AxesSubplot object at 0x704f0a50>


<p align="center">
  <img src="https://github.com/YannBouyeron/YannBouyeron.github.io/Images/raw/62FFEC5E-3F75-4173-9CF2-222939C40CF8.png
">
</p>


# Introduction à Pandas.

## Les Series.

##### On commence par importer les modules suivants:

	>>> import pandas as pd 
	>>> import numpy as np 	

##### On peut ensuite créer une série qui peut contenir des int float ou str :

	>>> s = pd.Series([2,4,6,8])
	
	>>> s
	0    2
	1    4
	2    6
	3    8
	dtype: int64
	

##### On peut éventuellement préciser certains arguments:

	>>> s = pd.Series([2,4,6,8], name="gogo", dtype="float", index=list("abcd"))
	
	>>> s
	a    2.0
	b    4.0
	c    6.0
	d    8.0
	Name: gogo, dtype: float64


##### Ou modifier / ajouter chacun de ces arguments plus tard..

	>>> s.name = "toto"
	
	>>> s.index = list("ABCD")
	
	>>> s
	A    2.0
	B    4.0
	C    6.0
	D    8.0
	Name: toto, dtype: float64


##### Pour changer le dtype on utilise la méthode `astype`:

	>>> s2 = s.astype(‘int64’) # ou s.astype(int) ou s.astype(float)...
	
	>>> s2
	0    2
	1    4
	2    6
	3    8
	Name: toto, dtype: int64

##### Il existe aussi d’autres manières de créer des séries:

A partir d’un dictionnaire {label : valeur} :

	>>> a = pd.Series({"a":2,"b":4,"c":6,"d":8})
	
	>>> a
	0    2
	1    4
	2    6
	3    8
	dtype: int64

A partir d’un Ndarray: 

	>>> b = pd.Series(np.arange(2,10,2))
	
	>>> b
	0    2
	1    4
	2    6
	3    8
	dtype: int32

##### Sélectionner un élément par son index:

	>>> s
	A    2.0
	B    4.0
	C    6.0
	D    8.0
	Name: toto, dtype: float64
	
	>>> s[0]
	2.0
	
	>>> s.iloc[0]
	2.0

##### Sélectionner un élément par son label (à condition qu’il en ait un):

	>>> s.A
	2.0
	
	>>> s.loc["A"]
	2.0	

##### Modifier un élément par son index ou par son label:

	>>> s
	A    2
	B    4
	C    6
	D    8
	Name: toto, dtype: int64
	
	>>> s.A = 45
	>>> s.B = 'gogo'
	>>> s.C = 6.9
	>>> s.iloc[3] = "bobo"
	
	>>> s
	A      45
	B    gogo
	C     6.9
	D    bobo
	Name: toto, dtype: object

##### Faire des opérations sur une série:

	>>> s
	A    2.0
	B    4.0
	C    6.0
	D    8.0
	Name: toto, dtype: float64
	
	>>> f = s*2
	
	>>> f
	A     4.0
	B     8.0
	C    12.0
	D    16.0
	Name: toto, dtype: float64

##### Assembler des séries:

	>> z = pd.Series(list("wxyz"))
	
	>>> z
	0    w
	1    x
	2    y
	3    z
	dtype: object
	
	>>> s
	A    2.0
	B    4.0
	C    6.0
	D    8.0
	Name: toto, dtype: float64
	
	>>> x = s.append(z, ignore_index=True)
	
	>>> x
	0    2
	1    4
	2    6
	3    8
	4    w
	5    x
	6    y
	7    z
	dtype: object

## Les DataFrame

### Créer un DataFrame:

Il existe de très nombreuses façons de créer un DataFrame... en voici 4

<a name="creatdfdico"></a>

##### A partir d’un dictionnaire de tuples:

	>>> d = {"nom":("Diatta", "Sane", "Diouf"), "prenom":("Robert", "Jean", "Albert")}
	
	>>> df = pd.DataFrame(d)
	
	>>> df
	      nom  prenom
	0  Diatta  Robert
	1    Sane    Jean
	2   Diouf  Albert

##### A partir d’un array:

	>>> n = np.array((("Diatta", "Robert"),("Sane", "Jean"),("Diouf", "Albert")))                                   
	
	>>> n
	array([['Diatta', 'Robert'],
	       ['Sane', 'Jean'],
	       ['Diouf', 'Albert']], dtype='<U6')
	
	>>> df = pd.DataFrame(n, columns=("nom","prenom"))
	
	>>> df
	      nom  prenom
	0  Diatta  Robert
	1    Sane    Jean
	2   Diouf  Albert

<a name="creatdfliste"></a>

##### A partir d’une liste de tuples (ou d’une liste de listes):

	>>> t = [('Diatta', 'Robert'), ('Sane', 'Jean'), ('Diouf', 'Albert')]
	
	>>> t
	[('Diatta', 'Robert'), ('Sane', 'Jean'), ('Diouf', 'Albert')]
	
	>>> df = pd.DataFrame(t, columns=("nom","prenom"))
	
	>>> df
	      nom  prenom
	0  Diatta  Robert
	1    Sane    Jean
	2   Diouf  Albert

##### A partir d’une liste de pd.Series:

	>>> a = pd.Series(("Diatta","Robert"))
	>>> b = pd.Series(("Sane","Jean"))
	>>> c = pd.Series(("Diouf","Albert"))
	
	>>> a
	0    Diatta
	1    Robert
	dtype: object
	
	>>> df = pd.DataFrame([a,b,c])
	
	>>> df
	        0       1
	0  Diatta  Robert
	1    Sane    Jean
	2   Diouf  Albert
	
	>>> df.columns = ("nom", "prenom")
	
	>>> df
	      nom  prenom
	0  Diatta  Robert
	1    Sane    Jean
	2   Diouf  Albert


Ou

	>>> n = pd.Series(["Diatta","Sane","Diouf"])
	>>> p = pd.Series(["Robert","Jean","Albert"])
	
	>>> n
	0    Diatta
	1      Sane
	2     Diouf
	dtype: object
	
	>>> p
	0    Robert
	1      Jean
	2    Albert
	dtype: object
	
	>>> df = pd.DataFrame([n,p])
	
	>>> df
	        0     1       2
	0  Diatta  Sane   Diouf
	1  Robert  Jean  Albert
	
	>>> df = df.T
	
	>>> df
	        0       1
	0  Diatta  Robert
	1    Sane    Jean
	2   Diouf  Albert
	
	>>> df.columns = ("Nom","Prenom")
	
	>>> df
	      Nom  Prenom
	0  Diatta  Robert
	1    Sane    Jean
	2   Diouf  Albert

### Sélectionner, trier, filtrer un DataFrame

	>>> df
	      nom  prenom              mail
	0  Diatta  Robert    rob@hotmail.fr
	1    Sane    Jean  jean@hotmail.com
	2   Diouf  Albert  bebert@gmail.com
	

<a name="headdf"></a>

##### Afficher les premières lignes d’un DataFrame. 
  
	>>> df.head()
	      nom  prenom              mail
	0  Diatta  Robert    rob@hotmail.fr
	1    Sane    Jean  jean@hotmail.com
	2   Diouf  Albert  bebert@gmail.com	

On ne voit pas la différence car mon DataFrame ne fait que trois lignes... mais c’est bien pratique quand on a un DataFrame de 3000 lignes. De plus il est possible de passer le nombre de lignes désiré en argument de head().

<a name="selcollabel"></a>

##### Seléctionner une colonne par son label... on récupère un pd.Series:

	>>> df
	      nom  prenom              mail
	0  Diatta  Robert    rob@hotmail.fr
	1    Sane    Jean  jean@hotmail.com
	2   Diouf  Albert  bebert@gmail.com
	
	
	>>> n = df.nom
	
	>>> type(n)
	<class 'pandas.core.series.Series'>
	
	>>> n
	0    Diatta
	1      Sane
	2     Diouf
	Name: nom, dtype: object
	
	
	>>> df["nom"]
	0    Diatta
	1      Sane
	2     Diouf
	Name: nom, dtype: object

<a name="selel"></a>

##### Sélectionner l’élément d’index 1 de la colonne "nom":

	>>> df
	      nom  prenom              mail
	0  Diatta  Robert    rob@hotmail.fr
	1    Sane    Jean  jean@hotmail.com
	2   Diouf  Albert  bebert@gmail.com
	
	
	>>> df.nom[1]
	'Sane'

<a name="selrawcol"></a>

##### Séléctionner des colonnes et des lignes  avec `loc` et  `iloc`: (on récupère un DataFrame)

###### La méthode `iloc` permet de sélectionner par les index:

Sélection de toutes les lignes de la colonne d’index 0 incluse jusqu’à la colonne d’index 1 exclue:

	>>> df
	      nom  prenom              mail
	0  Diatta  Robert    rob@hotmail.fr
	1    Sane    Jean  jean@hotmail.com
	2   Diouf  Albert  bebert@gmail.com
	
	
	>>> w = df.iloc[:, :1]
	
	>>> w
	      nom
	0  Diatta
	1    Sane
	2   Diouf
	
	>>> type(w)
	<class 'pandas.core.frame.DataFrame'>

Vous remarquerez que `iloc` retourne un DataFrame

Sélection de toutes les colonnes de la ligne d’index 1 incluse jusqu’à la ligne d’index 2 exclue:

	>>> df
	      nom  prenom              mail
	0  Diatta  Robert    rob@hotmail.fr
	1    Sane    Jean  jean@hotmail.com
	2   Diouf  Albert  bebert@gmail.com
	
	
	>>> df.iloc[1:2]
	    nom prenom              mail
	1  Sane   Jean  jean@hotmail.com

###### La méthode `loc` permet de sélectionner par les labels

Sélectionner des colonnes entières:

	>>> df
	      nom  prenom              mail
	0  Diatta  Robert    rob@hotmail.fr
	1    Sane    Jean  jean@hotmail.com
	2   Diouf  Albert  bebert@gmail.com
	
	
	>>> df.loc[:,["nom","mail"]]
	      nom              mail
	0  Diatta    rob@hotmail.fr
	1    Sane  jean@hotmail.com
	2   Diouf  bebert@gmail.com
	
	
	>>> df.loc[["nom","mail"]]
	      nom              mail
	0  Diatta    rob@hotmail.fr
	1    Sane  jean@hotmail.com
	2   Diouf  bebert@gmail.com
	

Sélectionner des lignes (n’ayant pas de labels): les index des lignes sont alors considérés comme des labels.
Les index initiaux et finaux sont alors inclus dans le retour.

	>>> df
	      nom  prenom              mail
	0  Diatta  Robert    rob@hotmail.fr
	1    Sane    Jean  jean@hotmail.com
	2   Diouf  Albert  bebert@gmail.com
	
	
	>>> df.loc[1:2]
	     nom  prenom              mail
	1   Sane    Jean  jean@hotmail.com
	2  Diouf  Albert  bebert@gmail.com

Ajoutons des labels de lignes:

	
	>>> df.index = list("abc")
	
	>>> df
	      nom  prenom              mail
	a  Diatta  Robert    rob@hotmail.fr
	b    Sane    Jean  jean@hotmail.com
	c   Diouf  Albert  bebert@gmail.com
	

Sélection de la ligne `b` incluse à `c` incluse:

	>>> df.loc["b":"c"]
	     nom  prenom              mail
	b   Sane    Jean  jean@hotmail.com
	c  Diouf  Albert  bebert@gmail.com

Sélection des colonnes `nom` et `mail` pour les lignes `b` incluse à `c` incluse:

	>>> df.loc["b":"c",["nom","mail"]]
	     nom              mail
	b   Sane  jean@hotmail.com
	c  Diouf  bebert@gmail.com

Sélectionner les lignes `a` et `c` des colonnes `nom` et `mail`

	>>> df.loc[[0,2],["nom","mail"]]
	      nom                mail
	a  Diatta   robert@hotmail.fr
	c   Diouf  bebert@hotmail.com

On peut toujours sélectionner par les index avec `iloc` si on le souhaite:

	>>> df.iloc[1:2]
	    nom prenom              mail
	b  Sane   Jean  jean@hotmail.com
	
	>>> df.iloc[1:3]
	     nom  prenom              mail
	b   Sane    Jean  jean@hotmail.com
	c  Diouf  Albert  bebert@gmail.com


### Modifier un DataFrame

##### Transposer

	>>> df
	      nom  prenom
	0  Diatta  Robert
	1    Sane    Jean
	2   Diouf  Albert
	
	>>> df.T
	             0     1       2
	nom     Diatta  Sane   Diouf
	prenom  Robert  Jean  Albert

<a name="addlabel"></a>

##### Changer (ou ajouter) des noms de colonnes et de labels:

	>>> df
	      nom  prenom
	0  Diatta  Robert
	1    Sane    Jean
	2   Diouf  Albert
	
	>>> df.columns
	Index(['nom', 'prenom'], dtype='object')
	
	>>> df.columns = ("colA","colB")
	
	>>> df
	     colA    colB
	0  Diatta  Robert
	1    Sane    Jean
	2   Diouf  Albert
	
	>>> df.index
	RangeIndex(start=0, stop=3, step=1)
	
	>>> df.index = list("abc")
	
	>>> df
	     colA    colB
	a  Diatta  Robert
	b    Sane    Jean
	c   Diouf  Albert

<a name="addcol"></a>

##### Ajouter une colonne à un DataFrame:

	>>> df
	     colA    colB
	a  Diatta  Robert
	b    Sane    Jean
	c   Diouf  Albert
	
	>>> df["colC"] = (34,21,45)
	
	>>> df
	     colA    colB  colC
	a  Diatta  Robert    34
	b    Sane    Jean    21
	c   Diouf  Albert    45

##### Concatener des DataFrame ... pour ajouter une (ou plusieurs) colonne.

	>>> df
	      nom  prenom
	0  Diatta  Robert
	1    Sane    Jean
	2   Diouf  Albert
	
	>>> m
	                 mail
	0   robert@hotmail.fr
	1      jean@gmail.com
	2  bebert@hotmail.com
	
	>>> pd.concat([df,m],axis=1)
	      nom  prenom                mail
	0  Diatta  Robert   robert@hotmail.fr
	1    Sane    Jean      jean@gmail.com
	2   Diouf  Albert  bebert@hotmail.com

<a name="addraw"></a>

##### Concatener des DataFrame ... pour ajouter une (ou plusieurs) ligne.

	>>> raw = pd.DataFrame([("Dupond","Serge")], columns=("colA","colB"))
	
	>>> raw
	     colA   colB
	0  Dupond  Serge
	
	>>> df
	     colA    colB
	a  Diatta  Robert
	b    Sane    Jean
	c   Diouf  Albert
	
	>>> df2 = df.append(raw)
	
	>>> df2
	     colA    colB
	a  Diatta  Robert
	b    Sane    Jean
	c   Diouf  Albert
	0  Dupond   Serge
	
	>>> df3 = df.append(raw, ignore_index=True)
	
	>>> df3
	     colA    colB
	0  Diatta  Robert
	1    Sane    Jean
	2   Diouf  Albert
	3  Dupond   Serge

Il existe de très nombreuses autres méthodes pour concatener des DataFrame... [Doc officielle](http://pandas.pydata.org/pandas-docs/stable/merging.html)

<a name="delcol"></a>

##### Supprimer une ou plusieurs colonnes:

	>>> df
	     colA    colB  colC
	a  Diatta  Robert    34
	b    Sane    Jean    21
	c   Diouf  Albert    45
	
	>>> df2 = df.drop(["colC"], axis=1)
	>>> df2
	     colA    colB
	a  Diatta  Robert
	b    Sane    Jean
	c   Diouf  Albert
	
	
	
	>>> df
	     colA    colB  colC
	a  Diatta  Robert    34
	b    Sane    Jean    21
	c   Diouf  Albert    45
	
	>>> df3 = df.drop(columns=["colC"])
	>>> df3
	     colA    colB
	a  Diatta  Robert
	b    Sane    Jean
	c   Diouf  Albert

<a name="delraw"></a>

##### Supprimer une ou plusieurs lignes:

	>>> df
	     colA    colB  colC
	a  Diatta  Robert    34
	b    Sane    Jean    21
	c   Diouf  Albert    45
	
	>>> df2 = df.drop(["a"])
	
	>>> df2
	    colA    colB  colC
	b   Sane    Jean    21
	c  Diouf  Albert    45

## Utiliser une base de données SQLite avec Pandas

##### Importer les modules pandas et sqlite3:

	>>> import pandas as pd
	>>> from sqlite3 import *

<a name="importsql"></a>

##### Importer une base SQL existante:

	>>> import pandas as pd
	>>> from sqlite3 import *
	
	>>> conn = connect("base.db")
	

On peut aussi se connecter de la même façon à une base SQL en plaçant son URL en argument de connect.

	>>> conn = connect("https://domaine/base.db")

On peut éventuellement commencer par récupérer les noms des tables:

	>>> liste_tables = pd.read_sql_query("select name from sqlite_master where type = 'table'", conn)
	
	>>> liste_tables
        name
	0  users


Ma base de données contient ici une seule table nommée users.

Puis envoyer une requête SQL pour récupérer le contenu d’une table

	>>> users = pd.read_sql_query("select * from users", conn)
	
	>>> users
   	      nom                mail  level
	0    Admi      admi@gmail.com      2
	1  Diatta  robert@hotmail.com      1
	2    Sane     jean@hotmail.fr      1





<a name="creatsql"></a>

##### Créer une base SQL


Commencez par importer les modules et créer un objet `conn`:

	>>> import pandas as pd
	>>> from sqlite3 import *
	
	>>> conn = connect("base.db")
	

Vous pouvez créer un DataFrame vide ou contenant déjà des lignes

	>>> df = pd.DataFrame({"nom":("Admi", "Diatta", "Sane"), "mail":("admi@gmail.com", "robert@hotmail.com", "jean@hotmail.fr"), "level":(2,1,1)})
	
	>>> df
          nom                mail  level
	0    Admi      admi@gmail.com      2
	1  Diatta  robert@hotmail.com      1
	2    Sane     jean@hotmail.fr      1


Convertir le DataFrame en table sql:

	>>> df.to_sql("users", conn, index=False)



<a name="setsql"></a>

##### Modifier la base sql:

En utilisant une commande sql:

	>>> cur = conn.cursor()
	
	>>> cur.execute("insert into users(nom, mail, level) values('Diouf', 'dio@yahoo.com', 1)") 
	<sqlite3.Cursor object at 0x73590d60>
	
	>>> users = pd.read_sql_query("select * from users", conn)
	
	>>> users
	      nom                mail  level
	0    Admi      admi@gmail.com      2
	1  Diatta  robert@hotmail.com      1
	2    Sane     jean@hotmail.fr      1
	3   Diouf       dio@yahoo.com      1

En modifiant le DataFrame et en remplaçant l’ancienne table par le nouveau DataFrame:

	>>> users = pd.read_sql_query("select * from users", conn)
	
	>>> users
              nom                mail  level
	0    Admi      admi@gmail.com      2
	1  Diatta  robert@hotmail.com      1
	2    Sane     jean@hotmail.fr      1
	
	>>> raw = pd.DataFrame({"nom":("Samb",), "mail":("samba@gmail.com",), "level":(3,)})
	
	>>> users = users.append(raw, ignore_index=True)
	
	>>> users
	      nom                mail  level
	0    Admi      admi@gmail.com      2
	1  Diatta  robert@hotmail.com      1
	2    Sane     jean@hotmail.fr      1
	3    Samb     samba@gmail.com      3

	>>> users.to_sql("users", conn, index=False, if_exists="replace")


## Utiliser des bases de données au format CSV avec Pandas.

<a name="creatcsv"></a>

##### Créer un DataFrame:

	>>> df = pd.DataFrame({"nom":("Admi", "Diatta", "Sane"), "mail":("admi@gmail.com", "robert@hotmail.com", "jean@hotmail.fr"), "level":(2,1,1)})
	
	>>> df
	      nom                mail  level
	0    Admi      admi@gmail.com      2
	1  Diatta  robert@hotmail.com      1
	2    Sane     jean@hotmail.fr      1 
	

##### Le convertir en CSV:

	>>> df.to_csv("mycsv", index=False)
	


<a name="importcsv"></a>

##### Convertir un CSV en DataFrame:

	>>> users = pd.read_csv("mycsv")
	
	>>> users
	      nom                mail  level
	0    Admi      admi@gmail.com      2
	1  Diatta  robert@hotmail.com      1
	2    Sane     jean@hotmail.fr      1


On peut aussi passer l'URL du CSV en argument à la place de son path


<a name="setcsv"></a>

##### Modifier le CSV:

	>>> users = pd.read_csv("mycsv")
	
	>>> raw = pd.DataFrame({"nom":("Samb",), "mail":("samba@gmail.com",), "level":(3,)})
	
	>>> users = users.append(raw, ignore_index=True)
	
	>>> users
	      nom                mail  level
	0    Admi      admi@gmail.com      2
	1  Diatta  robert@hotmail.com      1
	2    Sane     jean@hotmail.fr      1
	3    Samb     samba@gmail.com      3
	
	>>> users.to_csv("mycsv", index=False)
	
	>>> users2 = pd.read_csv("mycsv")
	
	>>> users2
	      nom                mail  level
	0    Admi      admi@gmail.com      2
	1  Diatta  robert@hotmail.com      1
	2    Sane     jean@hotmail.fr      1
	3    Samb     samba@gmail.com      3

## Utiliser des fichiers xlsx:

<a name="creatxlsx"></a>
<a name="setxlsx"></a>

##### Convertir un DataFrame en un fichier xlsx, puis l’inverse:

	>>> df
	      nom                mail  level
	0    Admi      admi@gmail.com      2
	1  Diatta  robert@hotmail.com      1
	2    Sane     jean@hotmail.fr      1
	
	>>> df.to_excel("mybase.xlsx", sheet_name = "Modou")
	
	>>> users = pd.read_excel("mybase.xlsx")
	
	>>> users
	      nom                mail  level
	0    Admi      admi@gmail.com      2
	1  Diatta  robert@hotmail.com      1
	2    Sane     jean@hotmail.fr      1

##### Créer un xlsx avec plusieurs feuilles:

	>>> df1 = pd.DataFrame({"nom":("Admi", "Diatta", "Sane"), "mail":("admi@gmail.com", "robert@hotmail.com", "jean@hotmail.fr"), "level":(2,1,1)})
	
	>>> df2 = pd.DataFrame({"nom":("Diatta", "Sane", "Diouf"), "prenom":("Robert", "Jean", "Albert")})
	   
    >>> writer = pd.ExcelWriter('gogo.xlsx')
    
    >>> df1.to_excel(writer,'feuille 1')
    
    >>> df2.to_excel(writer,'feuille 2')
    
    >>> writer.save()

<a name="importxlsx"></a>

##### Récupérer une ou plusieurs feuilles d’un xlsx:

Récupérer la feuille 1: feuille d’index 0 retournée par défaut:

	>>> table1 = pd.read_excel("gogo.xlsx")
	
	>>> table1
	      nom                mail  level
	0    Admi      admi@gmail.com      2
	1  Diatta  robert@hotmail.com      1
	2    Sane     jean@hotmail.fr      1


Récupérer la feuille 2 (feuille d’index 1):

	>>> table2 = pd.read_excel("gogo.xlsx", sheet_name = 1)
	
	>>> table2
	      nom  prenom
	0  Diatta  Robert
	1    Sane    Jean
	2   Diouf  Albert
	
	>>> table2 = pd.read_excel("gogo.xlsx", sheet_name = "feuille 2")
	
	>>> table2
	      nom  prenom
	0  Diatta  Robert
	1    Sane    Jean
	2   Diouf  Albert
	

Récupérer les feuilles 0 et 1 (on obtient un dictionnaire de feuilles):

	>>> tables = pd.read_excel("gogo.xlsx", sheet_name = [0,1])
	
	>>> tables
	OrderedDict([(0,       nom                mail  level
	0    Admi      admi@gmail.com      2
	1  Diatta  robert@hotmail.com      1
	2    Sane     jean@hotmail.fr      1), (1,       nom  prenom
	0  Diatta  Robert
	1    Sane    Jean
	2   Diouf  Albert)])

Récupérer toutes les feuilles (on obtient un dicitionnaire de feuilles):

	>>> tables = pd.read_excel("gogo.xlsx", sheet_name = None)
	
	>>> tables
	OrderedDict([('feuille 1',       nom                mail  level
	0    Admi      admi@gmail.com      2
	1  Diatta  robert@hotmail.com      1
	2    Sane     jean@hotmail.fr      1), ('feuille 2',       nom  prenom
	0  Diatta  Robert
	1    Sane    Jean
	2   Diouf  Albert)])
	
	>>> tables.keys()
	odict_keys(['feuille 1', 'feuille 2'])
	
	>>> tables["feuille 1"]
	      nom                mail  level
	0    Admi      admi@gmail.com      2
	1  Diatta  robert@hotmail.com      1
	2    Sane     jean@hotmail.fr      1
	
	>>> tables["feuille 2"]
	      nom  prenom
	0  Diatta  Robert
	1    Sane    Jean
	2   Diouf  Albert

## Convertir un DataFrame en Json :

	>>> df 
	      nom                mail  level
	0    Admi      admi@gmail.com      2
	1  Diatta  robert@hotmail.com      1
	2    Sane     jean@hotmail.fr      1
	
	>>> df.to_json()
	'{"nom":{"0":"Admi","1":"Diatta","2":"Sane"},"mail":{"0":"admi@gmail.com","1":"robert@hotmail.com","2":"jean@hotmail.fr"},"level":{"0":2,"1":1,"2":1}}'
	
	>>> df.to_json("myjson.js") # le json est enregistré dans le fichier myjson.js
	

## Convertir un Dataframe en html :

	>>> pd.set_option('display.max_colwidth', -1) # c'est pour ne pas couper les phrases trops longues 
	
	>>> html = df.to_html()

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

<a name="savegraph"></a>

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

<a name="multigraph"></a>

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

<a name="subplot"></a>

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


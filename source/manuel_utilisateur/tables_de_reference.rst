.. _tables_de_reference:

#######################
Les tables de référence
#######################


Une table de référence (ou de codification) permet de limiter volontairement
les valeurs possibles pour une information saisie. Cela évite que cette valeur
ne soit décrite de deux manières différentes. Dans cet applicatif, les tables
de référence sont composées d'un identifiant, d'un libellé et de dates de
validité.


La date de validité permet de contrôler les éléments qui apparaissent dans les
listes à choix des formulaires. Si la date de fin de validité est dépassée alors
cet élément n'est plus sélectionnable comme référence cependant il reste
sélectionné là où il l'a déjà été.


Nous allons décrire dans ce paragraphe comment paramétrer les tables de
référence qui sont utilisés dans les formulaires de l'applicatif :

* :ref:`entreprise`,
* :ref:`titre_de_civilite`,
* :ref:`sepulture_type`,
* :ref:`travaux_nature`,
* :ref:`zone_type`,
* :ref:`voie_type`.


Le paramétrage de ces éléments se fait dans le menu
(:menuselection:`Paramétrage --> Divers`).


.. image:: opencimetiere--menu-parametrage-divers.png


.. _entreprise:

L'entreprise
============

Cet élément est accessible via 
(:menuselection:`Paramétrage --> Divers --> Entreprise`).

Une entreprise dans cet applicatif correspond à une entreprise habilité à venir
effectuer des travaux à l'intérieur du cimetière. Elles sont identifiées par
leur nom.

Les informations à saisir sont :

- le nom de l'entreprise (obligatoire)
- s'il s'agit d'une entreprise de pompe funèbre
- l'adresse (sur deux lignes)
- le code postal
- la ville
- le téléphone



Cette table est référencée par le(s) élément(s) suivant(s) :

* :ref:`travaux`.


.. _titre_de_civilite:

Le titre de civilité
====================

Cet élément est accessible via 
(:menuselection:`Paramétrage --> Divers --> Titre de civilité`).

Le titre de civilité est le plus fréquemment utilisé pour identifier la civilité
d'une personne (Monsieur, Madame ou Mademoiselle). Il est également utilisé
pour le titre ou le rang d'une personne.

Cette table est référencée par le(s) élément(s) suivant(s) :

* :ref:`defunt`,
* :ref:`autorisation`.


.. _sepulture_type:

Le type de sépulture
====================

Cet élément est accessible via 
(:menuselection:`Paramétrage --> Divers --> Type de sépulture`).

Le type de sépulture est utilisé pour décrire une concession. Exemples :
'Fosse maçonnée haute', 'Cavurne', 'Pierre tombale', 'Caveau T2 haut',
'Caveau T2 bas', ...

Cette table est référencée par le(s) élément(s) suivant(s) :

* :ref:`concession`.


.. _travaux_nature:

La nature des travaux
=====================

Cet élément est accessible via 
(:menuselection:`Paramétrage --> Divers --> Nature des travaux`).

La nature des travaux est utilisée pour décrire les travaux sur un emplacement.
Exemples : 'Enlèvement porte', 'Démolition-Reconstruction à l'identique',
'Creusement', 'Surélévation', ...

Cette table est référencée par le(s) élément(s) suivant(s) :

* :ref:`travaux`.


.. _zone_type:

Le type de zone
===============

Cet élément est accessible via 
(:menuselection:`Paramétrage --> Divers --> Type de zone`).

Le type de zone est utilisé pour catégoriser une zone dans le système de
localisation. Exemples : 'Carré', 'Extension', 'Section', ... Un cimetière
peut être composé de plusieurs sections ou de plusieurs carrés.

Cette table est référencée par le(s) élément(s) suivant(s) :

* :ref:`zone`.


.. _voie_type:

Le type de voie
===============

Cet élément est accessible via 
(:menuselection:`Paramétrage --> Divers --> Type de voie`).

Le type de voie est utilisé pour catégoriser une voie dans le système de
localisation. Exemples : 'Allée', 'Place', 'Rangée', ... Une zone peut être
composé de plusieurs allées ou de plusieurs rangées.

Cette table est référencée par le(s) élément(s) suivant(s) :

* :ref:`voie`.


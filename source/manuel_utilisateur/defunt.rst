.. _defunt:

###########
Les défunts
###########

Il est proposé de décrire dans ce paragraphe de décrire la saisie des défunts
dans l'onglet "défunt" d'un emplacement.


.. image:: ../_static/tab_defunt.png

Saisir un défunt
----------------

Il est possible de créer ou modifier un défunt dans le formulaire ci dessous :

.. image:: ../_static/form_defunt.png


Les informations à saisir sont :

- le titre (:ref:`titre_de_civilite`)
- le nom du défunt (obligatoire)
- le prénon
- le nom d'usage
- la date de naissance
- la date de décés
- le lieu du décès
- la date d'inhumation
- les opérations funéraires : exhumation, inhumation


Calcul de l'occupation
----------------------

Le calcul de la taille d'occupation se fait à partir des paramères suivants :

- taille_cercueil : valeur par défaut 1 (:ref:`taille_cercueil`)
- taille_urne : valeur par défaut 0,1 (:ref:`taille_urne`)
- taille_reduction : valeur par défaut 0,5 (:ref:`taille_reduction`)
- temps_reduction : valeur par défaut 5 (:ref:`temps_reduction`)
    
C'est sur cette base que se fait le calcul de la taille et le calcul de place
dans l'emplacement.


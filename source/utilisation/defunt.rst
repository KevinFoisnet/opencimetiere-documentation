.. _defunt:

################
Saisir un defunt
################



Il est proposé de décrire dans ce paragraphe de decrire la saisie des défunts
dans l'onglet "defunt" de l'emplacement.


.. image:: ../_static/tab_defunt.png


Il est possible de creer ou modifier un defunt dans le formulaire ci dessous


.. image:: ../_static/form_defunt.png

Il est saisie :

- le nom du defunt (obligatoire)

- le prénon

- le nom marital

- les dates décès, inhumation, naissance

- le lieu du décès

- les opérations funéraires : exhumation, inhumation


Le calcul de la taille d'occupation est paramétré dans
dyn/var.inc ::

    $taille_cercueil = 1
    $taille_urne = 0,1
    $taille_reduction = 0,5
    
C'est sur cette base que se fait le calcul de la taille et la
calcul de place dans emplecement.
(méthode calcultaille de obj/defunt.class.php)




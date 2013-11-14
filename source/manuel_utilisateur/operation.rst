.. _operation:

#########
Opération
#########

Nous vous proposons dans ce chapitre d'utiliser les opérations.


Les opérations ont été implémentées par la version 2.02
d'openCimetière à l'initiative de la ville d'Albi.

Ce module est facultatif et les opérations funéraires peuvent être
saisies dans les emplacements directement (surtout lorsqu on est en phase
d'initialisation du projet et de saisie en masse).

Elles concernent :

- l'inhumation

- la réduction d'un ou plusieurs défunts

- le transfert d'un ou plusieurs défunt d'un emplacement à un autre

Les transferts ont intégré ce module avec la version 3.0.0.

Les opérations peuvent avoir 2 états :

- actif

- trt (opération traitée)



Lorsqu'elle concerne un défunt d'un emplacement, il est alors impossible
de modifier un défunt lorsqu'une opération est dans l'état actif.

Pour traiter une opération ou la valider, il faut appuyer sur
le bouton "v" de l'opération considérée.

Il est alors lancé le traitement de validation (app/valid_operation.php)
Les tables défunt, emplacement sont alors mises à jour et l'accès au defunt
via l'onglet de l'emplacement est permis

ATTENTION, CE TRAITEMENT EST DEFINITIF et on ne peut pas retourner en arrière.

Les opérations "traitées" sont visualisables dans l'onglet "opération-trt" de
l'emplacement. En appuyant sur l'icone pdf, on accéde à la liste des courriers automatiques
a générer pour l'opération (si elles sont actives).


.. toctree::

    inhumation.rst
    reduction.rst
    transfert.rst
    calcul_place_occupee.rst
    numdossier.rst

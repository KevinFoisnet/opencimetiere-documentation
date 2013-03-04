.. _voie:

###############
Saisir une voie
###############



Il est proposé de décrire dans ce paragraphe de decrire la saisie
d'une voie dans l'option paramétrage du menu ou dans l'onglet zone


Les voies sont listées dans l'option voie du menu paramétrage

.. image:: ../_static/tab_voie.png

Il est possible de géolocaliser la  ligne d'une voie :

.. image:: ../_static/sig_voie.png

Il est possible de creer ou modifier une voie dans le formulaire ci dessous

.. image:: ../_static/form_voie.png


Il est saisie :

- le libelle de la voie

- la zone de la voie

- le type de la voie


Le type de la voie peut être modifié dans dyn/var.inc ::

    $select_voie=array('ALLEE',
                        'ILOT',
                        'PLACE',
                        'PASSAGE',
                        'RANGEE',
                        'DIVISION');

.. _zone:

###############
Saisir une zone
###############

Il est proposé de décrire dans ce paragraphe de decrire la saisie
des zones dans le menu option parametrage ou l'onglet cimetiere


Les zones sont listés dans le menu "paramétrage": 

.. image:: ../_static/tab_zone.png

Il est possible de géolocaliser le périmètre d'une zone :

.. image:: ../_static/sig_zone.png

Il est possible de creer ou modifier une zone dans le formulaire ci dessous

.. image:: ../_static/form_zone.png


Il est saisie :

- le nom de la zone

- le type de la zone

- le cimetiere ou est la zone


Le type de la zone peut être modifié dans dyn/var.inc ::

    $select_zone=array('CARRE',
                    'COLLINE',
                    'ENCLOS',
                    'EXTENSION',
                    'SECTION');




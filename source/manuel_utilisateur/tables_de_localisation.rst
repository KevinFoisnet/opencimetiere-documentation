.. _tables_de_localisation:

##########################
Les tables de localisation
##########################


La localisation permet de donner une adresse précise à un emplacement. Cette
localisation est divisée en plusieurs niveaux. D'abord le cimetière qui peut 
contenir plusieurs zones. Puis chaque zone peut contenir plusieurs voies.
Enfin dans une voie l'emplacement est identifié par un numéro.


Nous allons décrire dans ce paragraphe comment paramétrer les tables qui
composent la localisation d'un emplacement :

* :ref:`cimetiere`,
* :ref:`zone`,
* :ref:`voie`.


Le paramétrage de ces éléments se fait dans le menu
(:menuselection:`Paramétrage --> Localisation`).


.. image:: opencimetiere--menu-parametrage-localisation.png


.. _cimetiere:

Le cimetière
============

Cet élément est accessible via 
(:menuselection:`Paramétrage --> Localisation --> Cimetière`). 

.. image:: opencimetiere--tableau-cimetiere.png


.. _saisir_cimetiere:

Saisir un cimetière
-------------------

Le formulaire est identique en mode ajout et modification.

.. image:: ../_static/form_cimetiere.png


Les informations à saisir sont :

- le libellé
- l'adresse (sur deux lignes)
- le code postal
- la ville
- des observations

.. tip::

    Il est possible de saisir une zone depuis l'onglet zone du formulaire d'un
    cimetière. Cela permet d'éviter d'avoir à sélectionner le cimetière concerné
    à chaque ajout de zone.

Localiser un cimetière (option SIG interne)
-------------------------------------------

|icone-localiser|

Cette action n'est disponible que si le paramètre "option_localisation"
(:ref:`paramétrage général <option_localisation>`) est positionné sur
"sig_interne".

Il est possible de géolocaliser le périmètre du cimetière :

.. image:: ../_static/sig_cimetiere.png


.. _zone:

La zone
=======

Cet élément est accessible via 
(:menuselection:`Paramétrage --> Localisation --> Zone`).


.. image:: opencimetiere--tableau-zone.png


Saisir une zone
---------------

Il est possible de creer ou modifier une zone dans le formulaire ci dessous

.. image:: ../_static/form_zone.png


Les informations à saisir sont :

- le cimetière dans lequel se trouve la zone
- le type de zone (:ref:`zone_type`)
- le libellé de la zone

.. tip::

    Il est possible de saisir une voie depuis l'onglet voie du formulaire d'une
    zone. Cela permet d'éviter d'avoir à sélectionner la zone concernée à chaque
    ajout de voie.

.. tip::

    Il est possible de saisir une zone depuis l'onglet zone du formulaire d'un
    cimetière. Cela permet d'éviter d'avoir à sélectionner le cimetière concerné
    à chaque ajout de zone.


Localiser une zone (option SIG interne)
---------------------------------------

|icone-localiser|

Cette action n'est disponible que si le paramètre "option_localisation"
(:ref:`paramétrage général <option_localisation>`) est positionné sur
"sig_interne".

Il est possible de géolocaliser le périmètre d'une zone :

.. image:: ../_static/sig_zone.png


.. _voie:

La voie
=======

Cet élément est accessible via 
(:menuselection:`Paramétrage --> Localisation --> Voie`).

.. image:: opencimetiere--tableau-voie.png



Imprimer un état de la voie
---------------------------

|icone-edition-pdfetat-voie|

.. |icone-edition-pdfetat-voie| image:: opencimetiere--icone-edition-pdfetat-voie.png


Imprimer un état de la voie par concession
------------------------------------------

|icone-edition-pdfetat-voieconcession|

.. |icone-edition-pdfetat-voieconcession| image:: opencimetiere--icone-edition-pdfetat-voieconcession.png



Saisir une voie
---------------

Il est possible de creer ou modifier une voie dans le formulaire ci dessous

.. image:: ../_static/form_voie.png


Les informations à saisir sont :

- le zone dans laquelle se trouve la voie
- le type de voie (:ref:`voie_type`)
- le libellé de la voie


.. tip::

    Il est possible de saisir une voie depuis l'onglet voie du formulaire d'une
    zone. Cela permet d'éviter d'avoir à sélectionner la zone concernée à chaque
    ajout de voie.


Localiser une voie (option SIG interne)
---------------------------------------

|icone-localiser|

Cette action n'est disponible que si le paramètre "option_localisation"
(:ref:`paramétrage général <option_localisation>`) est positionné sur
"sig_interne".

Il est possible de géolocaliser la ligne d'une voie :

.. image:: ../_static/sig_voie.png


.. |icone-localiser| image:: opencimetiere--icone-localiser.png



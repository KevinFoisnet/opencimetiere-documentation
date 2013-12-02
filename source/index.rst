.. opencimetiere documentation master file.

===============================
openCimetière 3.0 documentation
===============================

.. note::

    Cette création est mise à disposition selon le Contrat Paternité-Partage des
    Conditions Initiales à l'Identique 2.0 France disponible en ligne
    http://creativecommons.org/licenses/by-sa/2.0/fr/ ou par courrier postal à
    Creative Commons, 171 Second Street, Suite 300, San Francisco,
    California 94105, USA.


Créé dans un groupe de l'ADULLACT en 2005, openCimetière se place dans un
contexte de gestion difficile, dans ce secteur d'activité considéré comme peu
stratégique par les décideurs et pourtant combien important pour le service
public de proximité. Logiciel libre opérationnel depuis des années,
openCimetière a été en septembre 2006 élu "projet du mois" sur la forge. La
version 3.x a pour objectif de porter l'application dans un environnement plus
convivial (openMairie 4.x) avec de nouveaux outils  qui viennent
compléter les outils déjà existants comme le requêteur, les courriers type ainsi
que les états et sous-états. 

La version 3.0.0 utilise openMairie 4.4.0 avec :

* l'ergonomie jquery
* les tableaux de bord individualisable avec widget
* l'information géographique en interne avec openLayers
* le générateur openMairie

Cette version ne fonctionne qu'avec postgresql complété par postgis (si l'option SIG_interne est activée)

openCimetière reste un outil souple et adaptable à toute collectivité quelle que soit sa taille.
Les principales fonctions de l'application sont les suivantes :

* la gestion de la place (défunt) dans les concessions,
* la gestion des autorisations : concessionnaire et ayant droit,
* la gestion du terme de la concession : transfert de défunt, transfert à
  l'ossuaire,
* la gestion des concessions libres,
* la gestion des opérations funéraires,
* l'archivage systématique de l'ensemble des données pour constituer une mémoire
  commune.

Ce document a pour but de guider les utilisateurs et les développeurs dans la
prise en main du projet.

Bonne lecture et n'hésitez pas à nous faire part de vos remarques à l'adresse
suivante : contact@openmairie.org !


Manuel de l'utilisateur
=======================

.. toctree::

   manuel_utilisateur/index.rst


Guide du développeur
====================

.. toctree::

   guide_developpeur/index.rst


Bibliographie
=============

* http://www.openmairie.org/telechargement/openMairie-Guidedudveloppeur.pdf/view


Contributeurs
=============

(par ordre alphabétique)

* `atReal <http://www.atreal.fr>`_
* Florent Michon
* François Raynaud


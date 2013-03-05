.. _emplacement:

################
Les emplacements
################

Les emplacements sont listés dans le formulaire suivant

.. image:: ../_static/tab_emplacement.png

Il est possible de creer ou modifier ou supprimer un emplacement dans le formulaire ci dessous

.. image:: ../_static/form_emplacement.png

Il faut saisir le lieu :

- numero dans la voie

- voie

et la famille.

.. admonition:: XXX

    Le paramètrage suivant du formulaire se fait dans dyn/var.inc ::

        // duree par defaut des terrains communaux
        $duree_defaut_terraincommunal=5;
        $superficie_defaut_terraincommunal=2;
    
        /**
         * Types de concessions
         * $option_typeconcession => 1 signifie que cette option sera activée
         * $select_typeconcession => 
         /
        
        $select_typeconcession = array ("", "Familiale", "Individuelle", "Collective");
        
        /**
         * Renouvellement de concessions
         * $option_renouvellementconcession => 1 signifie que cette option sera activée
         /
    
        $option_renouvellementconcession = 1;

        // il est possible de paramétrer 5 zones supplémentaires ::
        // zones parametrables : concession
        
        $temp1_type = "hidden";// text ou hidden
        $temp1_lib= "zone 1";  // libelle sur le formulaire
        $temp1_taille=10;      // attention la longueur maxi du champs est de 100 varchar
        $temp1_max=10;         // attention la longueur maxi du champs est de 100 varchar
        
        $temp2_type = "hidden";
        $temp2_lib= "zone 2";
        $temp2_taille=20;
        $temp2_max=20; 
        
        $temp3_type = "hidden";
        $temp3_lib= "zone 3";
        $temp3_taille=30;
        $temp3_max=30; 
        
        $temp4_type = "hidden";
        $temp4_lib= "zone 4";
        $temp4_taille=10;
        $temp4_max=10;
        
        $temp5_type = "hidden";
        $temp5_lib= "zone 5";
        $temp5_taille=10;
        $temp5_max=10; 






.. _concession:

La concession
=============

Place dans un cimetière. http://fr.wiktionary.org/wiki/concession


.. _colombarium:

Le colombarium
==============

=> columbarium

Édifice destiné à recevoir des urnes mortuaires dans les cimetières où l’on
pratique l’incinération. http://fr.wiktionary.org/wiki/columbarium


.. _enfeu:

L'enfeu
=======

Niche dans un édifice religieux abritant un tombeau, un sarcophage ou une scène
funéraire. http://fr.wiktionary.org/wiki/enfeu



.. _terraincommunal:

Le terrain communal
===================

=> terrain commun

...


.. _ossuaire:

L'ossuaire
==========

Endroit couvert où l’on met des ossements humains.
http://fr.wiktionary.org/wiki/ossuaire


.. _depositoire:

Le dépositoire
==============

Nom donné, dans quelques localités, au lieu où l’on dépose les corps des morts,
avant de les enterrer, et jusqu’à ce que la décomposition putride commence à se
manifester. http://fr.wiktionary.org/wiki/d%C3%A9positoire





################################
La localisation de l'emplacement
################################

Option Plan
===========

A compléter...


Option SIG
==========

SIG interne
-----------

Il est possible de géolocaliser l'emplacement :

.. image:: ../_static/sig_emplacement.png


SIG externe
-----------

A compléter...


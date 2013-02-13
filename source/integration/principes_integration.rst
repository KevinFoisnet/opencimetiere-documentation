.. _principes_integration:

#########################################
Les principes d'une application composite
#########################################

openCimetière permet de construire une application composite en intégrant 
des contenus venant d'applications externes.

C'est ainsi que les emplacements peuvent s' afficher sur des fonds de carte internet.

Suivant wikipedia : "Une application composite (ou mashup ou encore mash-up) est une application
qui combine du contenu ou du service provenant de plusieurs applications plus ou moins hétérogènes."

http://fr.wikipedia.org/wiki/Application_composite

Les applications composites permettent de construire une application rapidement
a un faible coût grace à la fusion de multiples services internet. Les composants
sont facilement ré utilisables

openCimetière respecte les formats interopérables définies pour les bases de données
par l'OGC.

"L'Open Geospatial Consortium, ou OGC, est un consortium international pour développer
et promouvoir des standards ouverts, les spécifications OpenGIS®, afin de garantir
l'interopérabilité des contenus, des services et des échanges dans les domaines de
la géomatique et de l'information géographique".

http://fr.wikipedia.org/wiki/Open_Geospatial_Consortium

C'est ainsi que les données peuvent être consultés par tous les outils acceptant les
formats postgis, wms, wfs, kml, gml, json ... et notament QGIS (outil client lourd).


Il est décrit ici les principes d'integration d'openCimetière dans le domaine
de l'information géographique.

- la géolocalisation de l'emplacement

- l'utilisation de vues pour se connecter sur des bases externes

- la mise en place de lien sur un sig externe

Il est decrit ensuite l'intégration au travers de tableau de bord personnalisé.

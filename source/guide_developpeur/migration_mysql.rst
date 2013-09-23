.. _migration_mysql:


###############
Migration mysql
###############


Nous proposons dans ce châpitre de vous exposer les requêtes de migration utilisées par la ville d'Arles
pour passer de la version 2.10 mysql à la version 3.0.0. La migration a duré une journée.


La base postgresql se différencie avec celle de mysql (qui était avec le moteur MyIsam) par les éléments suivants

- une intégrité référentielle sur les clés secondaires qui ne peuvent pas prendre la valeur 0 (valeur par défaut d'un entier) ou vide (alphanumérique)

- la valeur par défaut 0000-00-00 des champs date mysql n'est pas acceptée dans postgresql

- le traitement de protection apostrophe en mysql est \' alors qu en postgres, il est '' donc il est utile de remplacer la protection
dans le fichier d'export mysql 

La version 3.0.0 se caractérise par de nouvelles tables de paramétrage titre_civilite, zone_type, voie_type ... et il est utile de
passer par un schema intermédiaire opencimetiere_temp


Construction de la base/schéma postgresql avec les scripts dans data/pgsql de la version 3.0.0
==============================================================================================

Vous devez d'abord executer les scripts de constitution de la base openMairie, schema openCimetiere.

Création d'un shéma opencimetiere_temp pour modifier les tables importées
=========================================================================

Les tables sont créés sans clés primaires et sans clés secondaires.

Les champs date sont créés en varchar(10) pour éviter l'intégrité "date" de postgresql plus forte.
Tous les champs acceptent le "Null"


script de création ::

    SET search_path = opencimetiere_temp, public, pg_catalog;
    
    -- localisation    
    CREATE TABLE zone (
      zone integer,
      cimetiere integer ,
      zonetype varchar(30),
      zonelib varchar(40) 
    );
    CREATE TABLE voie (
      voie integer ,
      zone integer,
      voietype varchar(30),
      voielib varchar(40)
    ) ;
    -- emplacement
    CREATE TABLE emplacement (
      emplacement integer,
      nature varchar(20),
      numero integer,
      complement varchar(6) ,
      voie integer,
      numerocadastre varchar(15) ,
      famille varchar(40) ,
      numeroacte varchar(15) ,
      datevente varchar(10),
      terme varchar(15) ,
      duree integer,
      dateterme varchar(10),
      nombreplace numeric ,
      placeoccupe numeric,
      superficie numeric,
      placeconstat numeric,
      dateconstat varchar(10),
      observation text ,
      plans varchar(30) ,
      positionx integer ,
      positiony integer,
      photo varchar(20) ,
      libre char(3) ,
      sepulturetype varchar(30) ,
      temp1 varchar(100),
      temp2 varchar(100),
      temp3 varchar(100),
      temp4 varchar(100),
      temp5 varchar(100)
    );
    CREATE TABLE defunt (
      defunt integer,
      nature varchar(15),
      taille real,
      emplacement integer,
      titre varchar(4),
      nom varchar(40),
      prenom varchar(40),
      marital varchar(40),
      datenaissance varchar(10),
      datedeces varchar(10),
      lieudeces varchar(40),
      dateinhumation varchar(10),
      exhumation char(3),
      dateexhumation varchar(10),
      observation text,
      reduction char(3),
      datereduction varchar(10),
      historique text
    );
    CREATE TABLE autorisation (
      autorisation integer,
      emplacement integer,
      nature varchar(15) ,
      titre varchar(4) ,
      nom varchar(40) ,
      marital varchar(40) ,
      prenom varchar(40) ,
      datenaissance varchar(10),
      adresse1 varchar(40) ,
      adresse2 varchar(40) ,
      cp varchar(5) ,
      ville varchar(40) ,
      telephone varchar(15) ,
      dcd char(3) ,
      parente varchar(15) ,
      observation text
    ) ;
    CREATE TABLE dossier (
      dossier integer,
      emplacement integer,
      fichier varchar(40),
      datedossier varchar(10),
      observation text,
      typedossier varchar(20)
    );
    CREATE TABLE travaux (
      idtravaux integer,
      idintervenant integer,
      emplacement integer,
      datedebinter date,
      datefininter date ,
      observation text ,
      naturedemandeur varchar(20),
      naturetravaux varchar(40) ,
    );
    CREATE TABLE emplacement_archive (
      emplacement integer,
      nature varchar(20),
      numero integer,
      complement varchar(6),
      voie integer,
      numerocadastre varchar(15),
      famille varchar(40),
      numeroacte varchar(15),
      datevente varchar(10),
      terme varchar(20),
      duree integer,
      dateterme varchar(10),
      nombreplace real,
      placeoccupe real,
      superficie real,
      placeconstat real,
      dateconstat varchar(10),
      observation text,
      plans varchar(30),
      positionx integer,
      positiony integer,
      photo varchar(20),
      libre char(3),
      sepulturetype varchar(30)
    );
    CREATE TABLE defunt_archive (
      defunt integer,
      nature varchar(15),
      taille real,
      emplacement integer,
      titre varchar(4),
      nom varchar(40),
      prenom varchar(40),
      marital varchar(40),
      datenaissance varchar(10),
      datedeces varchar(10),
      lieudeces varchar(40),
      dateinhumation varchar(10),
      exhumation char(3),
      dateexhumation varchar(10),
      observation text,
      reduction char(3),
      datereduction varchar(10),
      historique text 
    );
    CREATE TABLE autorisation_archive (
      autorisation integer,
      emplacement integer,
      nature varchar(15),
      titre varchar(4) ,
      nom varchar(40) ,
      marital varchar(40) ,
      prenom varchar(40) ,
      datenaissance varchar(10),
      adresse1 varchar(40) ,
      adresse2 varchar(40) ,
      cp varchar(5) ,
      ville varchar(40) ,
      telephone varchar(15) ,
      dcd char(3) ,
      parente varchar(15) ,
      observation text 
    );

Transfert des données de localisation
=====================================

L'insertion de la table cimetiere peut se faire directement dans le schéma opencimetiere suite à un export mysql.

L'insertion de la table zone se fait d'abord en opencimetiere_temp.

Ensuite la requête d'intégration dans opencimetiere suivante tient compte de la table 3.0.0 zone_type ::

    -- verification existence cle secondaire zonetype
    select distinct(zonetype) from opencimetiere_temp.zone;

    insert into opencimetiere.zone (zone,cimetiere,zonetype,zonelib) 
    select
        a.zone,a.cimetiere,b.zone_type,a.zonelib
        from opencimetiere_temp.zone a, opencimetiere.zone_type b
        where a.zonetype=b.libelle;

La table des voies a la même difficultée avec voie_type et l'insertion se fait d'abord dans opencimetiere_temp ::

    -- verification des voietype
    select distinct(voietype) from opencimetiere_temp.voie;
    
    insert into opencimetiere.voie (voie,zone,voietype,voielib) 
    select
        a.voie,a.zone,b.voie_type,a.voielib'
        from opencimetiere_temp.voie a, opencimetiere.voie_type b
        where a.voietype=b.libelle;

Mettre à jour les séquences cimetiere, zone et voie ::

    SELECT pg_catalog.setval('cimetiere_seq', 10, true);
    SELECT pg_catalog.setval('zone_seq', 10, true);  
    SELECT pg_catalog.setval('voie_seq', 10, true);  

Transfert des parametres
========================

Utilisateur :

Les noms de champs ont changé : om_utilisateur, om_profil et il y a des champs nouveau obligatoire ! om_collectivité (=1), om_type (=db)
et email (peut être égal à '')
Attention, om_profil est inversé 5=1 , 4=2 ...1=5
A la fin de la récupération, faire la requête suivante ::

    update opencimetiere.om_utilisateur set om_profil = 6 - om_profil where om_utilisateur > 1 -- admin est dans la base

entreprise

identreprise devient entreprise dans la nouvelle base et l'export de cette table peut se faire directement dans opencimetiere


Transfert des emplacements
==========================

On transfere emplacement sur opencimetiere_temp

Il s'agit d'éliminer les dates '0000-00-00' dans les champs : datevente, dateterme et dateconstat ::

    update opencimetiere_temp.emplacement set datevente = null where datevente = '0000-00-00';
    update opencimetiere_temp.emplacement set dateterme = null where dateterme = '0000-00-00';
    update opencimetiere_temp.emplacement set dateconstat = null where dateconstat = '0000-00-00';
    
On peut aussi remplacer '0000-00-00' par null directement dans le fichier d'export

Il est possible que d'autre dates soient malformées comme '2008-01-00'.

Si c'est le cas la requête d'intégration ne fonctionnera pas et il faudra corriger l erreur signalée

Les plans sont dans une table avec un identifiant numérique. Il faut donc les reprendre avec une ou plusieurs requete (une par plan) ::

    update opencimetiere_temp.emplacement set plans = 1 where plans = 'moules.jpg';

Les sepultures type sont aussi dans une table. Il faut donc mettre la cle secondaire numerique dans le champ sepulturetype ::

    update opencimetiere_temp.emplacement set sepulturetype = 4 where sepulturetype like '%pierre%';
    update opencimetiere_temp.emplacement set sepulturetype = 2 where sepulturetype like '%basse%';
    update opencimetiere_temp.emplacement set sepulturetype = 1 where sepulturetype like '%haute%';
    update opencimetiere_temp.emplacement set sepulturetype = null where sepulturetype ='';

 
Il est alors possible de lancer la requête d'intégration ::

    insert into opencimetiere.emplacement
        (emplacement, 
        nature, 
        numero, 
        complement, 
        voie, 
        numerocadastre, 
        famille,
        numeroacte,
        datevente,
        terme,
        duree,
        dateterme,
        nombreplace,
        placeoccupe,
        superficie,
        placeconstat,
        dateconstat,
        observation,
        plans,
        positionx,
        positiony,
        photo,
        libre,
        sepulturetype
        ) 
    select
        emplacement,
        nature,
        numero,
        complement,
        voie,
        numerocadastre,
        famille,
        numeroacte,
        cast(datevente as date),
        terme,
        duree,
        cast(dateterme as date),
        nombreplace,
        placeoccupe,
        superficie,
        placeconstat,
        cast(dateconstat as date),
        observation,
        cast(plans as integer),
        positionx,
        positiony,
        photo,
        libre,
        cast(sepulturetype as integer) 
        from opencimetiere_temp.emplacement ;
        
Transfert defunt
================

Les données de défunt sont transmises dans la table temporaire opencimetiere_temp.defunt

Il est proposé de traiter les dates égales à 0000-00-00 ::

    update opencimetiere_temp.defunt set datenaissance = null where datenaissance = '0000-00-00';
    update opencimetiere_temp.defunt set datedeces = null where datedeces = '0000-00-00';
    update opencimetiere_temp.defunt set dateinhumation = null where dateinhumation = '0000-00-00';
    update opencimetiere_temp.defunt set dateexhumation = null where dateexhumation = '0000-00-00';
    update opencimetiere_temp.defunt set datereduction = null where datereduction = '0000-00-00';

Attention;, il peut subsister des dates non conformes dans un format non accepté par postgres du style 2025-00-00 ou 2030-06-00 
Il faut les rechercher et les traiter avant intégration.

Il se peut que certains défunts ne soient plus rattaché à une concession. On trouve ces concessions en lancant la requete suivante ::

    select emplacement.emplacement,defunt.emplacement  from opencimetiere_temp.defunt
        left join opencimetiere.emplacement on defunt.emplacement = emplacement.emplacement
        where emplacement.emplacement is null order by defunt.emplacement;

Il faut ensuite détruire les défunts dans les emplacements inexistants ::

    delete from opencimetiere_temp.defunt where emplacement in ( liste des emplacements séparés par une virgule);

Il faut ensuite reconstitué la clé secondaire titre qui pointe sur la table titre :

    -- titre
    update opencimetiere_temp.defunt set titre = 1 where titre = 'Mr' or titre = 'M' or titre = 'M.';
    update opencimetiere_temp.defunt set titre = 2 where titre = 'Mell' or titre = 'Mlle'; 
    update opencimetiere_temp.defunt set titre = 3 where titre = 'Mme';
    update opencimetiere_temp.defunt set titre = 4 where titre like 'Enf%' or titre = 'Bébé' or titre='Enfa' or titre = 'enfa';

Vérifier que tous vos champs "titre" sont des clés de la table titre ::

    select titre,count(titre) from opencimetiere_temp.defunt group by titre order by titre;

Vous pouvez intégrer les défunts dans la base opencimetiere ::

    insert into opencimetiere.defunt(
      defunt,
      nature,
      taille,
      emplacement,
      titre,
      nom ,
      prenom ,
      marital,
      datenaissance ,
      datedeces ,
      lieudeces ,
      dateinhumation ,
      exhumation ,
      dateexhumation ,
      observation ,
      reduction ,
      datereduction ,
      historique )
    select
      defunt,
      nature,
      taille,
      emplacement,
      cast(titre as integer),
      nom,
      prenom ,
      marital,
      cast(datenaissance as date),
      cast(datedeces as date),
      lieudeces,
      cast(dateinhumation as date),
      exhumation,
      cast(dateexhumation as date),
      observation,
      reduction,
      cast(datereduction as date),
      historique 
      from opencimetiere_temp.defunt;
    
    -- compteur_defunt est le numero du dernier defunt saisi
    SELECT pg_catalog.setval('opencimetiere.defunt_seq', compteur_defunt, true);

Dans openCimetiere, il faut mettre à "Non" le verrou ::

    update opencimetiere.defunt set verrou = 'Non' ;
    
Transfert des autorisations :
=============================

Transferer les autorisations de mysql dans la base temporaire openmairie_temp, table autoriqation

remplacer les dates du format '0000-00-00' en null

Ensuite ilfaut traiter le titre ::

    update opencimetiere_temp.autorisation set titre = 1 where titre = 'Mr' or titre = 'M' or titre = 'Mr e';
    update opencimetiere_temp.autorisation set titre = 2 where titre = 'Mell' or titre = 'Mlle';
    update opencimetiere_temp.autorisation set titre = 3 where titre = 'Mme';
    update opencimetiere_temp.autorisation set titre = null where titre = '2 en' or titre='' ;


Vérifier avec la requête suivante ::

    select titre,count(titre) from opencimetiere_temp.autorisation group by titre order by titre;
    
Il faut changer le champ dcd qui est booleen et non plus en varchar(3) ::

    update opencimetiere_temp.autorisation set dcd = 't' where dcd = 'Oui' ;
    update opencimetiere_temp.autorisation set dcd = 'f' where dcd = 'Non' or dcd ='   ';

Il faut ensuite vérifier que tous les emplacements soient existants ::

    select  distinct(autorisation.emplacement)  
    from opencimetiere_temp.autorisation left join opencimetiere.emplacement 
    on autorisation.emplacement = emplacement.emplacement 
    where emplacement.emplacement is null 
    order by autorisation.emplacement;

et détruire les autorisations non rattachées à un emplacement ::

    delete from opencimetiere_temp.autorisation where emplacement in 
     (liste d emplacement séparé par une virgule);

On peut ensuite transférer dans opencimetiere ::

    insert into opencimetiere.autorisation(
     autorisation,
      emplacement,
      nature,
      titre ,
      nom ,
      marital,
      prenom ,
      datenaissance,
      adresse1 ,
      adresse2 ,
      cp ,
      ville ,
      telephone ,
      dcd ,
      parente ,
      observation)
    select
      autorisation,
      emplacement,
      nature,
      cast(titre as integer) ,
      nom ,
      marital ,
      prenom ,
      cast(datenaissance as date),
      adresse1,
      adresse2 ,
      cp  ,
      ville ,
      telephone ,
      cast(dcd as boolean),
      parente,
      observation
      from opencimetiere_temp.autorisation;

    
    -- on change aussi la sequence avec son compteur autorisation
    
    SELECT pg_catalog.setval('opencimetiere.autorisation_seq', compteur_autorisation, true);

Transfert des travaux
=====================

Transferer la table de mysql dans la table travaux d'opencimetiere_temp.

Dans les travaux, naturetravaux devient une table et il faut donc changer la clé secondaire ::

    update opencimetiere_temp.travaux set naturetravaux = 6 where naturetravaux = 'Construction caveau T2 haut';
    update opencimetiere_temp.travaux set naturetravaux = 13 where naturetravaux = 'Remise en place pierre tombale';
    update opencimetiere_temp.travaux set naturetravaux = 2 where naturetravaux = 'Permis de construire';
    update opencimetiere_temp.travaux set naturetravaux = 1 where naturetravaux = 'Autorisation de travaux';
    update opencimetiere_temp.travaux set naturetravaux = 3 where naturetravaux = 'Autorisation de recouvrement';
    update opencimetiere_temp.travaux set naturetravaux = 20 where naturetravaux = 'Nettoyage-Consolidation';
    update opencimetiere_temp.travaux set naturetravaux = 11 where naturetravaux = 'Construction pierre tombale';
    update opencimetiere_temp.travaux set naturetravaux = Null where naturetravaux = '';

Vérifier si les clés secondaires existent dans la table naturetravaux

    select distinct(naturetravaux) from opencimetiere_temp.travaux; 

Procéder à l'insertion des données dans opencimetiere ::

    insert into opencimetiere.travaux(
      travaux,
      entreprise,
      emplacement,
      datedebinter ,
      datefininter ,
      observation ,
      naturedemandeur ,
      naturetravaux) 
      select
      idtravaux,
      idintervenant,
      emplacement,
      datedebinter ,
      datefininter ,
      observation ,
      naturedemandeur ,
      cast(naturetravaux as integer) 
        from opencimetiere_temp.travaux;
    
    -- mettre a jour la sequence avec le dernier travaux saisi (compteur_travaux)
    
    SELECT pg_catalog.setval('opencimetiere.travaux_seq', compteur_travaux, true);

Transfert des courriers
=======================

Le profil de la table a peu changer et le chargement peut se faire directement en opencimetiere.

Vérifier cependant que :

- la date du courrier soit au format postgre (pas de 0000-00-00)

- le modéle du courrier existe en om_lettretype

N'oubliez pas de mettre à jour la séquence avec le dernier numéro de courrier saisi (compteur_courrier)::

    SELECT pg_catalog.setval('opencimetierecourrier_seq', compteur_courrier, true);

Transfert des dossiers
======================

Transférer le dossier en table dossier d'opencimetiere_temp

remplacer les dates '0000-00-00'

Vérifier si les emplacements sont présents ::

    select  distinct(dossier.emplacement)  
    from opencimetiere_temp.dossier left join opencimetiere.emplacement 
    on dossier.emplacement = emplacement.emplacement 
    where emplacement.emplacement is null 
    order by dossier.emplacement;

détruiser les dossiers où les emplacements n'existent pas ::

    delete from opencimetiere_temp.dossier where emplacement in 
    (liste des emplacements qui n existent pas séparés par une virgule);

Insérer les dossiers dans la base opencimetiere

    insert into opencimetiere.dossier(
      dossier,
      emplacement,
      fichier,
      datedossier,
      observation,
      typedossier)
    select
      dossier,
      emplacement,
      fichier,
      cast(datedossier as date),
      observation,
      typedossier
      from opencimetiere_temp.dossier;

    -- mettre à jour la sequence dossier
    
    SELECT pg_catalog.setval('opencimetiere.dossier_seq', compteur_dossier, true);


Transfert des fichiers du dossier
=================================

Vous pouvez conserver le file systeme de la version mysql. Dans ce cas la, copier ce qu il y a dans le repertoire trs de
votre opencimetiere 2.10 dans le repertoire trs de la version 3.0.0

Vous pouvez utiliser le nouveau filesysteme de la version openmairie 4.4.0

le plus simple est de mettre vos fichiers en trs/1 et de mettre les fichiers dans le nouveau filesystem en trs/2

Il est proposer auparavant de détruire les enregistrements dossiers qui ne correspondent pas à un fichier
existant et qui plante la procédure de migration 

script delete_dossier.php

    <?php
    // Conexion à la base de données 
    require_once('config.php');
    $sql = "select * from ".$schema.".".$table;
    $res = pg_query($connexion, $sql);
    while ($row = pg_fetch_array($res)) {
        if (!file_exists("../trs/1/".$row['fichier'])){
           echo $row[$table]." ".$row['fichier']."";
          $sql="delete from ".$schema.".".$table." where ".$table."=".$row[$table];
          $res1 = pg_query($connexion, $sql);	
              if ($res1)
            echo "supprime<br>";
          else
            echo " erreur ".$sql;
        }		
    }
    pg_close($connexion);
    ?>

script de connexion config.php

    <?php
    // connexion
    // parametres
    $user= "postgres";
    $pwd = "postgres";
    $host= "localhost";
    $base= "openmairie";
    $schema="opencimetiere";
    $table="dossier";
    // connexion pgsql
    $connexion = pg_connect("host=".$host." port=5432 dbname=".$base." user=".$user." password=".$pwd);
    if (!$connexion) {
      echo "erreur de connexion ".$host." ".$base." ".$user." ".$pwd;
      exit;
    }
    
    ?>

lancer la procédure de migration om_filestorage_migrate.php en paramétrant sans le script ::
        
    le repertoire de départ
    
    $source_conf = array(
        "storage" => "deprecated",
        "path" => "../trs/1/",
    );
    
    ...
    
    // et celui d arrivée
    
    $destination_conf = array(
        "storage" => "filesystem",
        "path" => "../trs/2/",
    );

refaire les emplacements de stockage en préférant un stockage externe a l'application dans dyn/filestorage.inc.php::

    $filestorage["filestorage-default"] = array (
        "storage" => "filesystem", // l'attribut storage est obligatoire
        "path" => "../../files/opencimetiere/", // le repertoire de stockage
        //"path" => "../trs/2", // le repertoire de stockage	
        "temporary" => array(
            "storage" => "filesystem", // l'attribut storage est obligatoire
            "path" => "../tmp/", // le repertoire de stockage
        ),
    );


Problème d'encodage sur la base
===============================

J'ai rencontré sur la base d'arles des problèmes d'encodage existant sur la base mysql que j'ai résolu de la manière suivante :

Dans les fichiers sql, j ai remplacé avec l'éditeur  ::

        Ã§ en ç
        Ã© en é
        Ã en I ?
        Ã‰ en E ?
        Ãš en è
        Ã en I
        Ã en E
         en é
         en à
         en é
        

ou par requetes ::

    select emplacement,observation, replace(observation, 'Ã©', 'é')  from opencimetiere.emplacement;
    
    
    

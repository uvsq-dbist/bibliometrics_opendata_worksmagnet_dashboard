# bibliometrics_opendata_worksmagnet_dashboard
<h1>Suivi du travail sur le Works-magnet</h1>
<h2>En un mot</h2>
L'objectif de l'outil est d'être un dashboard du Works-magnet en affichant à l'utilisateur :
<ul>
  <li>les "issues" open et closed créées par quelqu'un de son institution classées par mois</li>
  <li>pour les "issues" open, les labos added et removed</li>
</ul>
<h2>Utilisation</h2>
L’utilisateur se voit présenter un formulaire où il entre un domaine d'adresse mail, ce qui désigne une institution, et une fourchette d'années 
<br/><br/>
(Le cas échéant, il peut entrer plusieurs domaines d'adresse mail)
<h2>Langage</h2>
HTML, JavaScript
<br/><br/>
N'importe quel browser permet d'utiliser le code
<h2>Fichiers</h2>
Pour permettre une instalation la plus facile possible tout le code (toutes les fonctions) se trouve dans un seul fichier
<h2>Dépendance</h2>
L'outil est dépendant de l'API data.enseignementsup-recherche.gouv.fr avec le point d'entrée https://data.enseignementsup-recherche.gouv.fr/api/explore/v2.1/catalog/datasets/openalex-affiliations-corrections/records et de l'API ROR avec le point d'entrée https://api.ror.org/v2/organizations telles qu'elles existent aujourd'hui (mai 2025) 
<h2>Fonctionnement, fonctions</h2>
Six fonctions : 
<br/><br/>
<ul>
<li>
launch_function()
<br/><br/>
Lancé par le bouton de soumission, lance à son tour get_enseignementsup_recherche_data_function()
<br/><br/>
</li>
<li>get_enseignementsup_recherche_data_function() <= asynchrone
<br/><br/>Va chercher les données dans le point d'entrée https://data.enseignementsup-recherche.gouv.fr/api/explore/v2.1/catalog/datasets/openalex-affiliations-corrections/records
en actionnant une donnée offset afin de couvrir tous les nombres de réponses possibles
<br/><br/>A chaque réponse, actionne can_data_function() qui s'applique à la série de réponses renvoyée par la requête
<br/><br/>
Après le dernier passage, lancement de launch_ror_function()
<br/><br/>
</li>
<li>can_data_function()
<br/><br/>Stocke les données venues d'OpenAlex dans diverses variables
<br/><br/>
</li>
<li>launch_ror_function()
<br/><br/>Lance get_ror_data_function()
<br/><br/>
</li>
<li>get_ror_data_function() <= asynchrone
<br/><br/>Enrichissement par des données récupérées dans le ROR
<br/><br/>Va chercher les données dans le point d'entrée https://api.ror.org/v2/organizations
<br/><br/>Pour éviter une url trop longue, est lancée autant de fois qu'il y a de groupes de d'identifiants ROR
<br/><br/>La taille d'un groupe d'identifiants ROR : variable chunk_size
<br/><br/>Les labos étant souvent connus par leur acronyme, la logique du nom choisi est : S'il y a un acronyme, on prend le premier qui se présente, s'il n'y en a pas, on prend le nom
<br/><br/>Au dernier passage, lancement de l'affichage par la fonction display_function()
<br/><br/>
</li>
<li>display_function()
<br/><br/>Affichage des résultats
<br/><br/>
</li>
</ul>

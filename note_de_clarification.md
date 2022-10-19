# NOTE DE CLARIFICATION DU PROJET

## Objets

-Ressource (classe mère de Livre, OeuvreMusicale et Film):  
&nbsp;-code (chaine de caractères, clé)  
  -titre (chaine de caractères)  
  -dateApparition (date)  
  -éditeur (chaine de caractères)  
  -genre (chaine de caractères)  
  -codeClassification (chaine de caractères, unique)

-Livre:  
  -isbn (chaine de caractères, unique)  
  -résumé (texte)  
  -langue (chaine de caractères)

-OeuvreMusicale:  
  -longueur (entier)

-Film:  
  -durée (entier)  
  -synopsis (texte)  
  -langue (chaine de caractères)

-Exemplaire:  
  -état (neuf|bon|abimé|perdu)  
  -disponible (booléen)  
  -> associé à Ressource (1..n - 1)

-Contributeur:  
  -nom (chaine de caractères)  
  -prénom (chaine de caractères)  
  -dateNaissance (date)  
  -nationalité (chaine de caractères)  
  -> écrit un Livre (1..n - *)  
  -> compose une OeuvreMusicale (1..n - *)  
  -> interprète une OeuvreMusicale (1..n - *)  
  -> réalise un Film (1..n - *)  
  -> joue dans un Film (1..n - *)

-Membre:  
  -login (chaine de caractères, clé)  
  -motDePasse (chaine de caractères)  
  -nom (chaine de caractères)  
  -prénom (chaine de caractères)  
  -adresse (chaine de caractères)  
  -email (chaine de caractères)

-Adhérent:  
  -login (chaine de caractères, clé)  
  -motDePasse (chaine de caractères)  
  -nom (chaine de caractères)  
  -prénom (chaine de caractères)  
  -dateNaissance (date)  
  -adresse (chaine de caractères)  
  -email (chaine de caractères)  
  -téléphone (entier)
  -adhésion (booléen)
  -droitPrêt (booléen)
  -blacklisté (booléen)

-Prêt:  
  -datePrêt (date)  
  -dateRetourPrévue (date)
  -dateRetourRéelle (date)
  -étatRetour (bon|abimé|perdu)
  -> concerne un Exemplaire (* - 1)
  -> est effectué par un Adhérent (* - 1)

-Sanction (classe mère de Retard et Dégradation)

-Retard:
  -débutSanction (date)
  -finSanction (date)

-Dégradation:
  -motif (détérioration|perte)
  -débutSanction (date)
  -finSanction (date)


## Contraintes

-Ajouter une clé artificielle "idExemplaire" à Exemplaire

-Ajouter une clé artificielle "idContributeur" à Contributeur

-Ajouter une clé artificielle "idPrêt" à Prêt

-Ajouter une clé artificielle "idSanction" à Sanction

-Ajouter une méthode "duréePrêt()" à Prêt

-Un adhérent doit s'authentifier pour pouvoir emprunter un document

-Un prêt est possible seulement si l'exemplaire est en bon état et est disponible

-Un exemplaire ne peut pas être disponible et dans un état "abimé" ou "perdu" à la fois

-Un adhérent ne peut emprunter simultanément qu'un nombre limité d'œuvres, chacune pour une durée limitée

-Si un adhérent rend un document en retard, son droit d'emprunt est suspendu pour une durée égale au nombre de jours de retard

-Si un adhérent degrade ou perd un document, son droit d'emprunt est suspendu jusqu'à ce qu'il rembourse le document

-En cas de sanctions répétées, un adhérent peut être blacklisté

-Un adhérent blacklisté ne peut être actuellement adhérent, et donc ne peut pas emprunter de documents

## Utilisateurs

-Membres de la bibliothèques:  
  -gèrent des ressources documentaires: ajouter des documents, modifier leur description, ajouter des exemplaires d'un document, etc.  
  -gèrent les prêts, les retards et les sanctions  
  -gèrent les données des utilisateurs  
  -établissent des statistiques sur les documents empruntés par les adhérents

-Adhérents:
  -recherchent des documents  
  -effectuent et gèrent leurs emprunts  
  -peuvent se désinscrire et se réinscrire

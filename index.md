# Déjeuner Kap-Code
[Ancienne présentation](http://forum.gfii.fr/uploads/docs/ForumGFII_2017_Stephane-Schuck.pdf)

Présentation par Dr Stéphane Schück sur le thème de l'information & épidémiologie `infodémiologie`. En particulier, sur les champs suivants : médicament & pharmacovigilance. Domaine très pertinent car les données directement issues du patient, sans intermédiaire (données authentiques).

Dr Stéphane Schück (expert à la comission des AMM pour l'ancienne agence du médicament).

## Table des matières
* [Introduction](#Introduction)
* [Méthodologie](#Méthodologie)
  - [MedDRA](#MedDRA)
  - [Approche](#Approche)
  - [Sources](#Sources)
  - [Base de données](#BDD)
  - [Algorithmes](#Algorithmes)
  - [Exemple](#Exemple)
* [Résultats](#Résultats)

<!-- toc -->

## Introduction
- [Google frutrend](https://www.google.org/flutrends/about/) : prévision de la grippe à partir des cooccurrences de mots clés sur Google
- [twitter : un outil complémentaire pour la surveillance de l’épidémie saisonnière de grippe en france métropolitaine et en région ?](http://invs.santepubliquefrance.fr/beh/2018/34/pdf/2018_34_2.pdf)
Cette étude  exploratoire a permis de montrer que les données de  Twitter, en complément des systèmes existants, permettent le suivi de l’épidémie saisonnière de grippe en France et en région. Le système devra être amélioré pour confirmer les tendances observées lors de la prochaine épidémie de grippe.
- [The use of social media in public health surveillance](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4542478/pdf/WPSAR.2015.6.2-003.pdf) Revue générale par l'OMS des différents cas d'usage de l'exploration des réseaux sociaux pour la surveillance en santé publique.
- [Epidemiology from Tweets: Estimating Misuse of Prescription Opioids in the USA from Social Media](https://link.springer.com/article/10.1007%2Fs13181-017-0625-5) The purpose of this study was to demonstrate that the geographic variation of social media posts mentioning prescription opioid misuse strongly correlates with government estimates of MUPO in the last month.

## Méthodologie
1212
### MedDRA
[Dictionaire MedDRA](https://fr.wikipedia.org/wiki/MedDRA) : traduction du langage patient en langage médical standardisé (+ obligatoire pour la déclaration de cas de PV)
From [Filtering Entities to Optimize Identification of Adverse Drug Reaction From Social Media: How Can the Number of Words Between Entities in the Messages Help?](https://publichealth.jmir.org/2017/2/e36/)
> we  used the  Medical Dictionary for Regulatory Activities dictionary (MedDRA), which is  the international medical terminology developed under the auspices of the International Conference on Harmonization of Technical Requirements for Registration of Pharmaceuticals for Human Use (ICH). The MedDRA dictionary is organized by system organ  class (SOC) and  divided into  high-level group terms (HLGT), high-level terms (HLT), preferred terms (PT), and lowest-level terms (LLT). Synonymous LLT are grouped under a unique identifier labeled as preferred terms (PT)
> We used a lexicon built in-house by Kappa Santé. The lexicon was derived from the French version of MedDRA 15.0 and was extended by  adding more lay  medical vocabulary. A  fuzzy grouping technique was used to group commonly misspelled words or closely spelled words under one term. The grouping was performed at the MedDRA LLT level. The fuzzy grouping algorithm temporarily strips all vowels (except the first one), strips double or triple consonants from extracted words, and then compares them to see if they are the same. For example, “modeling” and “modelling” would be grouped together [31-34]. The original 15.0 release of MedDRA contains 19,550 PT and 70,177 LLT. Our lexicon contained a total of 19,530 PT and 63,392 LLT. Among them, 259 additional LLT were added by Kappa Santé, for example, “mal au crâne” (French familiar broadly used expression for headache) as a synonym of “mal de tête” (headache). Although not pure synonyms, as “crâne” is not equivalent to “head,” “mal de crâne is a familiar broadly used expression for headache. The decrease in the number of terms was caused by the removal of some PTs that were beyond the scope of ADRs, such as “married.” Moreover, the lexicon was manually reduced by grouping terms with similar meanings, for example, the PTs for “alcoholic” and “alcoholism.” Our final version for disorders contained a total of 63,392 terms (LLT level), including both original MedDRA LLT terms and nonstandard terms. We used the most specific (LLT) level to search for disorder entities in the posts.

Exemple:
> J'ai la tête dans le four (langage patient)
> Céphalée bilatéral de tension (MedDRA)

Dictionnaires de parlé médicaux : non développés en France (dommange !)

### Approche
Keyword search &rarr; Analysis &rarr; restitution

### Sources
- Doctissimo : à la 1ere personne, expérience propre et vécue. D'autres forums médicaux et spécialisés (psychologie)
- Facebook : peur d'exposer ses problématiques de santé car non anonyme
- Twitter : plus court (240 caractères), très ironique + humour, intéressant pour la détection d'épidémie, API permettant une extraction géolocalisée des messages
- Youtube : vidéos mais surtout commentaires (en réaction à une vidéo sur des pathologies)
- Instagram : idem Youtube

### BDD
Dans la base de données de Kap Code : 
- 750.000 témoignages sur le diabète
- 250.000.000 messages analysés sur 12 ans12
- 309.777 couples médicament-concept identifiés

### Algorithmes
TAL (Traitement automatique du langage. Exemple : LDA (Lattent Dirichlet Allocation, 2003 de mémoire))

Les algorithmes en interne (dont certains ont été  publiés ?) :
- analyse de parcours de soin : identifiaction des messages relevant des parcours de soin
- arrêt de traitement : identification des motifs d'arrêt de traitement - observance)
- évloution de la sévérité d'une pathologie
- détection de grossesse
- tératogénicité
- identification du genre
- présence de mots clés
- prise de médicaments : est-ce bien le propos d'une personne qui a pris elle-même les médicaments
- détection de concepts médicaux : identification des concepts médicaux identifiés par le patient puis classer dans la catégorie MedDRA correspondante
- détection des effets indésirables : est-ce que le concept médical exprimé dans ce context est un effet indésirable ou non
- impact sur la qualité de vie

### Exemple : algorithme de détection de cas de PV

Domaine de la déction de signal.
Idée : pour un médicament donné et un concept médical donné, est-ce que la fréquence de concept médical est significativement supérieure à sa fréquence quand on regarde l'ensemble des médicaments (définition du odds-ratio)
- Proportional reporting ratio (PRR)
- Reporting Odds Ratio (ROR)

## Résultats

Présentation sous forme de publications / rapports de recherche / dashboards.
Data visualisation

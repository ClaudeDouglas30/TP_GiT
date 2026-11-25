# TP_GiT

ce lab permet de voir en detail les etape d'initiation a  la manipulation de git 

git diff nous permet de voir la difference sur le code ecrit entre notre repertoire de travail et l'index.

resumer: 

Ce lab a couvert les fondamentaux professionnels de Git : gestion fine des modifications via l’index, lecture/validation des différences, annulation maîtrisée, navigation dans l’historique, synchronisation entre plusieurs copies et intégration via branches/merge. La compétence attendue est la capacité à produire un historique propre, auditable, et aligné avec des pratiques d’ingénierie logicielle.

exercice: 

Q1. Working directory : dossier de travail où tu édites tes fichiers (git status). Index (Staging area) : zone de préparation qui sélectionne les changements à inclure au prochain commit (git add). Repository : base de données Git locale qui enregistre l'historique permanent des commits (git commit).

Q2. burger.txt vient d'être créé et n'a jamais été ajouté à l'Index ni committé : Git ne suit pas encore ce fichier.

Q3. git diff montre les modifications non stagées (Working directory vs Index) ; git diff --cached (ou --staged) montre les modifications déjà stagées (Index vs dernier commit). Exemple : tu modifies encore un fichier après git add, git diff --cached te montre ce qui partira réellement au commit et évite d'oublier une nouvelle retouche.

Q4. Une modification entre dans l'historique au moment de git commit (après avoir été ajoutée à l'Index via git add).

Q5. Le TP impose des commits atomiques (un changement logique précis par commit). Cela rend l'historique lisible, facilite le débogage (git bisect / git log) et permet d'annuler ou d'isoler un changement sans casser le reste.

Q6.

Bash
touch hot_dog.txt
git add hot_dog.txt
git commit -m "Ajout de hot_dog.txt"
git log --oneline
Q7. Les fichiers sous « Changes to be committed » sont staged (prêts pour le prochain commit), tandis que ceux sous « Changes not staged for commit » sont modifiés dans le répertoire de travail mais non ajoutés à l'Index (ils ne seront pas inclus dans le commit sans un nouveau git add).

Q8. Pour relire et vérifier ligne par ligne ses changements avant de les valider dans l'Index et éviter d'inclure du code temporaire, des bugs ou des oublis.

Q9. --graph dessine l'arbre des branches et fusions en ASCII, et --pretty=short affiche un résumé compact (hash, auteur et première ligne du message), ce qui facilite la lecture de l'historique.

Q10. Il retire burger.txt de l'Index (unstage) tout en conservant tes modifications sur le disque dans le Working directory.

Q11. Il écrase les modifications locales de burger.txt avec la version du dernier commit (ou de l'Index). Risque : perte définitive des modifications non committées dans ce fichier.

Q12. Annuler la mise en Index sans perdre le travail en cours :

Bash
git reset HEAD <fichier>
# ou : git restore --staged <fichier>
Q13. Supprimer les modifications locales d'un fichier pour revenir au dernier commit :

Bash
git checkout -- <fichier>
# ou : git restore <fichier>
Q14. Il place le dépôt à l'état exact de ce commit (detached HEAD). git log paraît « incomplet » car il n'affiche que l'historique ancêtre de ce commit et masque les commits plus récents situés plus loin sur la branche.

Q15. Il affiche l'historique de toutes les branches et références (y compris celles qui ne sont pas pointées par HEAD actuel), permettant de repérer l'ensemble des commits vers lesquels voyager.

Q16. C'est lorsque HEAD pointe directement sur un commit précis au lieu d'une branche. Travailler dessus sans branche est déconseillé car les nouveaux commits ne seront rattachés à aucune branche nommée et risquent d'être difficiles à retrouver ou perdus après un changement de contexte.

Q17. Revenir sur la branche active (ex. master ou main) :

Bash
git checkout master
Q18. git clone configure automatiquement une télécommande nommée origin pointant vers l'URL du dépôt distant et crée les branches de suivi distantes correspondantes.

Q19. git commit n'enregistre que dans le dépôt local ; tant que git push n'est pas exécuté, les nouveaux commits ne sont pas envoyés vers le dépôt distant sur GitHub.

Q20. Il envoie les commits locaux de la branche master vers la branche master du dépôt distant origin (et met à jour la référence distante).

Q21. Dans tmp, git pull récupère les commits distants (git fetch) et les fusionne (git merge) dans la branche locale courante afin de mettre la copie à jour.

Q22.

Avec git checkout : git checkout -- description.txt (ou git checkout HEAD -- description.txt).

Avec git restore : git restore description.txt.

Q23. Parce que le clone capture l'état du dépôt distant au moment du clonage ; les commits créés localement ailleurs et non encore poussés (git push) n'existent pas encore sur le serveur distant.

Q24. Avec git branch ou git status. Git marque la branche courante avec une astérisque * (et souvent en vert), par exemple * master.

Q25. git branch fr-main crée uniquement une nouvelle branche nommée fr-main au commit courant, sans déplacer HEAD ni basculer dessus (tu restes sur ta branche actuelle).

Q26. git checkout fr-main bascule sur la branche fr-main et met à jour le Working directory. C'est la même commande (git checkout) que pour voyager dans le temps, mais appliquée ici au nom d'une branche (ce qui garde HEAD attaché à la branche, contrairement à un hash de commit).

Q27. Découper en 3 commits atomiques clarifie l'évolution de chaque message affiché et facilite le suivi ou l'annulation d'une ligne précise. Exemples de messages :

Ajout du premier println

Ajout du deuxième println

Ajout du troisième println

Q28. Le merge n'est pas symétrique car la branche cible (celle où l'on se trouve au moment du git merge) reçoit les changements de la branche source et accueille le commit de fusion (ou avance son pointeur) : fusionner fr-main dans master modifie master, tandis que fusionner master dans fr-main met fr-main à jour avec master.

Q29. C'est un commit qui possède au moins deux commits parents (issus de deux branches fusionnées). On le repère dans l'historique via git log --graph (deux branches qui se rejoignent sur le graphe) ou via l'en-tête Merge: dans git log.


# CREATION D'UN DEPOT CONTENANT UN FICHIER README :
mkdir git-cheatsheet
cd git-cheatsheet 
git init
touch README
git add README
git commit -m 'first commit'
git remote add origin git@github.com:slouis/git-cheatsheet.git
git push -u origin master

# SUPPRESSION DE L'HISTORIQUE D'UN FICHIER zzz :
git filter-branch --index-filter 'git rm --cached --ignore-unmatch zzz' HEAD
git push github master --force


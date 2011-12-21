
## CREATION D'UN DEPOT CONTENANT UN FICHIER README :

    mkdir git-cheatsheet
    cd git-cheatsheet 
    git init
    touch README
    git add README
    git commit -m 'first commit'
    git remote add origin git@github.com:slouis/git-cheatsheet.git
    git push -u origin master

## AJOUT DES COULEURS
    git config color.ui true

## SUPPRESSION DE L'HISTORIQUE D'UN FICHIER `zzz` :

Lien : http://help.github.com/remove-sensitive-data/ :

    git filter-branch --index-filter 'git rm --cached --ignore-unmatch zzz' HEAD
    git push github master --force

## CREER UN "PROXY" GIT EN LOCAL :

Lien : https://moocode.com/posts/6-code-your-own-multi-user-private-git-server-in-5-minutes

    #!/usr/bin/env ruby
 
    # user and permissions are passed from authorized_keys
 
    user = ARGV[0]
    permissions = ARGV[1]
    command = ENV['SSH_ORIGINAL_COMMAND']
    abort unless user and permissions and command
 
    # check the supplied command contains a valid git action
 
    valid_actions = ['git-receive-pack', 'git-upload-pack']
    action = command.split[0]
    abort unless valid_actions.include? action
 
    # check the permissions for this user
 
    abort "read denied for #{user}" unless permissions =~ /r/
    abort "write denied for #{user}" if action == 'git-receive-pack' and permissions !~ /w/
 
    STDERR.write "user #{user} authorized\n"
 
    # user made a valid request so handing over to git-shell
 
    Kernel.exec 'git', 'shell', '-c', command
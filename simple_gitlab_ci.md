*Don't forget to:*
* Add ssh key to your server to be able to ssh into
* Select ssh variable(s) type as file
* Add a blank line at the end for ssh variable(s)
* Make ci branches protected and use protected variables

---

***.branchname.env** files for branches that use ci*
```
export VARIABLE_FOR_SSH="$BRANCHNAME_VARIABLE_FOR_SSH"
export VARIABLE_FOR_SERVER_ROOT_USERNAME="$BRANCHNAME_VARIABLE_FOR_SERVER_ROOT_USERNAME"
export VARIABLE_FOR_SERVER_IP="$BRANCHNAME_VARIABLE_FOR_SERVER_IP"
export VARIABLE_FOR_DIRECTORY="$BRANCHNAME_VARIABLE_FOR_DIRECTORY"
```

---

***.gitlab-ci.yaml***
```
stages:
    - deploy

deploy:
    stage: deploy
    before_script:
        - source .${CI_COMMIT_REF_NAME}.env
        - chmod 400 $VARIABLE_FOR_SSH
    script:
        - ssh -o StrictHostKeyChecking=no -i $VARIABLE_FOR_SSH $VARIABLE_FOR_SERVER_ROOT_USERNAME@$VARIABLE_FOR_SERVER_IP "
            cd $VARIABLE_FOR_DIRECTORY &&
            sudo git config --global --add safe.directory $VARIABLE_FOR_DIRECTORY &&
            usdo git stash -k -u &&
            sudo git pull &&
            composer install --no-interaction &&
            php artisan migrate"
```



*.gitlab-ci.yaml*
```
stages:
    - deploy

deploy:
    stage: deploy
    before_script:
        - source .${CI_COMMIT_REF_NAME}.env
        - chmod 400 $CADDE_SSH
    script:
        - ssh -o StrictHostKeyChecking=no -i $CADDE_SSH root@$CADDE_IP "
            cd $CADDE_DIRECTORY &&
            git config --global --add safe.directory $CADDE_DIRECTORY &&
            git stash -k -u &&
            git pull &&
            composer install --no-interaction &&
            php artisan migrate"
```

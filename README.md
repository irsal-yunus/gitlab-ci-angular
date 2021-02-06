# gitlab-ci-angular
Gitlab CICD Angular using ssh executor:

install runner in server client
config runner based on ssh executor

# setting ssh-key to gitlab :
https://docs.gitlab.com/ee/ci/ssh_keys/
https://docs.gitlab.com/ee/ssh/

before_script:
# install ssh-agent
- 'which ssh-agent || (apk add --update --no-cache openssh-client)'
# run ssh-agent
- 'eval $(ssh-agent -s)'
# add ssh key stored in SSH_PRIVATE_KEY variable to the agent store
- echo "$GITLAB_CI_SSH_KEY" > /tmp/gitlab_ci_ssh
- chmod 600 /tmp/gitlab_ci_ssh
- ssh-add /tmp/gitlab_ci_ssh
# disable host key checking (NOTE: makes you susceptible to man-in-the-middle attacks)
# WARNING: use only in docker container, if you use it with shell you will overwrite your user's ssh config
- mkdir -p ~/.ssh
- echo -e "Host *\n\tStrictHostKeyChecking no\n\n" > ~/.ssh/config

# create variable sesuai kebutuhan script di gitlab-ci
# create triger pipeline untuk triger event dari branch lain
# create personal token untuk crul download artifacts
# 

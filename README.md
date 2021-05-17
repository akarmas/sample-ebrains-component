# sample-ebrains-component
showcase how to mirror from github to EBRAINS Gitlab..

1. Create an empty project at gitlab.ebrains.eu
2. Create a gitlab service account on the new project https://docs.gitlab.com/ee/user/project/settings/project_access_tokens.html
 Settings>Access tokens> Name: ghpusher Expire Date: leave empty to never expire > Create project access token
 Save the new project access token because you will not be able to access it again
3. Go to Settings>Repository>Protected branches and set "Allow force push" to On for the
branches you want to sync 
4. Go to your github repo that you want to mirror to EBRAINS
5. Settings > Secrets > New repository secret
  Set the name of the secret e.g. EBRAINS_GITLAB_ACCESS_TOKEN
  and the value of the secret the token that you copied in step 2.
6. Create the .github/workflows directories in your repository 
https://docs.github.com/en/actions/reference/workflow-syntax-for-github-actions
7. In the .github/workflows directory create a yml file e.g. ebrains.yml
  and define the rules for synching the mirror with Github Actions.

Credits to Arbor team for setting up the flow.

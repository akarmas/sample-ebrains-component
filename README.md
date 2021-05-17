# sample-ebrains-component
The project aims to showcase i) how to set up a mirror code repository from Github to 
EBRAINS Gitlab and ii) the necessary configurations to allow the automated update of
the mirror on certain events.
It can be used to facilitate the initial integration requirements that an EBRAINS component
team has to fulfill.
The steps that need to be followed to achieve this are detailed below and all the files in 
the present project can be used as an example and reference.
Let's assume that we want to mirror a code repository from Github (source_repo) to EBRAINS 
Gitlab (mirror=destination_repo).

The goal is to set up the destination_repo and configure the source_repo to automatically
update the destination_repo when certain events occur.
In this example the event that triggers the automated update is a push event in the master branch.

At the EBRAINS Gitlab perform the following steps:

1. Create an empty project at gitlab.ebrains.eu (destination_repo_name)
2. Create a gitlab service account on the new project (detailed documentation [here](https://docs.gitlab.com/ee/user/project/settings/project_access_tokens.html))
 From the left-side menu navigate to:
 Settings > Access tokens and
 i) set the name variable of the service account (here, Name: ghpusher) 
 ii) set the expiration date of the project access token to be created (here, Expire Date: leave empty to never expire)
 iii) select all the scopes 
 and then click the "Create project access token" button
 The new project access token will be created and you need to save the new project access 
 token because you will not be able to access it again (you will need the project access token
 later in the process of setting up the mirror)
3. Then navigate again from the left-side menu to 
 Settings > Repository > Protected branches 
 and set "Allow force push" to On, for the branches you want to sync from the source_repo to 
 the destination_repo (for this particular example only the master branch will be available)

Then at Github perform the following steps:

4. Navigate to the source_repo that you want to mirror to EBRAINS
5. Navigate from the horizontal menu to: 
 Settings > Secrets > New repository secret
  i) Set the name of the secret (here EBRAINS_GITLAB_ACCESS_TOKEN)
  ii) Set as the value of the secret the token that you created and saved at step 2.
  iii) Click the "Add secret" button
6. Create the .github/workflows directories in the source_repo (detailed documentation [here](https://docs.github.com/en/actions/reference/workflow-syntax-for-github-actions)) 
7. In the .github/workflows directory create a yml file (here ebrains.yml)
  and define the rules for synching the destination_repo with Github Actions

Note that the file ebrains_explanation.yml aims to explain the ebrains.yml and 
facilitate the reader to use it as a template.

## Acknowledgments
Credits to the Arbor team for initially implementing the flow (ebrains mirror [here](https://gitlab.ebrains.eu/arbor-sim/arbor)).

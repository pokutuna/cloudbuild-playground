git-push
===

Example of git commit & push from Cloud Build.

- [cloud-builders/git at master · GoogleCloudPlatform/cloud-builders https://github.com/GoogleCloudPlatform/cloud-builders/tree/master/git]
- [Accessing private GitHub repositories  |  Cloud Build Documentation](https://cloud.google.com/cloud-build/docs/access-private-github-repos)
- [Using secrets and credentials  |  Cloud Build Documentation https://cloud.google.com/cloud-build/docs/securing-builds/use-encrypted-secrets-credentials]

## Using Personal Access Token

Deploy keys are better, it's restricted to access to a specified repository. But generating and mounting keys on multiple repositories are bored. In that case, you can use a personal access token tied to the user's permissions via https.

```yaml
steps:
  # Get credentials from Secret Manager
  # It contains string like `https://username:personalaccesstoken@github.com`
  # see https://git-scm.com/docs/git-credential-store
  - name: gcr.io/cloud-builders/gcloud
    entrypoint: bash
    args:
      - '-c'
      - 'gcloud secrets versions access latest --secret=git-credentials > .git-credentials'

  # Clone the repository.
  - name: gcr.io/cloud-builders/git
    args: ['clone', 'https://github.com/pokutuna/cloudbuild-playground.git']

  # Set git configs to commit files.
  # Use `--local` to store into .git/config.
  # $HOME/.gitconfig is not under the `/workspace` directory.
  # (Or mount & keep the config as global.)
  - name: gcr.io/cloud-builders/git
    dir: $_DIR
    entrypoint: bash
    args:
      - '-c'
      - |
        git config --local user.name pokutuna-bot
        git config --local user.email bot@pokutuna.com
        git config --local credential.helper 'store --file /workspace/.git-credentials'

  ...
```

# ecr-login

Configure AWS credential and region environment variables and logs in the local Docker client to one or more Amazon ECR Private registries. Composite of  https://github.com/aws-actions/configure-aws-credentials and https://github.com/aws-actions/amazon-ecr-login

## Usage

```yaml
jobs:
  push:
    # These permissions are needed to interact with GitHub's OIDC Token endpoint.
    permissions:
      id-token: write
      contents: read

    steps:
      - name: Login to Amazon ECR
        id: login-ecr
        uses: ncarb/amazon-ecr-login@v2

      # reference the output registry to push images
      - name: Push image
        uses: ncarb/tag-push-action@v1
        with:
          registry: ${{ steps.login-ecr.outputs.registry }}
          repository: hubot
          local-image: image
```
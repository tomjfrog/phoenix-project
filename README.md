# Phoenix Project
A sample repo to showcase a modern Software Development Lifecycle approach.

# Initial Setup
The automation featured in this repo was originally created from the JFrog CLI with the command:

## Fork This Repo
## Add Github Actions Secrets
`JF_ACCESS_TOKEN`: An access token that has write permissions to the target repository.
`RELEASE_BUNDLE_SIGNING_KEY`: The name of the GPG Key to use for signing release bundles. This name is created when adding a GPG Key to Artifactory.
`JF_ENV_1`: The base64 encoded string that represents the environment variables to be used for the first environment.  Created by executing `jf c export <server id>` from the JFrog CLI. 
`JF_INSTANCE_NAME` The name of the JFrog instance to use for the environment.  This is the name of the server created when executing `jf c add <server id>` from the JFrog CLI.
7

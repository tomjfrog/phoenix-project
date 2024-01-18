# Phoenix Project

A sample repo to showcase a modern Software Development Lifecycle approach.

This demo showcases RBv2 capabilities in the context of a (project)[https://jfrog.
com/help/r/jfrog-platform-administration-documentation/introduction-to-projects]

There is a different (demo)[https://github.com/tomjfrog/feniks],  `tomjfrog/feniks` that showcases RBv2
capabilities without a project.

# Initial Setup

The automation featured in this repo was originally created from the JFrog CLI with the command: `jf c export`. This
will create a base64 encoded string representing a pre-configured JPD from your local JF CLI installation.

## Fork This Repo

## Add Github Actions Secrets

Add the following as _Repository Secrets_ in the _Settings_ tab of the repository:

* `JF_ACCESS_TOKEN`: An access token that has write permissions to the target repository.
* `RELEASE_BUNDLE_SIGNING_KEY`: The *name* of the GPG Key to use for signing release bundles. This name is created when
  adding a GPG Key to Artifactory via `Platform Security -> Keys Management -> Signing Keys`. NOTE: This is not the
  same as a GPG Key that's added via the REST API for RBv1 Distribution purposes.
* `JF_ENV_1`: The base64 encoded string that represents the environment variables to be used for the first environment.
  Created by executing `jf c export <server id>` from the JFrog CLI.

## Add Github Actions Variables

Add the following as _Repository Variables_ in the _Settings_ tab of the repository:

* JF_BASE_URL
* `JF_INSTANCE_NAME` The name of the JFrog instance to use for the environment. This is the name of the server created
  when executing `jf c add <server id>` from the JFrog CLI.
* `JF_PROJECT_KEY`: This demo features the RBv2 capabilities in the context of a project. This variable should be set to
  the Project key for a given project in Artifactory.
* `JF_RELEASE_BUNDLE_NAME`: Arbitrary name that will be used as the name of the RBv2.
* `JF_VIRTUAL_REPO`: The virtual repo that contains the `dev-local` local repo and the Remote Proxy needed to build
  and publish the initial artifact and Maven build.

## Execute a Typical Release Workflow

### Build an Artifact

By committing to `main`, whether via a direct push or a pull request, the `build` workflow will be triggered. This
workflow will build the artifact and publish it to the target repository in Artifactory. For this demo, it's recommended
to set a virtual repo that holds a local and remote repository. This will allow the build to be published to the
local by default.

### Create a Release Candidate

To build an RBv2, create a release in Github with the pattern `x.{x}.{x}-rc-{y}`. Examples of valid tags to trigger
this workflow are `1.0.0-rc-1` or `1.0.0-rc-2`. This will execute the following steps workflow which will:

1. Create an RBv2 from the latest published build.
2. Promote that RBv2 to a specified QA repo.

This RBv2 could be distributed to Edge nodes for in-depth QA testing, which would likely be done with at least some
manual workflows.

### Create a SemVer Production Release

To build a SemVer release, create a release in Github with the pattern `vx.{x}.{x}`. This will trigger a workflow to
promote the latest RBv2 to a Production repository and distribute it to an Edge node. The distribution will also do
a path mapping to the Edge node, thus copying the artifacts to a sensical path on the Edge node.

2

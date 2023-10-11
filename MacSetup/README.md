# Buildkite Mac Setup

This document will aim to describe the steps required to setup a Mac for Buildkite development.

## Requirmenets

- A Buildkite account. You can get a free account at the [Buildkite website](https://buildkite.com/).
- [Homebrew](https://brewh.sh) installed.
- Docker.

## Install the agent

These instructions are taken from the Buildkite Agent page. You will need to have a Buildkite account.
https://buildkite.com/organizations/<ORG_NAME>/agents#setup-macosn.

```shell
brew install buildkite/buildkite/buildkite-agent
```

The next sections assume that all your Homebrew files are installed in `/opt/homebrew`. This is known as the Homebrew prefix. You can confirm the location of your Homebrew prefix by running `brew --prefix`.

## Configure the agent

The agent needs to be configured with your Buildkite agent token. You can find your agent token on the Buildkite Agents page **https://buildkite.com/organizations/<ORG_NAME>/agents** .

The configuration file is located at the following location:
`/opt/homebrew/etc/buildkite-agent/buildkite-agent.cfg`

The following values need to be set in the configuration file: 

### `token`

This is your buildkite token. You can find it on the Buildkite Agents page **https://buildkite.com/organizations/<ORG_NAME>/agents* .

### `name`

This is the name of the agent. It can be anything you like.

### `tags`

This is a comma separated list of tags. You can use these tags to target specific agents when running builds.
A typical tags value might be `ci=true,docker=true,queue=default`.

The `docker=true` tag is used to indicate that the agent can run docker builds. The `queue=default` tag is used to indicate that the agent can run builds from the default queue.

### `build-path`

This is the path to the directory where builds will be run. The default value is `/opt/homebrew/var/buildkite-agent/builds`.

### `hooks-path`

This is the path to the directory where buildkite hooks are stored. The default value is `/opt/homebrew/etc/buildkite-agent/hooks`.

### `plugins-path`

This is the path to the directory where buildkite plugins are stored. The default value is `/opt/homebrew/etc/buildkite-agent/plugins`.

## Start the agent

To start the agent run the following command:

```shell
buildkite-agent start
```

You should now be able to see the  agent running on the Buildkite Agents page **https://buildkite.com/organizations/<ORG_NAME>/agents** .

## Docker Configuration

To run docker builds you will need to configure the agent to run docker builds. This is done by adding the `docker=true` tag to the agent configuration file.

Apart from this, you will also need to add your actual build paths to the docker Filesharing settings. This is done by going to `Docker -> Preferences -> Resources -> File Sharing` and adding the build paths to the list of shared folders.

In the event that this does not work, you may need to edit the docker configuration file directly. This is located at `~/Library/Group Containers/group.com.docker/settings.json`. You will need to add the build paths to the `filesharingDirectories` array.

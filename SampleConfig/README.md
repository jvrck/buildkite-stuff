# Sample Configuration

This directory contains a sample configuration for the Buildkite agent named `buildkite-agent.cfg`. 

This file is used by the Buildkite agent to configure itself. The file is a simple text file with a key-value pair on each line. The key and value are separated by a colon (`:`). The key is case-insensitive. The value is case-sensitive. The file is located in the `/buildkite` directory on the agents host.

At minimum, you will be required to insert your agent token into the file. You can find your agent token in the Agents section of your Buildkite account https://buildkite.com/organizations/<your-org>/agents.

Add your token to the line in the file that begins with `token`. 

Another useful configuration key is `tags`. This is useful to specify a agent queue to distinguish between different types of agents. For example, you may want to have a queue for agents that run on Windows and another for agents that run on Linux. You can then specify which queue to use when you create a new build.

The `tags` configuration is useful if you need tor run Docker in the agent. You will need to supply a tag of `docker=true` to the agent. This will ensure that the agent is scheduled on a host that has Docker installed.
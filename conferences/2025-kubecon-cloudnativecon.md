---
title: Conferences/2025/Kubecon & CloudNative Con
---

KubeCon & Coud Native Con Europe 2025
===
KubeCon + CloudNativeCon Europe 2025 took place in London. I had an all access pass which also included access to the
co-located conferences at day 0.

All talks will be available on the [CNCF YouTube channel](https://www.youtube.com/@CloudNativeComputingFoundation). So I
will not go into detail about the talks. I will just mention my aggregated learnings by topic

## Backstage

Backstage is a developer portal created by Spotify. I spent most of day 0 in Backstage talks.

A common theme was using custom plugins and (ab)using the scaffolder plugin for a set of guided workflows.

- The Scaffolder plugin, created for scaffolding new projects can do so much more. A lot of companies built a lot of
  workflow automation around it. Form API calls over automated component creation.
- Extending backstage is not that hard, keeping up with the changes is. Changelogs might not always contain breaking
  changes for the specific use cases and APIs used
- Backstage can serve as single source of truth for ownership information. As this introduces a critical dependency on
  backstage, it is important to have a backup plan in case backstage is not available. This can be done by e.g. falling
  back to the last information applied.
- Updating backstage can be tricky, especially as migrations are only working forwards and dont offer downgrading
  functionality

## Platform Engineering

As platform engineering is a hot topic, there were a lot of talks about it. I will just summarize the most important
points I took away.

- *Rent an engineer* is a great concept allowing upstream teams to lend engineering power for a limited time. This helps
  creating better connections to the
  upstream teams and helps the platform team to understand the needs of product teams.
- Users not only need to be heard, but also given the feeling to be heard. These can be two fundamentally different
  things.

## Automating maintenance

At Spotify `Fleet management` is used to automate the boring tasks like rolling out configuration changes between
standardized repositories, updating dependencies or applying critical bugs in a automated matter.

Their architecture is pretty simple, yet powerful

- Repository can decide if it wants to be part of it
- Migrations are created centrally
- Each migration runs a kubernetes job
    - Check out the repository
    - Apply the changes
    - Create a pull request
    - Auto-merge when CI passes
- Status can be checked in a global dashboard across all services

Unfortunately, this is not publicly available, but it is a great example of how to automate boring tasks and
standardize the process.

## Scaling prometheus

Etsi had an interesting challenge where they could not scale Prometheus horizontally anymore.

They got some help from Grafana Labs and an Prometheus maintainer.

- Disabling HTTP/2 was necessarry to avoid reusing sockets too much, which was limiting network bandwidth on Google
  Cloud
- Resharding is an expensive operation, for them it was better to just hardcode the min and max shards
- WAL write can become a bottleneck, as it is the only real synchronous part of Prometheus
- Reducing compaction time can significantly reduce the time it takes to write data to disk, at the cost of needing more
  disk space
- Turning off periodic go garbage collection using `GOGC=off` can help only reduce CPU load significantly, but also
  reduce the
  amount of memory used by Prometheus. In combination with limiting memory for the go runtime, this can significantly
  reduce the CPU load, enhancing performance
---
title: Conferences/2025/Kubecon & CloudNative Con
---

KubeCon & Coud Native Con Europe 2025
===
KubeCon + CloudNativeCon Europe 2025 took place in London. I had an all access pass which also included access to the
co-located conferences at day 0.

All talks will be available on the CNCF YouTube channel. So I
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
- Providing and using an API for the platform is a great way to provide a consistent interface for the platform. This
  can
  be done by providing a GraphQL API or a REST API. Its a good practice to also use the API for the platform team to
  consume the platform. This way, the API is used by both sides and can be improved over time.
- Starting a platform team makes sense when there is a clear need for it, e.g. when the number of services is
  growing and the need for a consistent interface is growing. It is important to have a clear vision for the platform
  team and to communicate it to the rest of the organization.
- Focus more on productivity and business value than on the technology. This helps to create a better experience for
  the users and to create a better product.
- Keep migration efforts as low as possible. Avoid breaking changes and try to keep the migration as simple as
  possible. This can be done by providing a clear migration path and by providing documentation for the migration.

## Marketing mindset for internal platforms / tools

Marketing as much as I hate it, is a great way to promote internal tools and platforms. It is important to create a
marketing strategy for the platform. This can be done by creating a marketing plan, defining the target audience and
creating a brand for the platform.

- Marketing is not only for external products. It can also be used for internal tools and platforms.
- Define personas for the users of the platform. This helps to understand the needs of the users and to create a better
  experience for them.
- Create a strong brand for the platform. This bonds the users to the platform and creates a sense of being part of
  something
  bigger. Merch, stickers, etc. can help to create a strong brand.
- Select advocate users to help promote the patform. The social proof is a great way to promote the platform.
- Create a community around the platform. This can be done by creating a slack channel, a mailing list or a forum.
- Create a feedback loop with the users. This can be done by creating a feedback form or a survey. This helps to
  understand the needs of the users and to create a better experience for them.
- Have at least one "5 minute guide" for each tool. This helps to onboard new users and to create a Wow effect.
- Gamify usage of the platform. This can be done by creating a leaderboard or a points system. This helps to create a
  sense of competition and to motivate users to use the platform.

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

## New with Prometheus 3

Prometheus 3 is a major release containing a lot of new features and improvements. Some of the most important
features are:

- New, cleaner UI
- AST for PromQL in the UI
- Metric discovery right from the new UI
- Native histogram support

## Nais - the platform for the norwegian government organizations

[Nais](https://nais.io) is a platform for the norwegian government organizations. It is a great example of how to build
a platform for
government organizations. Some of the most important features are:

- Open Source
- Strong documentation and branding
- Government internal community via Slack

They also started strong with
the [Marketing mindset for internal platforms / tools](#marketing-mindset-for-internal-platforms--tools) and
created a strong brand for the platform. They also created a community around the platform and created a feedback
loop with the users.


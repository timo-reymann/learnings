---
title: Conferences/2021/IT-Tage
---
IT-Tage 2021
===

> [IT Tage](https://www.ittage.informatik-aktuell.de/) is a conference for software development, architecture, AI, databases, DevOps and agile for the german speaking IT world

## GitOps mit GitLab: DevSecOps, Source Code Handling und CI/CD


### Workflows CI

- The later you fix security the more it costs
- Add security scanning to process → code might be manipulated not only dependencies


### Conversational Development

- Slice and deploy changes instead of features, improving feedback loop
- Deploying to rush hour is better than deploying on less frequent times → better and clearer feedback from usage
- Gitlab records presentations beforehand and does Q&A async → this way anyone can watch stuff when he has time
- Open communication is always preferred if possible → no 1:1 chats when discussing features/changes
- Build EVERYTHING together, one feedback loop for all stages


## Domain-driven Design für Legacy-Systeme

- Build a bubble inside the old monolith → small change and get some experience
- Expose legacy as services → easier to replace and modernize
- Extract step by step → clear value for business
- Build new data model and translate in separate layer to legacy → new and old in same application
- Data models should be split (also step by step)


## Gute Programmierer – schlechte Software. Warum Software selten dem Stand der Technik entspricht

- "Stand der Technik" ist not always the latest and greatest
- build minimal solutions that work for the use case
- at delivery the dependencies MUST be up to date
- :warning: violations can end up in law suits


## API-Design oder: Wie stelle ich sicher, dass meine Anwendung unwartbar wird?

- always develop consumer driven (pact seems to be only tool available cross tooling)
- it doesn't have to be always HTTP/REST
- APIs can/should also be organized by domain or even consumer to make changes easier


## Accelerate! Wie Chaos Engineering die Software-Delivery-Performance verbessern kann

- Prod is not always the right stage for chaos engineering


## Wie die NASA mich für eine Qualitätsworkshop-Methode inspirierte

### Quality Storming

- empty room → better mental setting
- all participants should be equal (no manager etc)
- include equal amount of business people (e. g. sales, devs)
- moderation is key
- understand what the current status of the process is, NOT what it SHOULD be
- define input and output to make the journey and bounds clear
- event stream should be in format "verb norm" e. g. Run tests
- participant count should be min 5 but at most 10


### Making errors and improving the handling

- the awareness of mistakes gets less over time
- find errors in the process without blaming
- the longer you make a mistake the harder it gets to learn from it
- minimize time to error discovery


### Making processes understandable

- BPMN makes it easier to talk about processes than other modelling languages or custom boards


## DevOps-Geschichten aus dem wahren Leben

- prevent "single person of knowledge"
- migrate complex parts first
- person with less knowledge always types in pair programming


## Keycloak.X: Keycloak ist tot – es lebe Keycloak!

- providers etc wont change
- ~ 2022 Keycloak won't be supported anymore → RH SSO till 2024
- FINALLY metrics integrated without 3rd party
- base path can be added with QUARKUS_HTTP_ROOT_PATH → no longer /auth in front
- profile support (like spring boot)


## Inspiriert programmieren! Kreativitäts-Tipps für den Entwickler-Alltag

- write down all ideas (even if they are stupid)
- get into inspirative situations (analyze situations)


## Die 7 Anti-Pattern für gute Architekturdokumentationen – Meisterwerk oder Groschenroman?


### Ideas

- become independent of availability of persons
- in good company with ADRs
- https://www.iese.fraunhofer.de/blog/softwarearchitekturen-einfacher-designen-und-verstaendlicher-dokumentieren-mit-dem-fraunhofer-adf/
- package mapping in docs


### Anti Patterns

- document after the change is implemented → loss of context
- only technical docs
    - document functionality
    - data decomposition and structure
- no "devtime" documentation
- over focused on templates
    - can and should be extended to be more useful
    - focus on the reader not the format
- too complex diagrams
    - legend
    - concise
    - no auto-layout


## Gute Legacy? Schlechte Legacy?
- modularized monoliths can still be good
- sometimes legacy makes sense to keep and refactor instead of recreate

- 10 000 000 lines projects can still be maintainable
- design patterns help the brain "chunk information" and not only make decisions easier but also onboarding new devs/reading code
    - wrong patterns interrupt flow
    - correct patterns don't require the brain to process unnecessary information
- analyze with tools and don't make assumptions
- visualize complexity and make money aspect clear to get management onboard


## Microservices: Wo sind meine Transaktionen und meine Konsistenz hin?

- solutions are available but leaky, not reliable
- bounded contexts are the only real solution
- error handling as process step e. g. when something fails do the business case rollback => nothing in stock after order? - go the journey back and replace item in order with voucher etc
    - "SAGA": https://microservices.io/patterns/data/saga.html


## Authentizität im Job – tut das weh?

- learn from other people is not always copying as long if its not only one person
- new roles might require change in personality or behaviour


## Weil jeder anders tickt – Best Practices zum Miteinander in interdisziplinären Teams

- education has no influence on diversity
- co-location is not blocking productivity at all


## Microfrontends – Konzept, Umsetzung und Anwendung in großen IT-Projekten

- server side includes can be combined with custom elements → SEO + reactivity
- webpack 5 has a solution → unstable for prod 
- cross team architecture board helps
- namespaces are mandatory and make trouble shooting easier
    - css
    - events
    - paths etc
- preact, hyperapp or other small frameworks should be used → smaller bundle size
- only makes sense for larger projects


## Projekt Onboarding in Zeiten von Corona

- too specific; left early


## DevOps als Enabler für Agilität

- deploy more often and even smaller
- cross-functional teams are the way to go
- Commits → conventional
- track deployment frequency is important


## DSGVO: Anonymisierung von heterogenen Test-Datenbanken und -Filesystemen

- attacking testing sytems is more common than expected
    - maybe lower standards
    - not all data is anonymized



# Infrastructure & Operations

## DevOps and SRE

- link to google review book

## Instrastructure as Code

- ansible
- terraform

## Observability

- architecture Prom + alermanager + DB
- architecture ELK
- OpenTracing / Jaeger etc

## Container Scheduling

- hashistack
- kubernetes
- service mesh
- ...

## Release engineering

- CI/CD - gitlab
- Artifactory

## Docker Hardening

## Chaos Engineering

## Post Mortem Report

### Title

- Date
- Project
- Environnement
- Infrastructure

### Incident overview

Brief description of the incident. Include general informations, like for instance:

- Context, reasons, time and duration of the incident
- Type of incident: complete downtime, loss of data, partial interruption of normal operation etc.
- People impacted by the incident: end users, business owners, developpers etc.

### Timeline

Precise timeline of the different issues that happened during the incident, including:

- Starting date of the incident
- Date when actions were taken to mitigate the incident
- Resolution date of the incident

### Root cause analysis

Detailed desciption of what caused the incident.

### Resolution

Description of all the actions taken to resolve the incident.
Include every actions taken, even the incorrect of ineffective ones.

### Preventive measures

List all the measures that should be taken to prevent/avoid this type of incident to happen again in the future.
Ex: logging, monitoring, code improvements, development workflow etc.

## Resources

- [Counting & Timing](https://code.flickr.net/2008/10/27/counting-timing/)
- [Brendan Gregg Overview](http://www.brendangregg.com/overview.html)
- [eBPF - Rethinking the Linux Kernel](https://www.infoq.com/presentations/facebook-google-bpf-linux-kernel/)

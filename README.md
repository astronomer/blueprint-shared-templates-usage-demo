# Blueprint shared templates usage demo

This repository demonstrates usage of [Blueprint templates](https://github.com/astronomer/blueprint) installed from a package.

Installing Blueprint templates from a package is a best practice when templates are shared amongst multiple development teams, each using their own Git repository. Installing a package avoids copy/pasting code into each repository and that code getting out of sync:

```mermaid
flowchart TD
    subgraph Platform["Platform Engineering Team"]
        BSR["Blueprint Shared<br/>Template Repository"]
        V100["v1.0.0"]
        V110["v1.1.0"]
        V200["v2.0.0"]
        BSR --> V100
        BSR --> V110
        BSR --> V200
    end

    subgraph DevTeams["Dev Teams"]
        R1["Dev Team 1<br/>Airflow Repo 1"]
        R2["Dev Team 2<br/>Airflow Repo 2"]
        DOTS["..."]
        RN["Dev Team N<br/>Airflow Repo N"]
    end

    V100 -.->|installed by| R1
    V100 -.->|installed by| R2
    V200 ~~~ DOTS
    V200 -.->|installed by| RN

    classDef plain fill:none,stroke:none;
    class DOTS plain;
```

This repository resembles one of the Airflow repositories, used by a dev team.

- See this example repository containing shared Blueprint templates: https://github.com/astronomer/blueprint-shared-templates-demo.
- Templates are released via a versioned package, and installed in each development team's Git repository. See [requirements.txt](requirements.txt). That ensures everybody knows which version of shared Blueprint templates is used.
- This repository only needs to install the shared Blueprint templates package. That package includes [airflow-blueprint](https://pypi.org/project/airflow-blueprint) as a dependency.

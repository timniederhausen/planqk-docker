[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

# Dockerized PlanQK Environment

Docker Compose file for running the entire PlanQK platform.

The fastest way to get started is using [Docker Compose](https://docs.docker.com/compose/):

  ```shell
  docker-compose pull
  docker-compose up
  ```
  
Wait a few seconds, then access the [PlanQK REST API](http://localhost:8080/atlas).

| PlanQK Component | URL | GitHub | Docker Hub |
|:------------------- |:--- |:------ |:---------- |
| QC-Atlas |<http://localhost:8080/atlas> | [Link](https://github.com/PlanQK/qc-atlas) | [Link](https://hub.docker.com/r/planqk/atlas) |
| Postgres DB | <http://localhost:5432> | [Link](https://github.com/docker-library/postgres) | [Link](https://hub.docker.com/_/postgres) |

**Make sure following ports in your environment are free in order to start the PlanQK platform properly:**

* `8080`
* `5432`

## How To

Simple How-To section to cover different kinds of use cases.

### Initialize the db on startup 

If an ssh key named planqk-atlas-content-ssh_secret is located in the directory, the planqk/initialized-db image pulls 
data from the repo set by QC_ATLAS_CONTENT_REPOSITORY_URL. The default is "git@github.com:PlanQK/planqk-atlas-content.git", 
which is a private repo for our content. To obtain the ssh key, ask the dev team for it. Alternatively, you can [generate a new pair of public/private 
ssh keys](https://help.github.com/en/enterprise/2.17/user/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent) 
and add the public key as a deploy key to the repo (https://github.com/PlanQK/planqk-atlas-content/settings/keys).
The private key needs to be saved as planqk-atlas-content-ssh_secret in the directory of the docker-compose file. 

Database initialization is skipped? 
--> Make sure the previous processes are terminated with ```docker-compose down```, otherwise postgres might skip the initialization. 

### How to run the environment in development mode

* To enable the execution of the QC-Atlas from your IDE the corresponding docker container can be removed
* Start the environment using: `docker-compose -f docker-compose.dev.yml up`
* Make sure you configure the QC-Atlas correctly to access the other components

### Tips and Tricks

```bash
# Pull the latest images
docker-compose pull

# Validate and view the resulting configuration
docker-compose [-f <file> ...] config

# Start services in background
docker-compose up -d

# Shutdown services and remove container
docker-compose down -v

# Display useful logs
docker-compose logs -f [--tail=1 <SERVICE_NAME>...]
docker-compose logs -f qc-atlas db
```

## Haftungsausschluss

Dies ist ein Forschungsprototyp.
Die Haftung für entgangenen Gewinn, Produktionsausfall, Betriebsunterbrechung, entgangene Nutzungen, Verlust von Daten und Informationen, Finanzierungsaufwendungen sowie sonstige Vermögens- und Folgeschäden ist, außer in Fällen von grober Fahrlässigkeit, Vorsatz und Personenschäden ausgeschlossen.

## Disclaimer of Warranty

Unless required by applicable law or agreed to in writing, Licensor provides the Work (and each Contributor provides its Contributions) on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied, including, without limitation, any warranties or conditions of TITLE, NON-INFRINGEMENT, MERCHANTABILITY, or FITNESS FOR A PARTICULAR PURPOSE.
You are solely responsible for determining the appropriateness of using or redistributing the Work and assume any risks associated with Your exercise of permissions under this License.

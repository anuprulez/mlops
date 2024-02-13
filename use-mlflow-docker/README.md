
## ML model building and deployment using MLFlow and Docker

- Build docker container: `docker build -t mlflow-docker -f Dockerfile . `

- Run `mlflow run <<path to the DIR containing MLproject file>> -P alpha=0.5`

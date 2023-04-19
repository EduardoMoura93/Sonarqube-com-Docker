# Sonarqube com Docker
Utilizar o Sonarqube local (na maquina do dev) com docker, para analisar e medir a qualidade do código.

Instale o Docker:
```
$ sudo apt-get install docker
$ sudo apt-get install docker.io
$ docker -v
```

Baixe a imagem do Sonarqube:
```
$ docker pull sonarqube
```

Execute o Sonarqube:
```
$ docker run -d --name sonarqube -e SONAR_ES_BOOTSTRAP_CHECKS_DISABLE=true -p 9001:9000 sonarqube:latest
Configure um token de acesso que sera necessário para conectar ao Sonar:
a. Log in to http://localhost:9001 with System Administrator credentials (login=admin, password=admin).

b. Crie um token para o user admin (TOKEN_DE_UM_USUARIO_DO_SONAR): Administration > Security > Users > Update Tokens
```

Para realizar a analise de uma projeto Gradle, execute:
```
$ gradle sonarqube -Dsonar.verbose=true -Dsonar.host.url="http://localhost:9000" -Dsonar.login="f571721bd9f037532b8521dcec44dc465d9012f2"
Para realizar a analise de uma projeto Maven, execute:

$ mvn clean verify sonar:sonar -Dsonar.host.url="http://localhost:9001" -Dsonar.login="squ_c32b828d22b7b45f284c1b26905eb7dd56a58b02"
```

Acesse o Sonarqube no Navegador e visualise a analise no menu Projetos:
```
http://localhost:9001/projects
```

Comandos mais completos com os principais parâmetros:
```
gradle sonarqube -Dsonar.verbose=true -Dsonar.host.url="http://localhost:9000" -Dsonar.login="TOKEN_DE_UM_USUARIO_DO_SONAR" -Dsonar.projectKey=“CHAVE_DO_PROJETO” -Dsonar.projectName=“NOME_DO_PROJETO” -Dsonar.projectVersion=“VERSAO_DO_PROJETO” -Dsonar.exclusions=“/UM_PACKAGE/, /UMA_CLASSE”

mvn clean verify sonar:sonar -Dsonar.host.url="http://localhost:9000" -Dsonar.login="squ_c32b828d22b7b45f284c1b26905eb7dd56a58b02" -Dsonar.projectKey=“CHAVE_DO_PROJETO” -Dsonar.projectName=“NOME_DO_PROJETO” -Dsonar.projectVersion=“VERSAO_DO_PROJETO” -Dsonar.exclusions=“/UM_PACKAGE/, /UMA_CLASSE”
```

# github-jenkins-sonar

* https://www.linkedin.com/pulse/integrating-github-webhooks-jenkins-automate-unit-becerril-dom%C3%ADnguez

## Pipeline Github -> Jenkins -> Sonarqube

### 1 Jenkins
Manage Jenkins -> Manage Plugins
* Install sonar plugins
* Install github plugins
* Create an api token (jenkinapitoken)

## 2 Github
* Create a github personal token:  
  Profile -> Settings -> Developer Settings or https://github.com/settings/tokens  (githubapitoken)  

* Create a Webhook to jenkins:  
  https://<jenkinsexternalip>:<port>/github-webhook/ set the (jenkinapitoken) as secret

## 3 Jenkins for github
* Create a github credential 
  user/password (user=davidboukari, password=(githubapitoken)  description: (davidboukarigitwithgithubtoken)
  
* Set up github server plugin  
  Manage Jenkins -> Configure System -> Github Server:  
  name=Github Connexion, API URL: https://api.github.com, credential=(davidboukarigitwithgithubtoken)
  
* Create pipeline multi-branches  
  Type: github  
  set the repo  
  Credential: (davidboukarigitwithgithubtoken)

## 4 Sonarqube Create a token api
* Security -> User:  (sonarqubeapitoken)
  
## 5 jenkins for sonarqube
* Create a credential type text with (sonarqubeapitoken) named (sonarqubeapitoken)  
  
* Manage Jenkins -> Configure System ->SonarQube servers
  name: sonarque, URL: http://<ipsonar>:<port>, credential=(sonarqubeapitoken)
  

## 6 Sonarqube
* Create a project
* Create a key
* Create a webhook for jenkins to notify jenkins that the job is finish
  Configuration -> Webhook: 
  Values: name=jenkins	https://<jenkinsexternalip>:<port>/sonarqube-webhook
  
## 7 Code source in jenkins file
* Build section
* Sonar section
* sonar-project.properties 
* java
```
cat sonar-project.properties
sonar.projectKey=java-swagger-demo
sonar.sources=src
sonar.java.binaries=target/classes,target/test-classes
sonar.language=java
sonar.sourceEncoding=UTF-8
sonar.verbose=true
```

* Python
```
cat sonar-project.properties
sonar.projectKey=jenkins-test-pipeline
sonar.projectVersion=1.0
sonar.sources=app
sonar.language=py
sonar.sourceEncoding=UTF-8
sonar.tests=tests
sonar.python.coverage.reportPaths=coverage.xml
sonar.verbose=true
```









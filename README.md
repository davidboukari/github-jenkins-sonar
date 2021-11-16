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

## 3 Jenkins
* Create a github credential 
  user/password (user=davidboukari, password=(githubapitoken)  description: (davidboukarigitwithgithubtoken)
  
* Set up github server plugin  
  Manage Jenkins -> Configure System -> Github Server:  
  name=Github Connexion, API URL: https://api.github.com, credential=(davidboukarigitwithgithubtoken)
  
* Create pipeline multi-branches  
  Type: github  
  set the repo  
  Credential: (davidboukarigitwithgithubtoken)
   

## 4 Sonarque
* Create a project
* Create a key

## 5 Code source In jenkins file
* Build section
* Sonar section
* sonar-project.properties 








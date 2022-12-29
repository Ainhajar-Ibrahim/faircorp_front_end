# Faircorp (Front End)

Based on the [Quentin Richaud's](https://gitlab.com/emse1/cours-dev-web-5-vuejs/-/blob/master/presentation/slides.md#assignment) assigenement.  
A vueJS application that makes use of the faircorp [API](https://faircorp-no-security-ainhajar-ibrahim.cleverapps.io/) deployed on clever Cloud and made in the course of [Guillaume Ehret](https://dev-mind.fr/).  

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```
## Docker 

To create a container and run it, run the following command in the root file of the project (you need to have docker installed and running): 
```
docker run -it -p 8081:8080 --rm --name fontend faircorp/frontend
```

## Docker-Compose 
First of all modify the docker-compose.yml file by giving the paths on your computer of the backend and the front end 
```
backend:
    build: 
      context: backend\path
      
frontend:
    build: 
      context: frontend\path
```
To create the two containers and run them, run the following command in the root file of the project (you need to have docker installed and running): 
```
docker-compose up -d --force-recreate
``` 
To stop the containers and delete them run the following command: 
```
docker-compose down --rmi all
```

## Warning

If the backend doensn't work anymore (due to unkown reasons) you can find it [here](https://github.com/Ainhajar-Ibrahim/faircop/tree/new-branch) (new-branch). Clone it and use it locally.  
In that case you have to modify the API's hostname in ./src/config.js in the frontend. (The backend runs mostly on port:8080 so the new hostname will be https://localhost:8080)

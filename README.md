# Faircorp (Front End)

Based on the [Quentin Richaud's](https://gitlab.com/emse1/cours-dev-web-5-vuejs/-/blob/master/presentation/slides.md#assignment) assigenement.  
A vueJS application that makes use of the faircorp [API](https://app-41a50e3d-146d-4bfc-80ae-84cb8df274e1.cleverapps.io/) deployed on clever Cloud and created made in the course of [Guillaume Ehret](https://dev-mind.fr/).  

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

## Warning

If the backend doensn't work anymore (due to unkown reasons) you can find it [here](https://github.com/Ainhajar-Ibrahim/faircop/tree/new-branch) (new-branch). Clone it and use it locally.  
In that case you have to modify the API's hostname in ./src/config.js in the frontend. (The backend runs mostly on port:8080 so the new hostname will be https://localhost:8080)
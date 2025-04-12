# POVO Interface
Hi! This is a redesign of Notre Dame's class search (PATH) and class registration (NOVO) softwares into one application. 
The project is being completed by Clair Green, Peter Hofley, and Michael Sorenson as part of a Human Computer Interaction class.
From our designs and Figma implementation, Clair coded this interface in Vue.js from scratch.
See below for some instructions on getting it running! 

## Project setup
```
npm install
```

## Extra Package Setup Needed
```
npm install -g vue-cal@next
npm install @vue/cli
vue add typescript 
```

## Typescript
Before adding Typescript, make sure you copy all the code in App.vue as this will replace it. Vue will ask you a bunch of questions, and you can just say yes
to all of them. After this, open App.vue, paste the code from before, and continue. (Or simply return to the previous commit once vue updates the code)
**In case main.ts gets deleted** simply create a main.ts file in povo-interface/src with the same code as in the github repo

### Run the prototype
```
npm run serve
```


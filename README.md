# Quasar and GraphQL
### State Without Vuex
For this demo we are going to use GraphQL and integrating vue-apollo https://apollo.vuejs.org/ with Quasar and the Quasar Apollo App Extension https://github.com/quasarframework/app-extension-apollo.  
### Install Quasar CLI and create a project
```npm install -g @quasar/cli```   
```quasar create graphql-demo```  
```quasar dev``` 
### install Apollo and vue-apollo via Quasar's App Extensions
```quasar ext add @quasar/apollo```  
#### Remove the extension
```quasar ext remove @quasar/apollo```  
### Set up the vue compiler to accept "dangerous tagged template strings"
Go to your quasar.conf.js file and enter the following under the build property.  
```js 
chainWebpack (chain, { isServer, isClient }) {
  chain.module.rule('vue')
    .use('vue-loader')
    .loader('vue-loader')
    .tap(options => {
      options.transpileOptions = {
        transforms: {
          dangerousTaggedTemplateString: true
        }
      }
      return options
    })
  }
``` 
### To use .gql or .graphql files add this
```js 
chain.module.rule('gql')
   .test(/\.(graphql|gql)$/)
   .use('graphql-tag/loader')
   .loader('graphql-tag/loader')
```  
#### The build property shoud look like this
```js  
build: {
      vueRouterMode: 'hash', // available values: 'hash', 'history'

      chainWebpack (chain, { isServer, isClient }) {
        chain.module.rule('vue')
          .use('vue-loader')
          .loader('vue-loader')
          .tap(options => {
            options.transpileOptions = {
              transforms: {
                dangerousTaggedTemplateString: true
              }
            }
            return options
          })
          chain.module.rule('gql')
          .test(/\.(graphql|gql)$/)
          .use('graphql-tag/loader')
          .loader('graphql-tag/loader')
        },
```   
### quasar.extensions.json
This is where your GraphQL endpoint is added.  
### The Folder in src quasar-app-extension-apollo  
In ```appollo-client-config.js``` you can add Apollo Client configuration options.  

In ```apollo-client-hooks.js``` you can add your custom code for processing before or after the client is initialized. For instance, you might want to add code for auhorization after the client in created.  
### The Flow of Data in GraphQL and Quasar
![alt text](https://github.com/BoMarconiHenriksen/quasar-and-graphql/blob/master/flow.png "Data Flow")  
### Initialize the Cache


### docpad
---
https://github.com/docpad/docpad

```js
var docpadInstanceConfiguration = {};
require('docpad').createInstance(docpadInstanceConfiguration, function(err.docpadInstance){
  if(err) return console.log(err.stack);
});

var renderOpts = {
  text: 'here is some **markdown**',
  filename: 'markdown',
  renderSingleExtensions:true
};
docpadInstance.action('render', renderOpts, function(err,result){
  console.log(result);
});

var renderOpts = {
  path: '/some/file.html.md',
  renderSingleExtensions:true
};
docpadinstance.action('render', renderOpts, function(err,result){
  console.log(result);
});

var renderOpts = {
  path: '/some/file.html.nd',
  renderSingleExtensions:true
};
docpadInstance.action('render', renderOpts, function(err, result){
  console.log(result);
});

var generateOpts = {
  collection: docpad.getCollection(),
  reset:true
};
docpadInstance.action('generate', generateOpts, function(err,result){
  if(err) return console.log(err.stack);
  console.log('OK')
});

docpadInstance.action('sever', functin(err,result){
  if(err) return console.log(err.stack);
  console.log('OK');
});

docpadInstance.action('generate server', function(err,result){
  if(err) return console.log(err.stack);
  console.log('OK');
});

docpadInstance.action('generate watch', function(err,result){
  if(err) return console.log(err.stack);
  console.log('OK');
});

database = docpadInstance.getDatabase()

document = docpadInstance.createDocment(data, options)
file = docpadInstance.createFile(data, options)

database = docpdInstance.getDatabase()
document = docpadInstance.createDocument(data, options)
database.add(document)
database.add(file)

docpadInstance.parseDocumentDirecory(options, next)
docpadInstance.parseFileDirectory(options, next)

resultCollection = docpadInstance.getFiles(query, sorting, paging)
resultModel = docpadInstance.getFile(query, sorting, paging)
resultCollection = docpadInstance.getFileAtPath(path, sorting, paging)
resultModel = docpadInstance.getFileAtPath(path, sorting, paging)
resultModel = docpadInstance.getFileById(id, {collection:null})
docpadInstance.getFileByRoute(url, function(err, resultModel){
  if ( err ) console.log(err.stack)
})

var express = require('express');
var http = require('http');
var app = express();
var server = http.createServer(app).listen(8080);
app.use(app.router);
var docpadInstanceConfiguration = {

};
var docPadInstance = require('docpad').createInstance(docpadInstanceConfiguration, function (err){
  if (err) return console.log(err.stack);
  docpadinstance.action('generate server watch', function(err){
    if(err) return console.log(err.stack);
  });
});

app.get '/alias-for-home', (req,res,next) ->
  req.templateData => {
    weDidSomeCustomRendering: true
  };
  var document = docpadInstance.getFile({relativePath:'home.html.md'});
  docpadInstance.serverDocument({document, req, res, next});
```

```
npm install -g npm
npm install -g docpad@6.80
docpad init
docpad run

docpad install eco
docpad install livereload

docpad install ghpages
docpad deploy-ghpages --env static

npm install --save-dev docpad-plugin-ghpages
```

```html
<html>
<head>
  <title><%= @document.title >
    <%= if @document.title then "#{@document.title} | Me" else "Me" %>
    <%= if @document.title then "#{@document.title} | #{@site.title}" else @site.title %>
    <%= @getPreparedTitle() %>
  </title>
  <%- @getBlock("meta").toHTML() %>
  <%- @getBlock("styles").toHTML() %>
</head>
<body>
  <h1><%= @document.title %></h1>
  <%- @content %>
  <%- @getBlock("scripts").toHTML() %>
  <%- @getBlock("styles").add(["/styles/style.css"]).toHTML() %>
  <%- @getBlock("scripts").add(["/vendor/jquery.js","/scripts/script.js"]).toHTML()%>
<ul>
 <% for page in @getCollection("html").findAll().toJSON(): %>
   <li class="<%= if page.id is @document.id then 'active' else 'inactive' %>">
     <a href="<%= page.url %>">
       <%= page.title %>
     </a>
   </li>
 <% end %>
</ul>
<% for page in @getCollection("page").JSON(): %>
<rule name="RemoveTMLExtensions" stopProcessing="true">
</rule>
<rule name="RewriteHTMLExtensions" stopProcessing="true">
  <match url="(.*)">
  <conditions>
    <add input="{REQUEST_FILENAME}" matchType="IsFile" negate="true"/>
    <add input="{REQUEST_FILENAME}" matchType="IsDirectory" negate="true"/>
  </conditions>
  <action type="Rewrite" url="{R:1}.html">
</rule>
</body>
</html>
```

```coffee
h1 {
  color: red;
}

h1
  color: red
  
docpadConfig = {
}
module.exports = documents = docpadConfig

docpadConfig = {
  templateData:
    site:
      title: "Me"
}

docpadConfig = {
  templateData:
    site:
      title: "Me"
    getPreparedTitle: -> if @document.title then "#{@document.title} | #{@site.title}" else @site.title
}

docpadConfig = {
  collectins:
    pages: ->
      @getCollection("html").findAllLive({isPage: true})
}

docpadConfig = {
  collections:
    pages: ->
      @getCollectin("html").findAllLive({isPage:true}).on "add", (model) =>
        model.setMetaDefaults({layout:"default"})
}
```


```js
(function(){
  $("body").hide().fadeIn(1000);
})();

if [-e "$DEPLOYMENT_SOURCE/package.json"]; then
  cd "$DEPLOYMENT_SOURCE"
  npm install --production --silent
  exitWithMessageOhError "npm failed"
  cd -> /dev/null
fi
```

```json
"engines": {
  "node": "6",
  "npm": "3"
},
"dependencies": {
  "docpad": "6",
  "docpad-plugin-blah": "2"
},
"main": "node_modules/.bin/docpad-server",
"scirpts": {
  "start": "docpad-server",
  "test": "docpad generate --debug --silent --env static",
  "info": "docpad info --silent"
}

{
  "scripts": {
    "deploy": "docpad deploy-ghpages  --silent --env static"
  }
}
```

```Procfile
web: npm start

heroku config:add NODE_ENV=production
rhc app create PROJECTNAME https://raw.githubsercontent.com/kyrylkov/openshift-iojs/master/metadata/mainfest.yml
rhc set-env -a PROJECTNAME NODE_ENV='production'
rhc alias-add PROJECTWEBSITE.COM -a PROJECTNAME
rhc app show -a PROJECTNAME
rhc app deploy https://github.com/USER/REPO.git#master -a PROJECTNAME
rhc tail -a PROJECTNAME
azure site deploymentscript --basic -t bash

travis encrypt "DEPLOY_USER=$YOUR_GITHUB_USERNAME" --add env.globa
travis encrypt "DEPLOY_TOKEN=$THE_PRESONAL_ACCESS_TOKEN" --add env.global
travis encrypt "GITHUB_TRAVIS_TOKEN=$THE_PERSONAL_ACCESS_TOKEN" --add env.global

shh-keygen -g rsa -b 4096 -C "circle@bevry.me"
```

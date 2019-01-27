### docpad
---
https://github.com/docpad/docpad

```
npm install -g npm
npm install -g docpad@6.80
docpad init
docpad run

docpad install eco
docpad install livereload

docpad install ghpages
docpad deploy-ghpages --env static
```
``
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
},
```

```Procfile
web: npm start

heroku config:add NODE_ENV=production
rhc app create PROJECTNAME https://raw.githubsercontent.com/kyrylkov/openshift-iojs/master/metadata/mainfest.yml
rhc set-env -a PROJECTNAME NODE_ENV='production'
rhc alias-add PROJECTWEBSITE.COM -a PROJECTNAME
```

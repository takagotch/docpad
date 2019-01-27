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
```

```
<html>
<head>
  <title><%= @document.title ></title>
  <%- @getBlock("meta").toHTML() %>
  <%- @getBlock("styles").toHTML() %>
</head>
<body>
  <h1><%= @document.title %></h1>
  <%- @content %>
  <%- @getBlock("scripts").toHTML() %>
</body>
</html>
```

```
```



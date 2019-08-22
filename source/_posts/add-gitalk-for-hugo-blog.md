---
title: "Add Gitalk for comments in Hugo Blog"
description: "Add Gitalk for comments in Hugo Blog"
date: "2019-08-10T11:12:00+08:00"
thumbnail: ""
categories:
  - Tools
tags:
  - Hugo
---

`Gitalk` is a comment plug based on Github issue api. 
`Hugo` can compile the Markdown files with themes and templates into static web files, such as CSS, HTML and JavaScript.

To use `Gitalk` in the `Hugo` blog, we need to add Gitalk related code as `<div>` into the HTML template.
Then update the config.toml for `Gitalk`.
<!--more-->

## Create Github Application
Firstly, you should create Github Application on Github.
Yon can refer to the official sites below for more information.

- https://github.com/gitalk/gitalk/
- https://gitalk.github.io/

Then you can get Client ID and Client Secret.

## Create Gitalk Comments Template
```
{{ if .Site.Params.enableGitalk }}
<div id="gitalk-container"></div>
<link rel="stylesheet" href="https://unpkg.com/gitalk/dist/gitalk.css">
<script src="https://unpkg.com/gitalk/dist/gitalk.min.js"></script>
<script>
  const gitalk = new Gitalk({
    clientID: '{{ .Site.Params.Gitalk.clientID }}',
    clientSecret: '{{ .Site.Params.Gitalk.clientSecret }}',
    repo: '{{ .Site.Params.Gitalk.repo }}',
    owner: '{{ .Site.Params.Gitalk.owner }}',
    admin: ['{{ .Site.Params.Gitalk.owner }}'],
    id: location.pathname, // Ensure uniqueness and length less than 50
    distractionFreeMode: false // Facebook-like distraction free mode
  });
  (function() {
    if (["localhost", "127.0.0.1"].indexOf(window.location.hostname) != -1) {
      document.getElementById('gitalk-container').innerHTML = 'Gitalk comments not available by default when the website is previewed locally.';
      return;
    }
    gitalk.render('gitalk-container');
  })();
</script>
{{ end }}
```

I'm using the `Mainroad` theme, so I just overwrite the `comments.html` with the code above.

## Update config.toml
```
[params]
  enableGitalk = true
  
[params.gitalk]
    clientID = "[Client ID]" # Your client ID
    clientSecret = "[Client Secret]" # Your client secret
    repo = "" # The repo to store comments
    owner = "" # Your GitHub ID
    admin= "" # Required. Github repository owner and collaborators. (Users who having write access to this repository)
    id= "location.pathname" # The unique id of the page.
    labels= "gitalk" # Github issue labels. If you used to use Gitment, you can change it
    perPage= 15 # Pagination size, with maximum 100.
    pagerDirection= "last" # Comment sorting direction, available values are 'last' and 'first'.
    createIssueManually= false # If it is 'false', it is auto to make a Github issue when the administrators login.
    distractionFreeMode= false # Enable hot key (cmd|ctrl + enter) submit comment.
```

- replace [Client ID] with Github Application's Client ID
- replace [Client Secret] with Github Application's Client Secret
- set repo to your blog address
- set owner and admin to your GitHub ID

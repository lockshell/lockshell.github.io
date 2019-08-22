---
title: "Display Word Count in Hugo Blog"
description: "Display Word Count in Hugo Blog"
date: "2019-08-10T10:57:14+08:00"
thumbnail: ""
categories:
  - "Tools"
tags:
  - "Hugo"
---

`Hugo` has many template params for the blog web page. There are two which are related to word count of articles.
<!--more-->
- `.FuzzyWordCount`: 文章内容的大致单词数 (字数)
- `.WordCount`: 文章内容的单词数 (字数)

## Add Word Count template in hugo theme

I'm using the `Mainroad` theme and wanna to append the word count behind the category info.

So I append the blow code in `categories.html`.
```
<span class="meta__text post-word-count"> {{ .WordCount }} words</span>
```

The content of the `categories.html`.
```
{{- if .Params.categories }}
<div class="meta__item-categories meta__item">
	{{ partial "svg/category.svg" (dict "class" "meta__icon") }}
	<span class="meta__text">{{ range $index, $category := .Params.categories }}{{ if gt $index 0 }}, {{ end }}<a class="meta__link" href="{{ "categories/" | relLangURL }}{{ . | urlize | lower }}" rel="category">{{ . }}</a>{{ end }}</span>
</div>
{{ end -}}
<span class="meta__text post-word-count"> {{ .WordCount }} words</span>
```

Great, it works. You can see there are about 160 words in this article.

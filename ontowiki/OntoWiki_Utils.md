---
title: OntoWiki_Utils
tags: [ontowiki]
sidebar: ontowiki_sidebar
permalink: /OntoWiki_Utils.html
editme_path: ontowiki/OntoWiki_Utils.md
---
This class provides a couple of utilities for different use cases.

## compactUri ($uri)

With the following command the uri in $uri will be compacted. That means that for instance **http://www.w3.org/2000/01/rdf-schema#** will replaced by **rdfs:**.
```
<?php
$uri = "http://www.w3.org/2000/01/rdf-schema#label";
$compactUri = OntoWiki_Utils::compactUri($uri);
// now $compactUri = "rdfs:label"
```

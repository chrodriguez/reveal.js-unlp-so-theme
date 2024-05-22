---
title: Mikroways reveal.js theme demo
scripts:
  - https://cdn.jsdelivr.net/npm/reveal.js-mermaid-plugin@2.1.0/plugin/mermaid/mermaid.min.js
  - https://cdn.jsdelivr.net/npm/asciinema-player@3.6.3/dist/bundle/asciinema-player.min.js
  - example/js/script.js
css:
  - https://cdn.jsdelivr.net/npm/asciinema-player@3.6.3/dist/bundle/asciinema-player.min.css
revealOptions:
  transition: 'concave'
  transitionSpeed: 'slow'
---
<!-- .slide: class="main-cover" data-transition="zoom" -->

# reveal.js
## Tema para la la facultad de informática de la UNLP

---
<!-- .slide: class="dark-logo-left" -->

## Dark with botom left logo

* Show how lists are shown
* Show blockquotes styles
* Other slides styles
* More styles
* Links are [like this](https://mikroways.net)

----
<!-- .slide: class="dark-logo-center" -->

# Dark with bottom cenetered logo

----
# This is a normal slide

* In normal styles background is light
* Links are [like this](https://mikroways.net)

> Blockquotes are shown like this
---
<!-- .slide: class="dark-logo-center" -->
## Dark with blockquote

This is a sample text

> And this is inside a blockquote

---
# Text in columns

This text is outside columns, but the following text is placed inside columns:

<div class="container">
<div class="col">

### Column 1

This is a text inside column 1. As you can see, text flows but don't overlaps
with next column
</div>

<div class="col">

### Column 2

* Item 1
* Item 2
</div>
</div>

----
# Text in small columns

This text is outside columns, but the following text is placed inside columns:

<div class="container">
<div class="col small">

### Small Column 1

This is a text inside column 1. As you can see, text flows but don't overlaps
with next column
</div>

<div class="col small">

### Column 2

* Item 1
* Item 2
</div>
</div>
---

# Shadows

----

## Text with shadow

<div class="shadow">
This text has shadow. As you can see, no border is added only a background
shadow
</div>
----

## An image with shadow

<div class="container small">

<div class="col">

![some image](images/frog.jpeg)<!--.element: height="400px" class="shadow" -->

</div>
<div class="col">

## Title

Nice frog with shadow

</div>
</div>

---
<!-- .slide: class="dark-logo-center" -->

# Asciinema

----
## Sample

<asciinema
  cast="images/sample.cast"
  opts-autoplay="true"
  opts-idle-time-limit="1"
  opts-speed="3"
  opts-rows="24"
  opts-terminal-font-family="'Meslo Font', monospace"
/>


----

## Asciinema integration

Configure reveal-md to use scripts and css like this:

<pre>
<code class="yaml hljs" data-line-numbers="5,6,8" >
title: Some title
highlightTheme: vs2015
scripts:
  - https://cdn.jsdelivr.net/npm/asciinema-player@3.6.3/dist/bundle/asciinema-player.min.js
  - example/js/script.js
css:
  - https://cdn.jsdelivr.net/npm/asciinema-player@3.6.3/dist/bundle/asciinema-player.min.css
...
</code>
</pre>

> Note asciinema version  3.6.3 is used. But what is `js/script.js` ?

----
## What is js/script.js

Loads asciinema on ready and when enter a slide, play asciinema if present:

<pre>
<code class="js hljs" >
function snakeToCamel(str) {
    return str.toLowerCase().replace(/([-_][a-z])/g, group =>
          group
            .toUpperCase()
            .replace('-', '')
            .replace('_', '')
        );
}

function setAsciinema(event) {
    const asciinemas = document.getElementsByTagName("asciinema");
    for (let i=0; i < asciinemas.length; i++) {
          let opts = {}
          let attrs = asciinemas[i].getAttributeNames().filter(
                  (n) => n.startsWith("opts-") );
          for (let o=0; o < attrs.length; o++) {
                  opts[snakeToCamel(attrs[o].replace(/^opts-/,''))] =
                        asciinemas[i].getAttribute(attrs[o]);
                }
          asciinemas[i].playerObject = AsciinemaPlayer.create(
                  asciinemas[i].getAttribute("cast"),
                  asciinemas[i],
                  opts
                );
        }
};

function playAscinema(event) {
    const asciinemas = event.currentSlide.getElementsByTagName("asciinema");
    for (let i=0; i < asciinemas.length; i++) {
          if (asciinemas[i].playerObject) {
                    asciinemas[i].playerObject.seek(0);
                    asciinemas[i].playerObject.play();
                }
        }
};


Reveal.on('ready', setAsciinema);
Reveal.on('slidechanged', playAscinema);

</code>
</pre>

---
<!-- .slide: class="dark-logo-center" -->

# Mermaid support

----

## Git graphs

<div class="mermaid">
  <pre>
    %%{init: { }}}%%
    gitGraph
      commit id: "Commit inicial"
      branch develop
      checkout develop
      commit
      commit
      checkout main
      merge develop id: "Merge"  tag: "0.1.0"
      checkout develop
      commit
      commit
  </pre>
</div>

----

## Or mindmaps

<div class="mermaid">
  <pre>
    %%{init: { }}}%%
      mindmap
        root((pod))
          {{Container}}
              Secret
              ::icon(fa fa-key)
              Configmap
              ::icon(fa fa-file)
              PersistentVolume
              ::icon(fa fa-hdd)
                  (PersistentVolumeClaim)
          [Replicaset]
            (Deployment)
          (Statefulset)
          (Daemonset)
          (Job)
            (Cronjob)
          )Service(
              )Ingress(
  </pre>
</div>

----
## Even timelines


<div class="mermaid shadow">
  <pre>
    %%{init: { }}}%%
    timeline
      1979: chroot en Unix
      2004: Solaris Containers
      2005: Open VZ
      2006: Process containers (cgroups)
      2008: LXC
  </pre>
</div>

> Note shadow is added

----

## Mermaid integration

Configure reveal-md to use mermaid plugin

<pre>
<code class="yaml hljs" data-line-numbers="5,6" >
title: Some title
highlightTheme: vs2015
scripts:
  - https://cdn.jsdelivr.net/npm/reveal.js-mermaid-plugin@2.1.0/plugin/mermaid/mermaid.min.js
  - example/js/script.js
...
</code>
</pre>

> Note mermaid-plugin version 2.1.0

----
## What is js/script.js

As simple as

<pre>
<code class="js hljs">
options.plugins.push(RevealMermaid);
</code>
</pre>

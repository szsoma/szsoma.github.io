---
layout: post
title: Jekyll blogolás
tags:
  - blog
  - frontend
  - jekyll
hero: https://cdn.lynda.com/course/383124/383124-635857017109698776-16x9.jpg
overlay: blue
published: true
---

Egy gyors áttekintés a Jekyll blogokról és a <a href="https://pages.github.com/" target="_blank">Github Pages</a>-ről.
{:.lead}
<!--break-->

Amikor pár hónapja megfogalmazódott bennem, hogy valahogy el kellene kezdeni tapasztalatot megosztani természetesen a blog volt az első ötletem. Utána elgondolkoztam egy podcaston is, de sajnos hülye hangom van mikrofonban :)
Szóval maradt a blogolás. De ha már lesznek front-end témák is, hogy fog kinézni, hogy egy Index vagy Google blogon csinálom?! Elkezdtem szétnézni, hogy milyen lehetőségek vannak, de Wordpress-t nem akartam használni. Maradt tehát a hipszter Jekyll! Nem bántam meg mert nagyon vicces így blogolni és jó érzés, hogy én heggesztettem össze.

## Hogy működik ez az egész?

Az első lépéseket leírtam az előző <a href="https://szsoma.github.io/posts/jekyll" target="_blank">postban</a>. Miután létrehoztuk a Jekyll projektünket elkezdhetjük felépíteni az oldalunkat vagy kereshetünk egy template-et is. Rengetegen csinálták meg a saját blogjukat Jekyll-el és tették elérhetővé pl. a <a href="http://jekyllthemes.org/" target="_blank">jekyllthemes.org</a>-on. Designer szemmel… inkább több a gané mint a szép, de azért lehet találni jókat is. A harmadik lehetőség — amit én is választottam — a kettő ötvözete. Magyarul kiválasztottam egy alap témát és utána azt testreszabtam, megpimpeltem kicsit.

## Config, liquid, yaml, stb…

A blogunk “beállításai” egy konfig file-ban vannak eltárolva. Itt állítjuk be a blog címét, font készletet, tulajdonost, leírást, a különböző social media felhasználóneveinket a kontakthoz. A html-t pedig úgy írjuk meg, hogy a config.yml[^1] file-ból húzzuk be ezeket az infókat Liquid template nyelvvel. A Liquid egy Shopify által fejlesztett sablonnyelv. Az ügyfeleiknek szerettek volna teljes tervezési szabadságot nyújtani vele. Igazából egy híd a sablonok és az adatok között. Fő célja az újrafelhasználhatóság. Gyakorlatban:

![800x400](https://soma.shoprenter.hu/custom/soma/image/data/liquid.jpg "liquid mukodese"){:.lead}

~~~HTML
{% raw  %}
<a href=”https://github.com/{{ site.author.github }}” target=”_blank”>
{% endraw  %}
~~~

Ez egy egyszerű link a fejlécben, annyit tesz, hogy a https://github.com/ mögé bekerül a config file author > github értéke, ami egész pontosan így néz ki:

~~~JS
[...]
author:
  fullname : John Doe
  github   : jdoe
[...]
~~~

![800x400](https://soma.shoprenter.hu/custom/soma/image/data/config-yaml.JPG "config file"){:.lead}

Ennek az a nagy előnye, hogy nem kell keresgélni az értékeket az kódokban, elég a config.yml-ben megváltoztatni. Természetesen, ha egy sablon Jekyll blogot töltöttünk le, akkor már meg van írva ez a file és csak fel kell tölteni a saját felhasználóneveinkkel, címmel, nevünkkel, fontunkkal stb.

Liquid-del html kódrészeket is illeszthetünk be. Nekem például így van megoldva a Disqus integráció is. Disqus.html-ben van a beillesztendő script és a post.html layout végén csak be van húzva ezzel a kóddal:

~~~HTML
{% raw  %}
{% include externals/disqus.html %}
{% endraw  %}
~~~

## Post
Ha új postot akarunk kitenni, akkor nincs más dolgunk, mint a posts mappában létrehozni egy markdown file-t. Dátum és utána cím kötőjellel elválasztva:  2017–10–18-blog-cime.md. Ide kell megírni a <a href="https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet" target="_blank">szintaktikának</a> megfelelő postunkat. Akár használhatjuk a <a href="https://stackedit.io/" target="_blank">Slackedit</a>-et is.
Ha local-on meg akarjuk nézni az oldalt, futtatni kell a

~~~JS
jekyll serve
~~~

parancsot és már nézhetjük is mit csináltunk. A bejegyzésünk a post.html layoutnak megfelelően fog megjelenni. Ennek szerkesztésével tudjuk testreszabni a bejegyzés sablonunkat. Kibővíthetjük egy hero képpel, a végére illeszthetünk be comment boxot vagy épp liquid-del saját megosztás gombokat készíthetünk:

~~~JS
{% raw  %}
<a href=”https://plus.google.com/share?url={{ site.url }}{{ page.url }}”
{% endraw  %}
~~~

## Pakoljuk fel a cuccot Githubra!
Eldöntöttük hát, hogy belevágunk a blogolásba mégpedig ezzel a kiválló Jekyll-el mert imádjuk a kihívásokat. Hogy ez mindenki számára elérhető legyen a legjobb, legegyszerűbb és legolcsóbb megoldás az, hogy Github Pages-el hostoljuk. Természetesen tudunk hozzá saját domaint is használni. 

Ha felhasználónév.github.io nevű repo-t csinálunk a blogunknak akkor a Github egyből tudni fogja, hogy ez egy Github Pages lesz. 

Dióhéjban ennyi lenne az alap. Nem egyszerű átlátni kezdőként, de kezdem kapisgálni, hogyan is működik. Legközelebb megmutatom, milyen új feature-öket csináltam eddig a blogomba!

[^1]: A YAML egy adat sorosító nyelv, amit úgy terveztek, hogy közvetlenül is olvasható és írható legyen emberi szemmel.
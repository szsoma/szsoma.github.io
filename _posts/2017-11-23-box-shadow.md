---
layout: post
title: Mi a franc az a spread?
tags:
  - frontend
  - ui
  - codepen
hero: https://images.techhive.com/images/article/2017/03/middle-earth-shadow-of-war-100712835-large.jpg
overlay: red
published: true
---
Ezt rejtegette előlem a box-shadow...
{: .lead}
<!--break-->

Sajnálatos módon - ciki vagy nem - még csak most jöttem rá mennyire király a spread[^1] ha box-shadow-t használunk. Ezt a 4. tulajdonságot Codepenen próbálgattam tegnap. (Lent be is lesz illesztve!)

## Kiterjedés
Valahogy így lehetne szabadfordítani ezt a funkciót. Megtalálható Photoshopban, Sketchben meg mindenféle szerkesztő programban a Drop Shadow layer style-ban. (Az Inner Shadowban choke van!)

![800x400](https://soma.shoprenter.hu/custom/soma/image/data/2017/spread-ps.png "ps drop shadow")

Mit akar ez jelenteni?
A spreaddel megadhatjuk, hogy hol kezdődjön az árnyék elhalványulása. Magyarul egy plusz ráhagyás. Nézzünk egy példát rá CSSben, ahol rendre ezeket jelentik a megadott értékek. 

~~~CSS
box-shadow: 0px 5px 20px 20px blue;
~~~

1. X offset érték
2. Y offset érték
3. Blur mértéke
4. Spread mértéke
5. Szín, átlátszóság

Ha a spread = 20px akkor az azt jelenti, hogy az árnyékot 10pixellell kiterjesztjük és a 20px-es blur csak ezután fog következni.

![800x400](https://soma.shoprenter.hu/custom/soma/image/data/2017/spread.gif "spread")

Ezért aztán felmerült bennem a kérdés, hogy inkább egy "plusz méret" opcióként kellene felfogni a spreadet. Ugyanis használhatjuk erre is, ha a box shadowban csak spread értéket adunk meg.

![800x400](https://soma.shoprenter.hu/custom/soma/image/data/2017/spread-size.gif "spread")

Megadhatunk negatív értéket is CSSsel. A képszerkesztő programokban viszont nem. (sajnos) Ezzel az eredeti árnyékunk méretét csökkenthetjük.
### Miért jó ez nekünk?
Azért, mert a méretekkel játszva jól érzékeltethetjük a térbeli mozgásokat. Ez nagyon hasznos tud lenni pl. material designhoz, hiszen nagyon élethű árnyékokat készíthetünk hoverre.

![800x400](https://soma.shoprenter.hu/custom/soma/image/data/2017/spread-negative.gif "spread")

Egy másik trükkös felhasználási módja lehet szaggatott vonalas munkáknál, ha ezt beljebb szeretnénk kicsit kezdeni.

~~~CSS
.coupon
  background: LightSeaGreen
  border: 1px dashed white
  box-shadow: 0px 0px 0px 4px LightSeaGreen
~~~

Ez csak néhány ötlet volt, hogy miket lehet csinálni egy kis fantáziával. Kísérletezzetek és nézzétek meg a pent is! 👨‍💻

## A végeredmény:
<p data-height="530" data-theme-id="30084" data-slug-hash="Bmxjpj" data-default-tab="result" data-user="szsoma" data-embed-version="2" data-pen-title="Box shadow  playground" class="codepen">See the Pen <a href="https://codepen.io/szsoma/pen/Bmxjpj/">Box shadow  playground</a> by Soma Szoboszlai (<a href="https://codepen.io/szsoma">@szsoma</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

<br>


	

[^1]: This is a fourth length value. Positive values will cause the shadow to expand and grow bigger, negative values will cause the shadow to shrink. If not specified, it will be 0 (the shadow will be the same size as the element).
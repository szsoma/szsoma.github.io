---
layout: post
title: Spin 2 Win!
tags:
  - frontend
  - design
  - animation
  - svg
  - codepen
hero: https://soma.shoprenter.hu/custom/soma/image/data/codepen.JPG
overlay: red
published: true
---

Szerencse kerék pörgetős demó SVG-vel és Greensock JS-sel. Továbbá, hogy lehet ennyire menő dolgot csinálni, mint a Codepen?? 🤓
{:.lead}
<!--break-->

## Codepen
Amikor elkezdi az embergyerek tanulni ezt a kiváló front-end szakmát, akkor először is szétnéz a YouTube-on. Esetleg valamilyen akciós Udemy-s kurzust megvásárol és nekikezd a rögös útnak.
Ezekben a kurzusokban a legtöbbször saját gépen dolgoznak a készítők, így mi is. Felcsapjuk kedvenc text editorunkat, mint pl. a <a href="https://code.visualstudio.com/" target="_blank">VS Codeot, </a> <a href="https://atom.io/" target="_blank">Atomot</a> vagy a <a href="https://www.sublimetext.com/" target="_blank">Sublime Textet</a> és mehet a menet. 

Azonban, ha elszaporodtak az apróbb projektjeink, kísérleteink és már 23923718 db mappát csináltunk nekik, akkor el lehet gondolkozni a<a href="https://codepen.io/" target="_blank"> Codepen</a>-en. 
A Codepen 2012 óta létezik, és egy olyan online közösség, ahol az emberek megírhatják kisebb projektjeiket (ők pennek hívják). Ezeket rendszerezhetjük, megoszthatjuk, mint portfóliót vagy épp beágyazhatjuk a blogunkba mint ahogy én is szoktam. Az online editorban HTML, CSS és JavaScript kódokkal dolgozhatunk a különböző füleken és a készterméket is látjuk. Nagyon klassz platform, ha valaki inspirálódni és tanulni szeretne. Ha tanár lennék, verném a gyerekeket, hogy használják tanuláshoz. (dehogy...ez family frendly blog) <br>
Azt is szeretem benne, hogy ready-to-use, egyszerűen csak kiválasztjuk milyen JS pluginnal (esetleg CSS keretrendszerrel, preprocessor-ral) szeretnénk dolgozni és lehet is kódolni. Nem kell headet, meg titlet írni, csak kezdeni in medias res.

Két full-stack developer (Alex Vazquez, Tim Sabat) és egy front-end designer Chris Coyier alapította. <a href="https://chriscoyier.net/" target="_blank">Chris Coyier</a> egy hatalmas figura, kiváló előadó és író. A Codepen mellett a <a href="https://css-tricks.com" target="_blank">CSS-tricks</a>-et is ő hozta létre. De amiért én különös módon szeretem a munkásságát az az, hogy elég jó SVG témakörben. Amikor az <a href="http://slides.com/szsoma/svg-svg-animationon-the-web-1" target="_blank">SVG előadásomra</a> készültem sok cikket és előadását megnéztem tőle. Na de elég ebből, térjünk a lényegre! 👆

## Lucky Wheel
A webes animációk az új kedvenc témaköröm. Ezek nem nagy projektek, ha eszembe jut valami csak felugrok Codepenre és nekilátok valaminek. Általában Greensock JS-sel csinálok animációkat, ami az SVG-vel nagyon jó barátok. De erről majd később.

Szóval pénteken hazatekertem munkából és leültem megcsinálni valamit, ami nagyon piszkálta a fantáziámat. Ez pedig egy szerencsekerék. A grafika Illustratorban készült, semmi nagy dologra nem kell gondolni, néhány vektoros alakzat az egész. Utána neki álltam megtervezni magát a mozgást Greensock JS-sel. A kerék egy folyamatosan lassuló mozgással forog a nyeremény jelölő pedig egy gyors oda-vissza mozdulatot tesz. TransformOrigin kb a szürke pont.

<p data-height="591" data-theme-id="30084" data-slug-hash="bYEXGx" data-default-tab="result" data-user="szsoma" data-embed-version="2" data-pen-title="luckywheel" class="codepen">See the Pen <a href="https://codepen.io/szsoma/pen/bYEXGx/">luckywheel</a> by Soma Szoboszlai (<a href="https://codepen.io/szsoma">@szsoma</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

### A nyeremény jelölő pöcök már érdekesebb
Itt az volt a cél, hogy a 12 részre osztott kör minden pálcikájánál biccentsen egyet. 
Tehát a pozícióját is így kell megválasztani, én a 2. pálcikához (60 fokhoz) tettem. Nem tökéletes, de elfogadható a szem számára.
### Hogy lett ez megoldva? Rafináltan.
Először is a tween(mozgás) kódjába bekerült egy onUpdate tulajdonság. Ez azt jelenti, hogy az onUpdate: utáni függvény valamit csinálni fog a kerék framenkénti mozgásának következtében. Fú, ez bonyolult. :)
Egészen pontosan ez a mágikus kódrészlet:

~~~JS
    function(){    
      currentRotation = Math.round(this.target[0]._gsTransform.rotation);
      tolerance = currentRotation - lastRotation;

      if(Math.round(currentRotation) % (360/12) <= tolerance){
        if(indicator.progress() > .3 || indicator.progress() === 0){
          indicator.play(0);
        }
      }
      lastRotation = currentRotation;
    }
~~~

Ami itt történik, az röviden annyi, hogy számolunk egy tolerance-t a pillanatyi forgásból és az utolsó forgásból. Ha gyorsan pörög a kerék akkor magas ez a változó, ha lassul az ease-ing miatt, akkor elkezd csökkenni.

Mit jelent ez? A gyors pörgésnél mindig 30%-os progress után kezdi újra a biccentést a kis pöckünk (indicator.progress() > .3). Vissza se áll az eredeti helyére már kezdi előlről. Ez tolerance = 5-ig van. Az ennél lasabb forgásnál már csak a 360/12=30 fokonként fog biccenteni.

## Színezés
A CSS SASS előfeldolgozóval készült, így könnyen meg lehetett oldani a színezést változókkal. <br>
A keret, középpont, és a nyereményjelölő egyszerű volt: a változókban lévő színeket az SVG class színezésére használom:

~~~CSS
.frame, .sticks {
  fill: $frameColor;
}
~~~

A szerencsekerék 12 szeletéhez egy egyszerű listát csináltam, amiben eltároltam a 12 színt:

~~~CSS
$colors: 
  #ba4d4e     //sector 1 color
  #1592e8     //sector 2 color
  #14c187     //sector 3 color
  #fc7800     //sector 4 color
  #14c187     //sector 5 color
  #1592e8     //sector 6 color
  #ba4d4e     //sector 7 color
  #1592e8     //sector 8 color
  #14c187     //sector 9 color
  #fc7800     //sector 10 color
  #14c187     //sector 11 color
  #1592e8;    //sector 12 color
~~~

A színbeállításhoz egy mixint és egy ciklust írtam. A mixin kap egy sorszámot és nem tesz mást, mint a fill tulajdonságnak beállítja a lista $n-edik színkódját. Az ezután következő for ciklus pedig ezt a mixint haszánlja a 12 körcikk színezésére:

~~~CSS
@mixin setColor($n){
  fill: nth($colors, $n);
}

@for $i from 1 through 12 {
  #_#{$i} {
    @include setColor($i);
  }
}
~~~

Így aztán elég csak ezeket a változókat átírni ha egyedi szerencsekereket akarunk magunknak.

## Teljesítmény
Az animáció 60FPS-t produkál, ez látszik a 17ms/frame körüli render időből.

![800x600](https://soma.shoprenter.hu/custom/soma/image/data/luckywheel-perf.JPG "performance")

A CPU 6 szoros lassításával én 30FPS-t kaptam betöltődésnél, második pörgetésre pedig már 60-at.

![800x600](https://soma.shoprenter.hu/custom/soma/image/data/luckywheel-perf-6x.JPG "performance 6x slowdown")

Még tovább fogom fejleszteni a kis szerencse kerekemet, mert nem tökéletes. Használjátok ti is a Codepent, főleg most #codevember-ben!
---
layout: post
title: UX és a webes animációk
tags:
  - blog
  - design
  - ux
  - animation
hero: https://i.pinimg.com/564x/b9/b5/8d/b9b58da6a098bf61fc72ccd613a5666b--barter-animation.jpg
overlay: purple
published: true
---

### Elvonja a figyelmet vagy vezeti a tekintetet?
Kalandozásomat a animációk világába nem is kezdhettem volna mással, mint a User Experience vizsgálatával. Van-e létjogosultsága az animációknak egy weboldalon?
{:.lead}
<!--break-->

> Attól függ…

És itt be is fejezhetném az elmélkedést. :) Na de menjünk ebbe bele kicsit.

Az agyunkat arra kódolta az evolúció, hogy észlelje a mozgást és minél gyorsabban reagáljon rá. Ezért képes egy animáció bevonzani a tekintetet, akkor is, amikor semmi más nem tudja. Tehát egy jó animációval képesek vagyunk a user figyelmét újból felkelteni vagy esetleg tovább vezetni valami fontos dologra. Viszont ha rosszul van időzítve vagy rossz helyen van akkor egy fontos dologról (pl. CTA gomb) vonhatja el a figyelmet. Hogy is működik ez?

Ha böngészünk egy weboldalon, akkor egy térképet készítünk magunkba az ott található információkról. Egy animációval át tudjuk formálni ezt a térképet, összpontosítani tudjuk a figyelmet egy fontos pontra. Viszont ha az animációnk nincs jól megírva (általában JS), akkor belassítja vagy meg is ölheti az oldalt és oda minden szorgalmasan összeszedett jó User Experience-ünk.

## Hol működnek a legjobban?

Ha egy weboldalra tévedünk akkor azonnal elkezdjük feldolgozni az oldalt. Keressük a kis információ morzsákat: megnézzük a képeket, elolvassuk a nagy, vastag betűvel írt címeket, stb. Előfordulnak olyan helyzetek, hogy valamiért több időre van szükségünk, hogy betöltsünk egy oldalt vagy alkalmazást. Az azonnali információéhséget például el lehet fedni egy jó loaderrel. Az animációkban elég sok információt lehet elrejteni még akkor is ha csak egy rövid ismétlődő mozgást nézünk.
Itt van egy példa:
![800x400](https://soma.shoprenter.hu/custom/soma/image/data/om-loading.gif "Optimonk loader"){:.lead}
### Bennem ezek a kérdések vetődnek fel:
>Mozog a kis Monk is vagy csak a szöveg? Hogyan mozog a szöveg? Mi a rendszer benne?

Mire megválaszolja a user betöltöttünk neki az alkalmazásunkat, és már fogyaszthatja is a jól megérdemelt tartalmát. Egy kutatás szerint az emberek sokkal tovább hajlandóak várni egy betöltődésre akkor, ha egyedi loading animációt használ az oldal vagy app.

Ha például egy applikációnk van akkor használhatunk progresszív tartalom megjelenítést is. Ezt elkészíthetjük div-ekkel vagy épp SVG-vel is úgy, hogy ahol szöveges tartalmat akarunk betölteni ott kicsíkozzuk a tartalmat és egy finom pulzáló színváltó animálást is tehetünk rá.
![800x400](https://soma.shoprenter.hu/custom/soma/image/data/1-3-4h8EC6DnTPlpNQnww_vA.gif "progressive content"){:.lead}

A Slack és a Facebook is sikeresen alkalmazza ezt a technikát. Amíg be nem töltünk mindent a user-ünket leköti, hogy megértse a különböző alakzatokat és a pulzálást. Ezzel időt nyerhetünk és mindenki boldog lesz.

Egy másik példában egy megértést könnyítő funkciót mutatok. Ezt szintén az egyik termékünkhöz készítettük és Landing page-eken használunk hasonlókat a különböző funkciók bemutatásánál. Én inkább annak a híve vagyok, hogy elég egyszer lejátszani, és meg kell hagyni a usernek, hogyha szeretné kattintásra újból megnézheti. Így letisztultabb lesz a blokk, és nem vonja el a figyelmet a fontosabb szövegről.

![800x400](https://soma.shoprenter.hu/custom/soma/image/data/1-ZphBYfXEcpBI8THilv9lvg.gif "progressive content"){:.lead}

Egy időben UI animációkat is akartunk készíteni az egyedi projektjeinkhez, viszont ezt evetettük időhiány miatt. Mindenesetre egy hasonló animáció jelentősen tudná növelni egy olyan ügyfelünk elégedettségét, aki mondjuk semmit nem ért a szakmához és nem tudja elképzelni, a mozgásokat az új webáruházában.

Ezeken kívül rengeteg más lehetőségünk van még ahol használni tudjuk az animációk adta lehetőségeket. Ezeket sorra ki is akarom tárgyalni a jövőben, mert le vannak gyártva élesben az SVG előadásomhoz.

Szóval úgy gondolom, hogy ha nem esünk túlzásokba az animációk terén akkor fel tudják dobni az oldalunkat, segíteni tudnak fontos információk átadásában, jobb megértésében. Ehhez viszont szükséges, hogy amennyire csak lehet próbáljuk mellőzni a méretes gif file-okat és használjunk SVG- grafikákat CSS-sel vagy JS-sel animálva.
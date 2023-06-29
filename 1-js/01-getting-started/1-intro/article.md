# Een introductie naar JavaScript

Laten we zien wat is zo bijzonder over JavaScript, wat kunnen we ermee bereiken, en welke andere technologieën speel er lekker mee.

## Wat is JavaScript?

Oorspronkelijk was *JavaScript* gemaakt om "webpagina's levend te maken".

De programma's in deze taal heten *scripts*. Ze kunnen direct in een HTML van een webpagina worden geschreven en worden automatisch uitgevoerd wanneer de pagina wordt geladen.

Scripts worden geschreven en uitgevoerd als platte tekst. Ze hebben geen speciale voorbereiding of compilatie nodig om te worden uitgevoerd.

In dit opzicht is JavaScript heel anders van een andere taal genaamd [Java](https://nl.wikipedia.org/wiki/Java_(programmeertaal)).

```smart header="Waarom heet het <u>Java</u>Script?"
Toen JavaScript werd gemaakt, had het een andere naam: "LiveScript". Maar Java was erg populair in die tijd, dus er besloten werd dat het positioneren van een nieuwe taal als een "jongere broer" van Java zou helpen.

Maar naarmate het evolueerde, werd JavaScript een volledig onafhankelijke taal met zijn eigen specificatie genaamd [ECMAScript](https://nl.wikipedia.org/wiki/ECMAScript), en nu heeft het helemaal geen relatie met Java.
```

Tegenwoordig kan JavaScript niet alleen in de browser uitgevoerd worden, maar ook op de server of eigenlijk op elk apparat met een speciale programma genaamd [de JavaScript-engine](https://en.wikipedia.org/wiki/JavaScript_engine).

De browser heeft een ingebouwde engine die ook wel een "JavaScript virtuele machine" wordt genoemd.

Verschillende engines hebben verschillende "codenamen". Bijvoorbeeld:

- [V8](https://en.wikipedia.org/wiki/V8_(JavaScript_engine)) -- in Chrome en Opera.
- [SpiderMonkey](https://en.wikipedia.org/wiki/SpiderMonkey) -- in Firefox.
- …Er zijn andere codenamen zoals "Chakra" voor IE, "ChakraCore" voor Microsoft Edge, "Nitro" en "SquirrelFish" voor Safari, enz.

De bovenstaande uitdrukkingen zijn goed om te onthouden omdat ze worden gebruikt in ontwikelaarsartikelen op internet. We zullen ze ook gebruiken. Bijvoorbeeld, als "een functie wordt ondersteund door V8", dan werkt het waarschijnlijk in Chrome en Opera.

```smart header="Hoe werken engines?"

Engines zijn ingewikkeld. Maar de basis is eenvoudig.

1. De engine (ingebouwd als het een browser is) leest ("ontleeds") het script.
2. Dan converteert ("compileert") hij het script naar de machinetaal. 
3. En dan wordt de machinecode uitgevoerd, behoorlijk snel.

De engine past optimalisaties toe bij elke stap van het proces. Hij bekijkt zelfs het gecompileerde script terwijl het uitgevoerd wordt, analyseert de gegevens die erdoorheen stromen, en optimaliseert de machinecode verderop basis van die kennis.
```

## Wat kan in-browser JavaScript?

Modern JavaScript is een "veilige" programmerstaal. Het biedt geen toegang op laag niveau tot geheugen of CPU, omdat het oorspronkelijk is gemaakt voor browsers die dit niet nodig hebben.

De mogelijkheden van JavaScript zijn sterk afhankelijk van de omgeving waarin het wordt uitgevoerd. [Node.js](https://nl.wikipedia.org/wiki/Node.js) ondersteunt bijvoorbeeld functies waarmee JavaScript willekeurige bestanden kan lezen/schrijven, netwerkverzoeken kan uitvoeren, enz.

In-browser JavaScript kan alles wat te maken heeft met het manipuleren van webpagina's, interactie met de gebruiker en de webserver.

In-browser JavaScipt kan bijvoorbeeld:

- Nieuwe HTML aan de pagina toevoegen, de bestaande inhoud wijzigen, stijlen veranderen.
- Reageren op de gebruikersacties, uitgevoerd worden op muisklikken, aanwijzerbewegingen, toetsaanslagen.
- Verzoeken versturen via het netwerk naar externe servers, bestanden downloaden en uploaden (zogenaamde [AJAX](https://nl.wikipedia.org/wiki/Asynchronous_JavaScript_and_XML) en [Comet](https://nl.wikipedia.org/wiki/Comet_(internet))).
- Cookies ophalen en instellen, vragen stellen aan de bezoeker, berichten tonen.
- Data aan de clientzijde onthouden ("lokale opslag").

## Wat kan in-browser JavaScript NIET?

De mogelijkheden van JavaScript in de browser zijn beperkt omwille van de veiligheid van de gebruiker. Het doel is om te voorkomen dat een kwaadaardige webpagina toegang krijgt tot privé-informatie of de gegevens van de gebruiker schaadt.

Voorbeelden van dergelijke beperkingen zijn:

- JavaScript op een webpagina mag geen willekeurige bestanden op de harde schijf lezen/schrijven, kopiëren of programma's uitvoeren. Het heeft geen directe toegang tot OS-functies.

    Moderne browsers staan het toe om met bestanden te werken, maar de toegang is beperkt en wordt alleen geboden als de gebruiker bepaalde acties uitvoert, zoals een bestaand "droppen" in een browservenster of het selecteren via een `<input>`-tag.

    Er zijn manieren om met de camera/microfoon en andere apparaten te communiceren, maar hiervoor is de uitdrukkelijke toestemming van de gebruiker vereist. Een pagina met JavaScript mag dus niet de camera stiekem inschakelen, de omgeving observeren en de informatie naar de [NSA](https://nl.wikipedia.org/wiki/National_Security_Agency) sturen.
- Verschillende tabbladden/vensters weten over het algemeen niets van elkaar af. Soms wel, bijvoorbeeld wanneer het ene venster JavaScript gebruikt om het andere te openen. Maar zelfs in dit geval heeft JavaScript van de ene pagina mogelijk geen toegang tot de andere als ze van verschillende sites komen (van een ander domein, ander protocol of poort).

    Dit wordt de "Same Origin Policy" (hetzelfde oorsprongbeleid) genoemd. Om dat te omzeilen moeten *beide pagina's* overeenkomen voor gegevensuitwisseling en speciale JavaScript-code bevatten die het afhandelt. Dat behandelen we in de tutorial.

    Deze beperking is, nogmaals, voor de veiligheid van de gebruiker. Een pagina van `http://anysite.com` die een gebruiker heeft geopend, mag geen toegang hebben tot een ander browsertabblad met de URL `http://gmail.com` en daar informatie stelen.
- JavaScript kan gemakkelijk via het net communiceren met de server waar de huidige pagina vandaan komt. Maar zijn vaardigheid om gegevens van andere sites/domeinen te ontvangen is beperkt. Hoewel mogelijk, vereist het een expliciete toestemming (uitgedrukt in HTTP-koppen) van de externe kant. Nogmaals, dat is een veiligheidsbeperking.

![](limitations.svg)

Dergelijke beperkingen bestaan niet als JavaScript buiten de browser wordt gebruikt, bijvoorbeeld op een server. Moderne browsers staan ook plug-ins/extensies toe die om uitgebreide machtigingen kunnen vragen.

## What makes JavaScript unique?

There are at least *three* great things about JavaScript:

```compare
+ Full integration with HTML/CSS.
+ Simple things are done simply.
+ Support by all major browsers and enabled by default.
```
JavaScript is the only browser technology that combines these three things.

That's what makes JavaScript unique. That's why it's the most widespread tool for creating browser interfaces.

That said, JavaScript also allows to create servers, mobile applications, etc.

## Languages "over" JavaScript

The syntax of JavaScript does not suit everyone's needs. Different people want different features.

That's to be expected, because projects and requirements are different for everyone.

So recently a plethora of new languages appeared, which are *transpiled* (converted) to JavaScript before they run in the browser.

Modern tools make the transpilation very fast and transparent, actually allowing developers to code in another language and auto-converting it "under the hood".

Examples of such languages:

- [CoffeeScript](http://coffeescript.org/) is a "syntactic sugar" for JavaScript. It introduces shorter syntax, allowing us to write clearer and more precise code. Usually, Ruby devs like it.
- [TypeScript](http://www.typescriptlang.org/) is concentrated on adding "strict data typing" to simplify the development and support of complex systems. It is developed by Microsoft.
- [Flow](http://flow.org/) also adds data typing, but in a different way. Developed by Facebook.
- [Dart](https://www.dartlang.org/) is a standalone language that has its own engine that runs in non-browser environments (like mobile apps), but also can be transpiled to JavaScript. Developed by Google.
- [Brython](https://brython.info/) is a Python transpiler to JavaScript that allow to write application in pure Python without JavaScript.

There are more. Of course, even if we use one of transpiled languages, we should also know JavaScript to really understand what we're doing.

## Summary

- JavaScript was initially created as a browser-only language, but is now used in many other environments as well.
- Today, JavaScript has a unique position as the most widely-adopted browser language with full integration with HTML/CSS.
- There are many languages that get "transpiled" to JavaScript and provide certain features. It is recommended to take a look at them, at least briefly, after mastering JavaScript.

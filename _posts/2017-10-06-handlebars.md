---
date: '2017-10-06 09:02 +0200'
published: true
title: Handlebars
---
Handlebars är en kraftfull mall (eng: templating) motor som är enkel att använda. Handlebars innehåller:

* Templates

Det är baserat på Mustasch mallens språk, men förbättrar den på flera viktiga sätt. Med Handlebars kan du skilja din HTML markup från din JavaScript och skriva renare kod.

Det rekommenderade sättet att lägga till mallar på din sida är att inkludera dem i `<script>` taggar med en speciell typ.Typattributet är viktigt, annars webbläsaren att försöka analysera dem som vanliga JavaScript's.

Mallarna har en lättfattlig syntax. De kan innehålla HTML och text, blandade med Handlebars uttryck.

Uttryckningar är inslagna i dubbel- eller trippelklamrar `{{}}`. Uttryck talar om för Handlebars att inkludera värden i variabler eller för att utföra funktioner i så kallade Helper functions.

---

## Templates

Mallar måste sammanställas till en JavaScript-funktion före användning. Du kan se ett exempel nedan:

**html**
```hb
<script id="template" type="text/x-handlebars-template">Mitt namn är {{name}}</script>

/*Det nya innehållet kommer att placeras här*/
<div class="content-placeholder"></div>
```

**JS**
```js
// hämta innehållet i vår mall
var templateScript = document.getElementById('template').innerHTML;

// Kompilera mallen
var template = Handlebars.compile(templateScript);

// Definera vårt data objekt
var context={
  "name": "Ray"
            };

// Skicka data:n till vår mall
var theCompiledHtml = template(context);

// Skicka in vår compilerade html markup till dokumentet
document.getElementById('placeholder').innerHTML = theCompiledHtml
```

---

## Expressions

För att bygga upp från det föregående exemplet kommer all eventuella data som du skriver ut i ett {{}} uttryck, automatiskt att hämta behandlad HTML markup.

Det här är en bra säkerhetsfunktion, men ibland kanske du vill skriva ut rå HTML. I det här fallet kommer du att använda trippelklamers uttryck {{{}}}.

Observera också att Handlebars uttryck stödjer nästlade värden som gör att vi enkelt kan komma åt data från vilket  JavaScript objekt som helst.

**HTML**
```html
<script id="template" type="text/x-handlebars-template">
    \\{{description.escaped}}
    {{example}}
    <br><br>
    {{description.unescaped}}
    {{{example}}}
</script>

<!--Your new content will be displayed in here-->
<div id="placeholder"></div>
```

**JS**
```js
// Grab the template script
var templateScript = document.getElementById('template').innerHTML

// Kompilera mallen
var template = Handlebars.compile(templateScript);

// Define our data object
var context={
    "description": {
      "escaped": "Using {{}} brackets will result in escaped HTML:",
      "unescaped": "Using {{{}}} will leave the context as it is:"
    },
    "example": "<button> Hello </button>"
  };

// Pass our data to the template
var theCompiledHtml = template(context);

// Add the compiled html to the page
document.getElementById('placeholder').innerHTML = theCompiledHtml
```
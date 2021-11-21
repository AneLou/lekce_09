# HTML a CSS 1: lekce 9

Podzim 2021, online

<small>22. listopadu 2021</small>

---

# CSS selektory, pseudotřídy, pseudoelementy a specificita

---

# Dnešní cvičení

https://github.com/Czechitas-Liberec-HTML-CSS-2021-DK/lekce_09

---

# Dnešní témata

- Možnosti připojení CSS do stránky
- CSS selektory – základní a pokročilejší
- CSS pseudotřídy a pseudoelementy
- Pravidla CSS specificity

---

# Způsoby připojení CSS

1. Externí soubor (tag  `<link>`)
2. Přímo v HTML (značka  `<style>`)
3. Inline styly
4. (Pomocí jazyka JavaScript)

---

## Způsoby připojení CSS - externí soubor

- Externí soubor nebo více souborů CSS pomocí tagu `<link>`
- Nejpoužívanější

   ```html
   <link rel="stylesheet" href="/styles/typography.css" />
   <link rel="stylesheet" href="/styles/contact.css" />
   ```

---

## Způsoby připojení CSS - přímo v HTML

- Přímo v HTML prostřednictvím značky `<style>`
- Spíše zastaralý způsob

   ```html
   <style>
     /* CSS komentář */
     body {
       max-width: 1600px;
     }

     p {
       margin-bottom: 1rem;
     }
   </style>
   ```

---

## Způsoby připojení CSS - inline styly

- Přímo do otvírací značky HTML elementu pomocí atributu style
- Pokud není možnost zasáhnout do kódu jinak
- Vždy přepisují externí styly!
- Nejde použít stavové styly např. pro `:hover` a `:focus`

   ```html
   <p style="max-width: 20rem; color: silver;">
     Text odstavce s maximální šířkou 20 rem a šedou barvou písma.
   </p>
   ```

---

## Způsoby připojení CSS - JavaScript

- Pouze pro úplnost
- Nejde použít stavové styly např. pro `:hover` a `:focus`

---

# Selektory

Existuje více jak 30 různých CSS selektorů a nespočet dalších možností, jak je kombinovat.

note:

- https://code.tutsplus.com/tutorials/the-30-css-selectors-you-must-memorize--net-16048

---

## Typový selektor

- Vybere všechny elementy daného typu
- Prostý název HTML tagu (v CSS bez špičatých závorek!)

```css
/* odstavce vypiš tučně */

p {
  font-weight: bold;
}
```

---

## Třídy

- Název třídy (začíná tečkou, aby se odlišil od názvu prvku):

```css
/* prvky s třídou .perex vypiš kurzívou */

.perex {
  font-style: italic;
}
```

note:

- 1 třídu může mít více prvků, bez ohledu na jejich typ
- 1 prvek může mít více tříd, na pořadí tříd v HTML nezáleží

---

## Identifikátory

- ID může mít jen 1 prvek na stránce – příliš vysoká _specificita_
- Nepoužíváme!

```css
/* Tohle nedělejte! */
#navbar {
  background-color: #000;
}
```

---

## Několikanásobný selektor

- Stejná pravidla se přiřadí více prvkům naráz!

```css
/* nadpisy 1.‒4 úrovně vypiš karmínovou */

h1,
h2,
h3,
h4 {
  color: crimson;
}
```

---

## Kontextový selektor

- Vyjadřuje strukturu HTML
- Odstavce, které jsou uvnitř patičky:

```css
footer p {
  color: white;
}
```

---

## Přímý potomek

```css
/* odkazy uvnitř prvků s třídou .perex, které jsou jeho přímým potomkem vypiš kaštanovou */

.perex > a {
  color: maroon;
}
```

```html
<div class="perex">
  <p>Text odstavce <a href="#">odkaz na zajímavý zdroj</a>, další text</p>
  <a href="#">odkaz na celý článek</a
  ><!-- tento odkaz bude kaštanovou barvou, předchozí odkaz ne -->
</div>
```

---

## Vícenásobné třídy
- Umožní nám přesnější zacílení
- Používat s rozumem, pokud nás prosazení pravidla nutí řadit více než 3 třídy, bude vhodnější přidat třídu novou

```css
/* .perex, který má současně třídu .main vykresli se slonovinovým pozadím */

.perex.main {
  background-color: ivory;
}
```

Předchozí zápis podbarví tento prvek:

```html
<p class="perex main">Úvodní odstavec nějakého článku…</p>
```

---

## Atributy

- Prvky s konkrétním atributem nebo hodnotou atributu


```css
/* prvkům s atributem `alt` přidej spodní ohraničení */
[alt] {
  border: 1px solid silver;
}
```

```css
/* prvky s prázdným atributem `alt` orámuj karmínově */
[alt=""] {
  border-color: crimson;
}
```

---

# Pseudotřídy

- Určují stav prvku
- Podle chování uživatele nebo podle struktury HTML

`:hover`, `:focus`, `:first-child`, `:last-child`, `:nth-child()`, `:nth-of-type()`, ...

---

## Pseudotřídy - `:first-child`, `:last-child`

```css
/* První potomek elementu */
div:first-child {}

/* Poslední potomek elementu */
div:last-child {}
```

---

## Pseudotřídy - `:nth-child`

```css
/* pravidlo platí pro druhou položku seznamu */
li:nth-child(2) {}

/* pravidlo platí pro každou třetí položku */
li:nth-child(3n) {}

/* jako předchozí, ale začíná se u druhé položky */
li:nth-child(3n + 2) {}
```

---

# Pseudoelementy

- `::first-line`, `::first-letter`
  - lze stylovat pouze font, styl textu, pozadí, margin, padding a border
- `::before`, `::after`
  - lze stylovat vše
- `::selection`
  - lze stylovat pouze color, background-color a pár dalších

---

# Pseudoelementy - `::before`, `::after`

```css
div::before {
  content: "Před";
}

div::after {
  content: "Za";
}
```

```htmlmixed
<div>
  Před
  <!-- Vše ostatní co bylo v divu předtím -->
  Za
</div>
```

---

# Pseudoelementy - `content`

- Co vše můžeme použít v `content`:

```css
div::before {
  content: "Text";
}

div::before {
  content: "url(/cesta/k/obrazek.jpg)";
}

/* Nic, pro obrázková pozadí*/
div::before {
  content: "";
}

div::before {
  content: "<h1>Toto nejde!</h1>";
}
```

---

## Univerzální selektor
- Vybere všechny elementy v dokumentu

```css
* {
  border: 1px solid red;
}
```

---

# Dědičnost

Dědičnost v CSS je způsob, jakým se dostávají hodnoty vlastností od rodičovských elementů k potomkům.

<small>Martin Michálek, [Vzhůru Dolů](https://www.vzhurudolu.cz/prirucka/css-dedicnost)</small>

---

# Kaskáda

**3 základní principy**:

1. Pořadí
2. Specificita
3. Důležitost

---

## Kaskáda - pořadí

- Pořadí rozhoduje a poslední vyhraje

```css
p {
  color: crimson;
}

p {
  color: cornflowerblue;
}
```
---

## Kaskáda - specificita

- Selektor s vyšší váhou (specifitou) vyhrává

```css
section p {
  color: crimson;
}

p {
  color: cornflowerblue;
}
```

note:

- čím konkrétněji je popsán prvek, tím má pravidlo vyšší váhu
- čím konkrétněji ~ čím vyšší specificita

---

# Specificita

- Hodnota, která vyjadřuje přesnost zacílení selektoru
- Pravidlo se vyšší specificitou se uplatní bez ohledu na pořadí v kódu
- Teprve střetnou-li se stejně „silná“ pravidla, vítězí to, které je ve stylopise později

---

# Specificita
- Má číselnou hodnotu (jde spočítat)
- [Specificity calculator](https://specificity.keegan.st)
- [Specificity with Fish](https://specifishity.com)

![image](https://user-images.githubusercontent.com/91323442/142771061-ea7e3cb1-8e15-4bd6-a96e-5ad27d27671b.png)
![image](https://user-images.githubusercontent.com/91323442/142771069-e5f96b77-90fe-4749-a9f9-5a858f5be122.png)

---

## Kaskáda - důležitost

- Pravidlo označené jako důležité, vyhraje vždy:

```css
p {
  font-size: 1rem !important;
}
```

note:

- atomový kufřík, když jiné možnosti selžou => snažte se nepoužívat
  - hrozí, že se uškvaříte v importantovém pekle

---

# 5. (poslední) povinný domácí úkol

- Zadaný v GitHub Classroom
https://classroom.github.com/a/3-KaYQCw
- Ukážeme si, co je třeba
- Odevzdat do předposlední lekce 6.12.


![Island](https://raw.githubusercontent.com/tvorimweb-2020-praha-podzim/du_06_island/master/zadani/vysledek-3-pc.jpg)

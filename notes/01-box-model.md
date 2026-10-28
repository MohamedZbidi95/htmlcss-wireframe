# Appunti – htmlcss-wireframe (le card)

Esercizio del prof: 22/09/2026 – repo `htmlcss-wireframe`
Lezioni del corso: L05 (HTML), L06 (CSS), L07 (Box Model), L08 (testo e colori)

Dove vedi **⚠️ ATTENZIONE** c'è un errore comune, e come si fa giusto.

---

## 1. Struttura base di una pagina

```html
<!DOCTYPE html>
<!-- dice al browser: questo è HTML5            -->
<html lang="it">
  <!-- lang = lingua della pagina: it, en, fr...   -->
  <head>
    <!-- informazioni sulla pagina, NON si vedono   -->
    <meta charset="UTF-8" />
    <!-- permette le lettere accentate              -->
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>La mia prima app</title>
    <!-- nome nella SCHEDA del browser -->
    <link rel="stylesheet" href="./css/style.css" />
    <!-- collega il file CSS       -->
  </head>
  <body>
    <!-- tutto quello che SI VEDE nella pagina      -->
  </body>
</html>
```

> ⚠️ **ATTENZIONE – lingua**
>
> ```html
> <html lang="en">
>   <!-- ❌ la pagina è in italiano -->
>   <html lang="it">
>     <!-- ✅ -->
>   </html>
> </html>
> ```

> ⚠️ **ATTENZIONE – title e h1 sono due cose diverse**
>
> ```html
> <title>Document</title>
> <!-- ❌ titolo di default, lasciato lì         -->
> <title>La mia prima app</title>
> <!-- ✅ nella SCHEDA del browser, in alto       -->
>
> <h1>LA MIA PRIMA APP</h1>
> <!-- nella PAGINA: il titolo grande             -->
> ```
>
> Il `title` sta nell'`head`, l'`h1` nel `body`: sono due elementi diversi.

> ⚠️ **ATTENZIONE – il collegamento al CSS**
> Senza questa riga nell'`head` il CSS viene ignorato del tutto:
>
> ```html
> <link rel="stylesheet" href="./css/style.css" />
> ```

---

## 2. Block e inline

```html
<div>A</div>
<!-- block: va a capo, prende tutta la larghezza     -->
<p>B</p>
<!-- block                                            -->
<h1>C</h1>
<!-- block                                            -->

<span>D</span>
<!-- inline: resta sulla stessa riga, come una parola -->
<img src="x.png" />
<!-- inline                                           -->
<a href="#">E</a>
<!-- inline                                           -->
```

Risultato:

```
A
B
C
D [immagine] E
```

Il browser guarda **il tipo di tag**, non la lunghezza del testo.

> ⚠️ **ATTENZIONE – due p non stanno sulla stessa riga**
>
> ```html
> <p>Primo</p>
> <p>Secondo</p>
> ```
>
> Anche se sono corti, non stanno affiancati: `p` è block, **va sempre a capo**, anche con una parola sola.

> ⚠️ **ATTENZIONE – i titoli sono block**
>
> ```html
> <img src="foto.png" />
> <h2>Pinco Pallo</h2>
> <!-- ❌ h2 è block: il nome va SOTTO la foto -->
>
> <img src="foto.png" />
> <span>Pinco Pallo</span>
> <!-- ✅ span è inline: il nome sta ACCANTO   -->
> ```
>
> Il nome deve essere grande e in grassetto? Lo fa il CSS, non il tag.
> **L'HTML decide la struttura, il CSS decide l'aspetto.**

> ⚠️ **ATTENZIONE – un block non va dentro un inline**
>
> ```html
> <span>
>   <p>ciao</p>
>   <!-- ❌ la scatola grande dentro quella piccola -->
> </span>
>
> <span>Pinco Pallo</span>
> <!-- ✅ uno dopo l'altro                         -->
> <p>ciao</p>
> ```

---

## 3. Tag semantici

Un tag semantico è un `div` **con un nome che dice cosa contiene**. Nel browser si vede **uguale** a un `div`: cambia solo il significato, per chi legge il codice, per Google e per gli screen reader.

```html
<header>...</header>
<!-- la parte in alto: titolo, logo, menu      -->
<nav>...</nav>
<!-- il menu con i link                          -->
<main>...</main>
<!-- il contenuto principale (uno per pagina)    -->
<section>...</section>
<!-- un capitolo: un titolo + il suo contenuto   -->
<article>...</article>
<!-- un pezzo autonomo: un post, una card        -->
<footer>...</footer>
<!-- la parte in basso: crediti, contatti        -->
<div>...</div>
<!-- scatola generica, quando nessun tag va bene -->
```

### Esempio pratico: il sito di una pizzeria

```
┌─────────────────────────────────────┐
│ header                              │
│   Pizzeria Da Mario                 │
│  ┌───────────────────────────────┐  │
│  │ nav                           │  │
│  │  Home | Menu | Contatti       │  │
│  └───────────────────────────────┘  │
├─────────────────────────────────────┤
│ main                                │
│  ┌───────────────────────────────┐  │
│  │ section: Le nostre pizze      │  │
│  │  ┌──────────┐  ┌──────────┐   │  │
│  │  │ article  │  │ article  │   │  │
│  │  │Margherita│  │ Diavola  │   │  │
│  │  └──────────┘  └──────────┘   │  │
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │ section: Dove siamo           │  │
│  └───────────────────────────────┘  │
├─────────────────────────────────────┤
│ footer                              │
│   © 2026 Pizzeria Da Mario          │
└─────────────────────────────────────┘
```

Lo stesso disegno, in codice:

```html
<header>
  <h1>Pizzeria Da Mario</h1>
  <nav>
    <a href="#">Home</a>
    <a href="#">Menu</a>
    <a href="#">Contatti</a>
  </nav>
</header>

<main>
  <section>
    <h2>Le nostre pizze</h2>
    <article>
      <h3>Margherita</h3>
      <p>Pomodoro e mozzarella.</p>
    </article>
    <article>
      <h3>Diavola</h3>
      <p>Salame piccante.</p>
    </article>
  </section>

  <section>
    <h2>Dove siamo</h2>
    <p>Via Roma 10, Torino.</p>
  </section>
</main>

<footer>
  <p>© 2026 Pizzeria Da Mario</p>
</footer>
```

Come scegliere il tag:

```
Esiste un tag che descrive il contenuto?
        │
   ┌────┴────┐
   SÌ        NO
   │         │
usa quello   usa <div>
```

> ⚠️ **ATTENZIONE – nav è solo per i menu**
>
> ```html
> <nav>
>   <!-- ❌ dentro ci sono un titolo e una tabella, non link -->
>   <h2>Order Details</h2>
>   <table>
>     ...
>   </table>
> </nav>
>
> <section>
>   <!-- ✅ un titolo + il suo contenuto = section            -->
>   <h2>Order Details</h2>
>   <table>
>     ...
>   </table>
> </section>
> ```

> ⚠️ **ATTENZIONE – scrittura dei tag**
>
> ```html
> <heder>
>   <fotter>
>     <!-- ❌ -->
>     <header>
>       <footer><!-- ✅ --></footer>
>     </header></fotter
>   ></heder
> >
> ```
>
> Un tag scritto male non funziona, e il browser non dà errore.

La struttura delle card:

```html
<header>
  <h1>LA MIA PRIMA APP</h1>
</header>
<main>
  <section>
    <div class="card">
      <img class="avatar" src="./PNG/utente.png" alt="Avatar" />
      <span>Pinco Pallo</span>
      <!-- inline: accanto all'immagine -->
      <p>Lorem ipsum...</p>
      <!-- block: va sotto               -->
    </div>
  </section>
</main>
<footer>
  <p>Made with ♥ by ...</p>
</footer>
```

---

## 4. Classi

Una classe è un'**etichetta**: tutti gli elementi con la stessa etichetta ricevono **gli stessi stili**.

```html
<div class="card">
  <!-- la scatola intera        -->
  <img class="avatar" src="..." />
  <!-- solo la foto piccola     -->
</div>
```

> ⚠️ **ATTENZIONE – stessa classe a due cose diverse**
>
> ```html
> <div class="card">
>   <img class="card" src="..." />
>   <!-- ❌ la foto riceve bordo, sfondo e padding della card -->
> </div>
>
> <div class="card">
>   <img class="avatar" src="..." />
>   <!-- ✅ un nome che dice cos'è                          -->
> </div>
> ```

> ⚠️ **ATTENZIONE – la classe sull'elemento sbagliato**
>
> ```html
> <div class="avatar">
>   <!-- ❌ la scatola si chiama avatar, la foto niente -->
>   <img src="..." />
>
>   <div class="card">
>     <!-- ✅ -->
>     <img class="avatar" src="..." />
>   </div>
> </div>
> ```

> ⚠️ **ATTENZIONE – nomi confusi**
>
> ```html
> <div class="block">
>   <!-- ❌ "block" è già un concetto CSS: confonde -->
>   <div class="card"><!-- ✅ il nome dice COSA è                      --></div>
> </div>
> ```

> ⚠️ **ATTENZIONE – scrittura**
>
> ```html
> <div calss="card">
>   <!-- ❌ il CSS non trova la card, e non dà errore -->
>   <div class="card"><!-- ✅ --></div>
> </div>
> ```

---

## 5. Sintassi CSS

```css
.card {
  color: red;
}
/*
.card        → selettore       chi colpire
color: red;  → dichiarazione   una riga
color        → proprietà       cosa cambiare
red          → valore          come cambiarlo
:            → "diventa"
;            → fine della riga
*/
```

```css
header {
} /* tag: SENZA punto          */
.card {
} /* classe: CON il punto      */
* {
} /* tutti gli elementi        */
```

> ⚠️ **ATTENZIONE – due punti, non punto e virgola**
>
> ```css
> background-color ; white;   /* ❌ il browser ignora tutta la riga */
> background-color: white;    /* ✅ */
> ```

> ⚠️ **ATTENZIONE – chiudere la graffa**
>
> ```css
> p {
>     font-size: 15px;
> footer {                    /* ❌ manca la } di p: si rompe anche il footer */
>     background-color: #2c3e50;
> }
>
> p {
>     font-size: 15px;
> }                           /* ✅ */
> footer {
>     background-color: #2c3e50;
> }
> ```
>
> Trucco: **quando scrivi `{`, scrivi subito anche `}`**. Poi torni in mezzo.

> ⚠️ **ATTENZIONE – la regola "non funziona", ma era giusta**
>
> ```css
> .card {
>   background-color: white;
>   color: black;
> }
> ```
>
> Sembra che il CSS non sia collegato, ma funziona: bianco e nero sono **uguali al default** del browser, quindi non si vede la differenza.
> Per controllare, usa un colore evidente: `background-color: red;`

---

## 6. CSS Reset

Va **in cima** al file, sempre.

```css
* {
  box-sizing: border-box; /* le misure contano tutta la scatola        */
  margin: 0; /* toglie gli spazi automatici del browser   */
  padding: 0;
}
```

Senza reset il browser aggiunge da solo spazi al `body` (8px), ai titoli e ai paragrafi. Per questo header e footer non toccavano i bordi dello schermo.

---

## 7. Box model

Ogni elemento è una scatola, come un quadro:

```
          margin (fuori, trasparente)
   ┌─────────────────────────────────┐
   │ border (la cornice)             │
   │   ┌─────────────────────────┐   │
   │   │ padding (dentro)        │   │
   │   │   ┌─────────────────┐   │   │
   │   │   │ contenuto       │   │   │
   │   │   └─────────────────┘   │   │
   │   └─────────────────────────┘   │
   └─────────────────────────────────┘
```

```css
.card {
  padding: 20px; /* spazio DENTRO: lo sfondo lo colora           */
  margin: 20px; /* spazio FUORI: trasparente, si vede la pagina */
  border: 1px solid #ddd; /* la cornice: spessore, tipo, colore           */
  border-radius: 10px; /* angoli arrotondati                           */
}
```

> ⚠️ **ATTENZIONE – il margin non riguarda il body**
> Il margin non è il margine della scatola madre (il body): il margin è lo spazio **fuori** dalla scatola, tra lei e le scatole **vicine**. ✅
>
> ```
> [card 1]
>           ← margin: spazio tra le due card
> [card 2]
> ```

> ⚠️ **ATTENZIONE – lo spessore del bordo vuole il numero**
>
> ```css
> border: px solid red; /* ❌ "px" da solo non è una misura */
> border: 1px solid red; /* ✅ */
> ```

Tipi di bordo:

```css
border: 2px solid black; /* ━━━━━━ continuo  */
border: 2px dashed black; /* ─ ─ ─  trattini  */
border: 2px dotted black; /* · · ·  puntini   */
```

`border` è la **proprietà**, `solid` è un **valore**. "Attributo" si usa solo nell'HTML (`class`, `src`, `href`).

### box-sizing

```css
.box {
  width: 200px;
  padding: 20px;
  border: 5px solid black;
}
/* content-box (default): larga 200 + 20 + 20 + 5 + 5 = 250px
   border-box (dal reset): larga 200px, tutto compreso         */
```

`border-box` = misuri la scatola **da fuori**, pareti comprese.

> ⚠️ **ATTENZIONE – border-box non è la pagina**
> `border-box` non è la pagina del browser: è un **modo di misurare ogni singola scatola**: da fuori, pareti comprese. ✅
>
> ```
> *                → A CHI lo applico: a tutti gli elementi
> border-box       → COSA applico: misura tutta la scatola
> ```

---

## 8. Larghezza e altezza

```css
.avatar {
  max-width: 80px; /* larga AL MASSIMO 80px                          */
  height: auto; /* l'altezza si adatta, l'immagine non si deforma */
}

.card {
  min-height: 150px; /* alta ALMENO 150px: se il testo è lungo, cresce */
}
```

```
height: 150px           min-height: 150px
┌────────────┐          ┌────────────┐
│ testo      │          │ testo      │
│ testo      │          │ testo      │
└────────────┘          │ testo      │ ← cresce
  testo ← esce          └────────────┘
```

`max` = tetto. `min` = pavimento.
Regola del prof: **non usare `height` se non è necessario**.

> ⚠️ **ATTENZIONE – min e max al contrario**
>
> ```css
> .card {
>   max-height: 150px;
> } /* ❌ tetto: il testo lungo ESCE dalla card */
> .card {
>   min-height: 150px;
> } /* ✅ pavimento: la card CRESCE             */
> ```

---

## 9. Selezionare con precisione

> ⚠️ **ATTENZIONE – il tag colpisce TUTTI**
>
> ```css
> img {
>   /* ❌ tutte le immagini della pagina diventano 80px,
>     max-width: 80px;           anche un logo o una foto grande aggiunti dopo */
> }
>
> .avatar {
>   /* ✅ solo le immagini con class="avatar"        */
>   max-width: 80px;
> }
> ```
>
> Lo stesso vale per `span { }`: colpisce **tutti** gli span. Più preciso: `.card span { }`.

---

## 10. Testo e colori

```css
body {
  background-color: #f2f2f2; /* colore di sfondo                  */
  color: #333; /* colore del testo                  */
  font-family: arial, sans-serif; /* tipo di carattere, con la riserva */
}

header {
  text-align: center; /* testo al centro                   */
  font-size: 25px; /* grandezza del testo               */
}

span {
  font-weight: bold; /* spessore del tratto: grassetto    */
}
```

```
font-size    → quanto è GRANDE la lettera
font-weight  → quanto è SPESSO il tratto
font-family  → che TIPO di carattere
```

`#f2f2f2` è un colore scritto in **HEX** (esadecimale).

> ⚠️ **ATTENZIONE – il nome della proprietà**
>
> ```css
> font: arial; /* ❌ proprietà sbagliata: riga ignorata */
> font-family: arial, sans-serif; /* ✅ con la riserva dopo la virgola    */
> ```

> ⚠️ **ATTENZIONE – l'unità di misura**
>
> ```css
> font-size: 20x; /* ❌ manca la p: riga ignorata */
> font-size: 20px; /* ✅ */
> ```

```html
<strong>importante</strong>
<!-- HTML: grassetto con SIGNIFICATO (importante) -->
<b>grassetto</b>
<!-- HTML: grassetto senza significato            -->
```

```css
font-weight: bold; /* CSS: grassetto solo per ESTETICA              */
```

---

## 11. Ereditarietà

Le proprietà **del testo** passano dal genitore ai figli.

```css
body {
  font-family:
    arial, sans-serif; /* la ricevono TUTTI gli elementi della pagina */
}
```

```
Si ereditano:      color, font-size, font-family, font-weight, text-align
NON si ereditano:  padding, margin, border, background-color
```

Se il figlio ha la sua regola, vince quella del figlio:

```css
body {
  color: white;
}
.card {
  color: black;
} /* il testo nella card è nero */
```

> ⚠️ **ATTENZIONE – il colore di default**
> Il default del browser è testo **nero** su sfondo **bianco**. Il testo era bianco perché lo **ereditava** dal `body`, che aveva `color: white`. ✅

> ⚠️ **ATTENZIONE – metti la proprietà in alto, nel genitore giusto**
>
> ```css
> p {
>   font-family: arial, sans-serif; /* ❌ cambia solo i paragrafi:
>                                            titolo e nomi restano col carattere vecchio */
> }
>
> body {
>   font-family: arial, sans-serif; /* ✅ la ereditano tutti */
> }
> ```

> ⚠️ **ATTENZIONE – text-align sul body centra tutto**
>
> ```css
> body {
>   text-align: center;
> } /* ❌ centra il testo di TUTTA la pagina, card comprese */
> header {
>   text-align: center;
> } /* ✅ centra solo l'header                              */
> ```

---

## 12. Il trucco del colore evidente

Quando non sai se una regola funziona, mettile un colore impossibile da non vedere:

```css
.card {
  background-color: red;
} /* si vede subito dove sta la card */
```

Poi lo togli.

---

## 13. Git: i 3 comandi

```
git add .                          prepara tutti i file
git commit -m "feat: messaggio"    scatta la foto, con la nota
git push                           carica su GitHub
```

```
feat:   ho aggiunto qualcosa di nuovo
fix:    ho corretto qualcosa
```

> ⚠️ **ATTENZIONE – commit senza messaggio**
> Nel pannello Source Control, se la casella **Message** è vuota, il commit **non parte**.

> ⚠️ **ATTENZIONE – commit e push sono due cose**
>
> ```
> commit  → salvato sul MIO PC
> push    → caricato su GITHUB
> ```

> ⚠️ **ATTENZIONE – Ctrl + C nel terminale**
> Nel terminale **Ctrl + C interrompe** il comando, non copia.
> Per copiare: seleziona e **clic destro**, oppure **Ctrl + Shift + C**.

> ⚠️ **ATTENZIONE – un repository dentro un altro**
> Non mettere una cartella con `.git` dentro un'altra cartella con `.git`: i due Git si mescolano.
> Ogni esercizio ha **il suo** `.git`. Le cartelle che raccolgono gli esercizi no.

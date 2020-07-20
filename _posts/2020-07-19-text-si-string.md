---
layout: post
title: Text și String-uri
categories: [Programare,Start,Elixir,String,Tip,Date]
excerpt: Unul dintre cele mai utile lucruri pe care le facem cu ajutorul calculatorului este să prezentăm informații utilizatorului. De aceea, în programare folosim foarte des informații organizate sub formă de text.
---

Unul dintre cele mai utile lucruri pe care le facem cu ajutorul calculatorului este să prezentăm informații utilizatorului. De aceea, în programare folosim foarte des informații organizate sub formă de text.

## Despre text și string

În multe limbaje de programare, un text este reprezentat ca o înșiruire de caractere cuprinsă între ghilimele.

```elixir
"Acesta este un text în Elixir."
```

În mod normal, termenul pe care-l folosim pentru text în programare este *string*.

Cel mai simplu *string* este cel __vid__.

```elixir
"" # string-ul vid este o simplă pereche de ghilimele
```

Chiar dacă un *string* vid nu conține informație utilă, el e folositor fiindcă poate fi punctul de plecare atunci când "adunăm" mai multe *string*-uri laolaltă.

Deși, la prima vedere, e surprinzător, în Elixir nu există un tip de date dedicat pentru *string*-uri. Acestea sunt implementate în limbaj cu ajutorul altor feluri de date: __binary__ sau __charlist__. Deocamdată nu ne uităm la aceste tipuri de date, dar e util să știm acest lucru. 

## Concatenarea *string*-urilor

Operația de "adunare" a două *string*-uri se numește __concatenare__. Practic alipim cele două *string*-uri și obținem unul nou. În Elixir, *string*-urile de la care am pornit nu se modifică, nici nu se distrug, ele rămân la fel ca înaintea operației de concatenare. Acest lucru este important și e rezultatul faptului că datele sunt imutabile în Elixir (adică nu se modifică). Rezultatul concatenării este un *string* nou.

Operația de concatenare se face cu ajutorul operatorului `<>`:

```elixir
"Hello" <> "Elixir"
```

Expresia de mai sus reprezintă concatenarea *string*-urilor `"Hello"` și `"Elixir"`. Rezultatul pe care-l obținem este un nou *string*, `"HelloElixir"`. Am vrea totuși să obținem un text prietenos pentru utilizator. Deci trebuie să punem un spațiu între cuvinte.

Acest lucru s-ar fi întâmplat dacă am fi concatenat *string*-urile `"Hello "` și `"Elixir"`. Observă spațiul de la sfârșitul *string*-ului `"Helllo "`; el aparține *string*-ului fiincă este între cele două ghilimele. Deci concatenarea celor două dă rezultatul `"Hello Elixir"`.

Fiindcă facem concatenarea a două *string*-uri, spunem că operatorul `<>` este binar -- adică primește doi __operanzi__; lucrează cu două valori și dă un rezultat.

### Despre comutativitate

Atunci când concatenăm două *string*-uri e importantă ordinea în care le punem. De exemplu, poate e destul de evident că

```elixir
"Functional" <> "Programming"
```

nu dă același rezultat cu

```elixir
"Programming" <> "Functional"
```

Primul exemplu are ca rezultat `"FunctionalProgramming"`, iar cel de-al doilea, `"ProgrammingFunctional"`.

Asta ne dovedește că operația de concatenare __nu este comutativă__, deci ordinea contează.

### Despre asociativitate

Pe de altă parte, putem înlănțui mai multe concatenări, fără să conteze ordinea în care aplicăm operațiile. De exemplu:

```elixir
"String concatenation " <> "is" <> " associative."
# dă, în final, rezultatul
"String concatenation is associative."
# chiar dacă aplicăm prima concatenare mai întâi,
"String concatenation is" <> " associative."
# sau dacă aplicăm cea de-a doua concatenare mai întâi
"String concatenation " <> "is associative."
```

Operațiile de concatenare din exemplul anterior se execută de la stânga la dreapta, așa cum am învățat că se evaluează expresiile în mod normal.

Totuși, putem influența ordinea operațiilor, folosind parantezele rotunde:

```elixir
"String concatenation " <> ("is" <> " associative.")
```

De data asta, mai întâi se execută cea de-a doua concatenare și obținem expresia

```elixir
"String concatenation " <> "is associative."
```

care, în final, este evaluată la valoarea `"String concatenation is associative."`.

Acum ne dăm seama că nu contează dacă se execută mai întâi prima concatenare sau cea de-a doua, ceea ce dovedește asociativitatea operației. Mai mult, știind ordinea evaluării operațiilor, putem spune despre concatenarea *string*-urilor că este asociativă la stânga.

### Elementul neutru

Elementul neutru față de concatenare este *string*-ul vid. Asta înseamnă că un *string* concatenat cu cel vid rezultă *string*-ul inițial. Deci rezultatul concatenării cu *string*-ul vid este valoarea celuilalt operand.

De exemplu,

```elixir
"Elixir is fun" <> ""
# este echivalent cu
"" <> "Elixir is fun"
# și dă rezultatul
"Elixir is fun"
```

Valoarea *string*-ului vid este foarte importantă atunci când vrem, de exemplu, să concatenăm o mulțime de *string*-uri. *String*-ul vid va fi valoarea inițială pentru un *acumulator*, iar aceasta nu influențează rezultatul final. Vom vedea lucrul acesta atunci când vom vorbi despre colecții de date.

## Interpolare 

Uneori, avem un text în interiorul căruia vrem să "lipim" dinamic valori. De exemplu, avem un mesaj pe care vrem să-l dăm utilizatorului în fiecare zi: "Astăzi, un euro valorează X lei". Acea valoare X ar trebui să fie dinamică și să reflecte rata de schimb a zilei. Dacă afișăm mesajul astăzi, X are o anumită valoare, dar mâine va avea, cel mai probabil, altă valoare.

Rezolvăm problema inserând o expresie Elixir în interiorul șirului de caractere. Elixir va ști că e o expresie ce trebuie evaluată fiindcă o scriem între caracterele `#{}`.

Pentru exemplul nostru, să presupunem că avem o variabilă `exchange_rate`, a cărei valoare vrem să o inserăm dinamic în *string*:

```elixir
exchange_rate = 4.84
"Astăzi, un euro valorează #{exchange_rate} lei"
```

Expresia pe care am inserat-o în text e simplă, dar putem scrie expresii oricât de complicate. Expresia este evaluată imediat, iar valoarea rezultată este "lipită" în poziția corespunzătoare din text.

## *String*-uri pe mai multe rânduri


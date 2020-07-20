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

În urma evaluării, rezultatul va fi *string*-ul "Astăzi, un euro valorează 4.84 lei".

În termeni tehnici, acest mecanism de inserare a valorii unei expresii într-un șir de caractere se numește __interpolare__.

## *String*-uri multi-linie

Până acum am folosit doar *string*-uri care se scriu pe un singur rând, dar nu suntem limitați la asta. Putem avea șiruri de caractere dispuse pe mai multe linii, astfel:

```elixir
"
Acesta este
un
string
pe mai multe rânduri.
"
```

## *Sigils*

Un alt *feature* interesant pe care ni-l pune limbajul la dispoziție e ceva ce se numește *sigil*. Explicăm cel mai ușor ce înseamnă, printr-un exemplu. Să presupunem că vrem să creăm un *string*, ca e un citat dintr-o carte. Deci avem nevoie să reprezentăm și caracterele "ghilimele" în șirul de caractere.

În mod normal, caracterul `"` reprezintă începutul sau sfârșitul unui *string* și nu e așa ușor să ne dăm seama cum am putea să avem și ghilimele în text. Un *sigil* ne face viața mai ușoară. Îl definim cu ajutorul construcției `~s()`. Revenind la exemplul nostru, putem avea ceva de genul:

```elixir
~s("By working faithfully eight hours a day, you may eventually get to be a boss and work twelve hours a day." -Robert Frost, American poet)
```

*String*-ul rezultat e următorul:

```elixir
"\"By working faithfully eight hours a day, you may eventually get to be a boss and work twelve hours a day.\" -Robert Frost, American poet"
```

Deci rezultatul evaluării unui *sigil* e un *string*, după ce a trecut anumite caractere speciale (cum ar fi ghilimelele) printr-un proces de transformare, care se numește *escaping*.

Vedem în șirul de caractere obținut din *sigil*-ul pe care l-am scris, că ghilimelele sunt prefixate de caracterul *backslash* (`\`).

Cu ajutorul caracterului *backslash*, facem *escape* caracterelor care au, în mod normal, o semnificație aparte și nu pot fi folosite direct în *string*-uri. Folosim *escaping* cu *backslash* și în cazul caracterelor non-tipăribile, cum ar fi *new line*. Reprezentăm într-un *string* caracterul *new line* prin construcția `\n`.

Un exemplu, pe care l-am scris în IEx:

```elixir
iex(7)> my_text = "Împărțim linia\nîn două."
"Împărțim linia\nîn două."
iex(8)> IO.puts(my_text)
Împărțim linia
în două.
:ok
```

Am creat variabila `my_text`, ce a fost legată de *string*-ul "Împărțim linia\nîn două.". Atunci când afișăm pe ecran conținutul șirului de caractere cu funcția `IO.puts/2`, vedem că apare pe două rânduri, fiindcă ăsta e rolul lui *new line*, să despartă reprezentarea pe ecran, adăugând un rând nou.

## Modulul `String`

Tot ce avem nevoie să știm despre *string*-uri găsim în documentația Elixir, în special uitându-ne la modulul `String`: [https://hexdocs.pm/elixir/String.html](https://hexdocs.pm/elixir/String.html).

Pe lângă informații generale despre lucrul cu șiruri de caractere, găsim în documentație că modulul `String` ne pune la dispoziție multe funcții utile, cum ar fi `length/1`, care ne dă lungimea unui *string* sau `upcase/2`, ce transformă în majuscule toate literele din text.

## Concluzii

*String*-urile sunt date cu care lucrăm în majoritatea programelor pe care le scriem, indiferent de limbajul de programare pe care îl alegem. Ele ne permit să prezentăm utilizatorului informații în forma pe care o dorim. Dacă învățăm să folosim *String*-urile bine, vom fi programatori fericiți pe întreaga durată a carierei noastre. :) 

---
layout: post
title: Text și String-uri
categories: [Programare,Start,Elixir,String,Tip,Date]
excerpt: Unul dintre cele mai utile lucruri pe care le facem cu ajutorul calculatorului este să prezentăm informații utilizatorului. De aceea, în programare folosim foarte des informații organizate sub formă de text.
---

Unul dintre cele mai utile lucruri pe care le facem cu ajutorul calculatorului este să prezentăm informații utilizatorului. De aceea, în programare folosim foarte des informații organizate sub formă de text.

## Despre text

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

Operația de "adunare" a două *string*-uri se numește __concatenare__. Practic alipim cele două *string*-uri și obținem unul nou. În Elixir, *string*-urile de la care am pornit nu se modifică, nici nu se distrug, ele rămân la fel ca înaintea operației de concatenare. Acest lucru este important și e rezultatul faptului că datele sunt imutabile în Elixir (adică nu se modifică). Rezultatul concatenării este un *string* nou.

Operația de concatenare se face cu ajutorul operatorului `<>`:

```elixir
"Hello" <> "Elixir"
```

Expresia de mai sus reprezintă concatenarea *string*-urilor `"Hello"` și `"Elixir"`. Rezultatul pe care-l obținem este un nou *string*, `"HelloElixir"`. Am vrea totuși să obținem un text prietenos pentru utilizator. Deci trebuie să punem un spațiu între cuvinte.

Acest lucru s-ar fi întâmplat dacă am fi concatenat *string*-urile `"Hello "` și `"Elixir"`. Observă spațiul de la sfârșitul *string*-ului `"Helllo "`; el aparține *string*-ului fiincă este între cele două ghilimele. Deci concatenarea celor două dă rezultatul `"Hello Elixir"`.

Fiindcă facem concatenarea a două *string*-uri, spunem că operatorul `<>` este binar - adică primește doi __operanzi__; lucrează cu două valori și dă un rezultat.



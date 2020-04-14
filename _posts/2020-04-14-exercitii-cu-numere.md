---
layout: post
title: Exerciții cu numere
categories: [Programare,Start,Elixir,Numere,Tip,Date]
excerpt: La sfârșitul postării anterioare am propus câteva exerciții, prin care să ne familiarizăm cu operatorii aritmetici. Așa cum am promis, ne vom uita acum la câteva dintre exemplele mai interesante.
---

La sfârșitul postării anterioare am propus câteva exerciții, prin care să ne familiarizăm cu *operatorii aritmetici*. Așa cum am promis, ne vom uita acum la câteva dintre exemplele mai interesante.

## Operatorii unari

În primul rând, să ne uităm la exemplele `-8`, `- 8`, `+10`, `+ 10`.

![Operatorii unari plus și minus](/images/lesson-003/plus-minus.png "Operatorii unari plus și minus")

La fel ca în aritmetică, caracterele `+` și `-` puse în fața unui număr reprezintă semnul acelui număr.

Semnul plus, pus în fața unui număr pozitiv, nu are niciun efect și este omis atunci când evaluăm expresia. Acest lucru se vede și în consola interactivă Elixir, `iex`.

În schimb, semnul minus, care ne arată faptul că avem de-a face cu un număr negativ, trebuie să fie prezent. `iex` reflectă acest lucru după evaluarea expresiei.

Captura de ecran ne arată faptul că semnele `+` și `-` pot fi scrise în fața unui număr fie alipite de acesta, fie nu. Elixir înțelege semnificația lor.

Tehnic vorbind, aceste semne sunt operatori aritmetici *unari*. Am vorbit puțin data trecută despre *operatori* și *operanzi*, menționând faptul că ei sunt clasificați după numărul de *operanzi* pe care-i primesc.

Apropo, documentația oficială Elixir se găsește la adresa: [https://hexdocs.pm/elixir/](https://hexdocs.pm/elixir/).

Explicațiile despre operatorii unari le găsim aici:
- `+`: [https://hexdocs.pm/elixir/Kernel.html#+/1](https://hexdocs.pm/elixir/Kernel.html#+/1)
- `-`: [https://hexdocs.pm/elixir/Kernel.html#+/1](https://hexdocs.pm/elixir/Kernel.html#+/1)

## Operații înlănțuite

Următorul exemplu la care aș vrea să ne uităm este `100 + 1 + 10`. Așa cum intuim, expresia se reduce la o singură valoare, suma celor trei valori inițiale. Lucrul cel mai interesant la această expresie este modul în care este evaluată:

![Evaluarea unei expresii cu trei operanzi](/images/lesson-003/100+1+10.jpg "Evaluarea unei expresii cu trei operanzi")

Vedem că evaluarea acesteia e un proces format din doi pași:
- prima dată se evaluează prima adunare, iar expresia este redusă la forma `101 + 10`
- apoi se evaluează ce-a de-a doua operație de adunare, expresia fiind redusă la forma ei finală, `111`

Putem spune că problema a fost descompusă în două probleme mai simple, al căror rezultat a fost apoi combinat pentru a afla rezultatul problemei inițiale. Această tehnică are o mare utilitate în programare și e folosită la rezolvarea multor probleme complexe.

Un alt lucru important pe care trebuie să-l remarcăm e faptul că expresia a fost evaluată de la stânga la dreapta. Acesta este modul în care se evaluează expresiile, dacă nu cumva intervin alte reguli, așa cum vom vedea în ultimul exemplu.

## Operatorul de împărțire a două numere

Prima regulă pe care trebuie să ne-o amintim când vine vorba de operatorul de împărțire `/` este aceea că, în Elixir, rezultatul e întotdeauna un număr real. Vedem asta în captura de ecran următoare:

![Operatorul de împărțire](/images/lesson-003/division.png "Operatorul de împărțire")

Chiar dacă deîmpărțitul se împarte exact la împărțitor, deci câtul ar fi un număr întreg, rezultatul diviziunii prin `/` e un *float*, adică un număr în virgulă mobilă - ceea ce în aritmetică ar fi un număr real.

La fel ca în cazul adunării, o înșiruire de operații de împărțire se execută de la stânga la dreapta.

Așa cum în matematică împărțirea la zero nu este permisă, nici în programare nu putem face acest lucru. Atunci când am încercat să obținem rezultatul expresiei `20 / 0`, Elixir ne-a oferit, în schimb, un mesaj de eroare care spune

```elixir
** (ArithmeticError) bad argument in arithmetic expression
```

În acest caz, argumentul "rău" este valoarea 0 pentru împărțitor.

Atunci când ceva nu merge bine în programul nostru, Elixir "aruncă" o eroare, așa cum este și `ArithmeticError`. Există multe tipuri de erori posibile, fiecare dintre ele reprezentând o anumită situație, pe care noi trebuie să o gestionăm în program. Vom vedea ceva mai încolo cum facem asta.

![Numere cu perioadă](/images/lesson-003/periodic-number.png "Numere cu perioadă")

Dacă rezultatul împărțirii ar fi un număr cu perioadă, Elixir returnează o aproximație a acestuia, cu un număr finit de zecimale.

## Precedența operatorilor

Ultima expresie la care ne uităm este `7 + 3 + -2 * 5 + 10 / 5`.

De data aceasta nu toate operațiile se execută în ordine de la stânga la dreapta fiindcă, așa cum am menționat, intră în acțiune o altă regulă, numită *precedența operatorilor*. Această regulă determină, în esență, care sunt operatorii mai "puternici", și care sunt mai "slabi". Lista completă o găsim în documentația oficială: [https://hexdocs.pm/elixir/operators.html](https://hexdocs.pm/elixir/operators.html).

Pentru operatorii aritmetici pe care-i folosim în exemplul nostru, putem alcătui o listă, în ordinea tăriei, de la cel mai puternic, la cel mai slab:
- operatorul unar `-`, care e folosit pentru `-2`
- operatorii binari de înmulțire (`*`) și împărțire (`/`)
- operatorul binar de adunare (`+`)

Iată cum este evaluată expresia noastră de către Elixir:

![Evaluarea expresiei aritmetice](/images/lesson-003/arithmetic-expression-evaluation.jpg "Evaluarea expresiei aritmetice")

Atunci când avem o expresie mai complexă, de multe ori ajută să delimităm anumiți termeni ai expresiei prin intermediul parantezelor rotunde, pentru a vedea mai bine ordinea în care se execută.

Alteori, parantezele rotunde sunt necesare pentru că ne permit să indicăm noi ordinea în care vrem să fie efectuate operațiile, la fel ca în aritmetică. Atât că în programare putem aplica această tehnică și pentru alte feluri de expresii, nu doar cele aritmetice.

## Concluzie

Cam atât deocamdată despre operatorii aritmetici de bază.

Acum e timpul să instalăm Elixir pe laptopul sau PC-ul propriu și să trecem la următorul nivel în programare.

Dar până la următoarea postare, te încurajez să experimentezi cu diverse expresii aritmetice de genul celei de mai sus. Cu puțin exercițiu, îți va fi din ce în ce mai ușor să evaluezi expresii complexe. În plus, vei putea să identifici "dintr-o privire" expresiile mai simple din care se compune o expresie complexă și ordinea evaluării acestora.

---
layout: post
title: Operații cu numere
categories: [Programare,Start,Elixir,Numere,Tip,Date]
excerpt: Unul dintre primele lucruri pe care le-a realizat omenirea cu ajutorul calculatoarelor electronice a fost calculul aritmetic. Mașinile sunt nemaipomenit de bune la "măcinat" numere.
---

Unul dintre primele lucruri pe care le-a realizat omenirea cu ajutorul calculatoarelor electronice a fost calculul aritmetic. Mașinile sunt nemaipomenit de bune la "măcinat" numere. De exemplu, e mult mai rapid și sigur să facem totalul prețurilor produselor din coșul de cumpărături cu ajutorul unei aplicații de pe *smartphone*. E de așteptat să lăsăm majoritatea calculelor matematice pe seama instrumentului pe care l-am creat pentru așa ceva (chiar dacă acest lucru vine cu un preț). Mai ales, știind că avem în permanență în buzunar un dispozitiv cu putere de procesare de 100 000 de ori mai mare decât calculatorul pe care-l avea nava spațială *Apollo 11*.

Acum, să continuăm să ne familiarizăm cu sintaxa limbajului de programare, adăugând operatorii aritmetici la trusa noastră de unelte.

## Operatorul +

Așa cum ne așteptăm, atunci când scriem `7 + 5` și apăsăm *Enter*, primim rezultatul adunării celor două numere.

![Adunarea a două numere](/images/lesson-002/addition.png "Adunarea a două numere")

Elixir citește această __expresie__, își dă seama că `7` și `5` sunt numere întregi și înțelege că semnul plus dintre ele semnifică faptul că vrem să le adunăm. Așa cum am pomenit și în postarea anterioară, și aici cuvântul cheie este *expresie*. Rezultatul adunării este o valoare. Insist pe această idee fiindcă, dacă ne obișnuim să ne gândim la acest lucru, ne va fi de mare ajutor mai încolo.

Acum trebuie să introducem o nouă noțiune, pentru a înțelege cum clasificăm diverse valori. Deja am văzut, în postarea anterioară, că o înșiruire de caractere, cum ar fi "Hello Elixir!", se numește *string* în programare. Mai clar, spunem că o valoare între ghilimele este __de tip__ *string*.

Trebuie să ținem minte că fiecare valoare cu care lucrăm este de un anumit __tip__. Când spunem __tip__, spunem de fapt __tip de date__. Un tip de date este totalitatea valorilor de un anumit fel. E o mulțime, în principiu, cu număr infinit de valori. Dacă e să ne gândim la *string*-uri ca la totalitatea cuvintelor, ne dăm seama că există o infinitate de cuvinte posibile.

Revenind la numere și aritmetică, știm despre `7` și `5` că sunt numere întregi. Similar, în programare valorile de genul acesta se numesc __întregi__ sau, în engleză, *integers*.

Mai există și alte tipuri de date și le vom descoperi pe parcurs.

Este important să înțelegem ce tip are o valoare, fiindcă doar așa putem ști ce operații putem face cu ea. Fiecare tip de date are asociat un set de caracteristici, care ne vine în ajutor.

Ca un exemplu, știind că 7 este un *integer*, iar "hello" este un *string*, ne dăm seama că nu are rost să încercăm să le adunăm, pentru că o astfel de operație nu are sens. Dacă ar fi să încercăm așa ceva, obținem o eroare:

![Expresie aritmetică incorectă](/images/lesson-002/bad-argument-in-arithmetic-expression.png "Expresie aritmetică incorectă")

Aici, Elixir ne atenționează că am încercat să folosim __operatorul__ aritmetic `+` împreună cu "hello", care este un *string*; iar adunarea cu un *string* nu are sens.

Am folosit deja de câteva ori cuvântul *operator*, referindu-ne la semnul de adunare, dar încă nu am explicat ce înseamnă. Un astfel de semn este numit operator fiindcă este un simbol ce denotă o *operație*.

Așa cum semnul `+` are un nume, la fel și numerele `7` și `5` din exemplul nostru au un nume. Valorile pentru care folosim un operator se numesc __operanzi__.

Tot legat de operatori, în programare există în general mai multe feluri, în funcție de numărul de operanzi cu care lucrează:
1. operatori *unari*, care operează pe un singur operand
2. operatori *binari*, care operează pe doi operanzi; aceștia sunt cel mai des întâlniți
3. operatori *ternari*, care primesc trei operanzi

În exemplul adunării a două numere întregi, operatorul de adunare este un *operator binar*.

## Exerciții

Să facem câteva exerciții cu numere întregi. De data asta, nu ne limităm doar la operatorul de adunare, ci vom introduce și scăderea, înmulțirea și împărțirea.
Așadar, aceasta e lista operatorilor aritmetici de bază:

- adunare: `+`
- scădere: `-`
- înmulțire: `*`
- împărțire: `/`

Hai să rulăm câteva comenzi în consola noastră interactivă. Prin consolă ne referim la un program ce ne permite să introducem comenzi de la tastatură. Un alt exemplu de consolă ar fi *Command Prompt* în Windows sau *Terminal* în Linux si macOS.

Poate ai observat că fereastra în care introducem comenzile afișează în partea de sus textul *Interactive Elixir*. Așa se numește programul pe care îl folosim pentru a rula rapid comenzi în Elixir; prescurtat, se mai numește și `iex`. Lucrul acesta în vedem și în dreptul cursorului, unde introducem comenzile; de exemplu, `iex(1)>`. Valoarea dintre parantezele rotunde reprezintă numărul de ordine al comenzii pentru sesiunea curentă de lucru.

Atunci când vom instala Elixir-ul pe calculatorul nostru, vom vedea și cum lansăm în execuție programul `iex`.

Acum, e timpul să exersăm câteva expresii aritmetice în consola `iex`:

```elixir
169 + 196

17 - 23

-8

+ 10

15 * 15

100 + 1 + 10





```

Fiecare expresie din lista de mai sus e de sine stătătoare. Te încurajez să le execuți pe fiecare în parte și să observi rezultatele. Te rog să observi și modul în care le-am scris în această listă; e intenționat.

Sunt rezultatele așa cum te-ai așteptat? Ce concluzii ai putut trage în legătură cu operatorii aritmetici?

Vom discuta aceste exemple în detaliu în postarea următoare.

Programatorilor Elixir le place să se identifice cu titlul de *alchimiști*. Încet încet devenim și noi mici alchimiști.

Până data viitoare, *Happy brewing!*

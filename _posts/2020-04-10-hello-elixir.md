---
layout: post
title: #001 Hello Elixir
categories: [Programare,Start,Elixir]
excerpt: Elixir este un limbaj de programare cu ajutorul căruia putem crea tot felul de programe. Putem scrie de la jocuri sau aplicații de birou, până la website-uri și sisteme de mesagerie, cum ar fi Whatsapp.
---

Elixir este un limbaj de programare cu ajutorul căruia putem crea tot felul de programe. Putem
scrie de la jocuri sau aplicații de birou, până la aplicații *web* - pe care, de multe ori,
le numim *site*-uri - și sisteme de mesagerie, cum ar fi __Whatsapp__. De fapt, aplicația
__Whatsapp__ e construită pe aceeași fundație pe care rulează toate aplicațiile construite
cu Elixir.

## Despre limbajele de programare

Dar ce este un limbaj de programare? Atunci când doi oameni din țări diferite se întâlnesc,
ei trebuie să găsească o limbă pe care o știu amândoi, pentru a putea comunica.
Să spunem că un român se întâlnește cu un olandez și vor să povestească. Cel mai probabil
amândoi știu engleză, așa că vor discuta în engleză.

Atunci când noi vrem să "conversăm" cu un calculator, trebuie să găsim o limbă comună, pe care
s-o înțelegem amândoi. Un limbaj de programare e o astfel de limbă comună.

Așa cum în lume există multe limbi folosite de culturi diverse, și în lumea digitală există
mai multe limbaje de programare pe care le putem folosi pentru a comunica cu prietenul nostru,
calculatorul.

Calculatorul, cunoscut și sub numele de __sistem de calcul__, este ca un prieten pe care-l
rugăm să ne ajute să rezolvăm o problemă. El este gata să ne ajute și va face __exact__ ce-i
spunem noi să facă. Este responsabilitatea noastră să-i comunicăm pe înțelesul lui ce anume
vrem să obținem, care e rezultatul la care vrem să ajungem.

De aceea, e important să învățăm nu doar limba pe care o înțelege (limbajul de programare),
ci și modul în care trebuie să-i descriem problema și ceea ce vrem să obținem (tehnici de
programare). Dar lucrurile acestea le vom învăța, pas cu pas, la timpul potrivit.

La fel ca o limbă naturală, un limbaj are o gramatică. Această gramatică se numește
în programare, __sintaxa limbajului__. În primă fază, ne vom concentra să învățăm elemente
din sintaxa limbajului Elixir, pentru a putea descrie cât mai multe lucruri.

Orice program pe calculator e format din una sau mai multe instrucțiuni, scrise în limbajul
de programare pe care l-am ales.
E ca și când îi dăm calculatorului o rețetă pe care noi am scris-o, iar el trebuie să
pregătească prăjitura descrisă în rețetă.

La fel ca o rețetă culinară, un program se scrie și se citește, rând cu rând, de la stânga
la dreapta și de sus în jos. Programatorii se referă la textul rețetei - pardon, programului! -
cu termenul de __cod__, pe care o să-l întâlnim foarte des. În orice discuție cu un programator
va folosi cel puțin o dată cuvântul "cod".

De asemenea, un rând de cod se mai numește "linie de cod" sau simplu, "linie". Deci dacă îți
spune cineva să citești codul de la linia 7, nu te speria, vrea să spună să citești textul
de la rândul cu numărul 7.

## Primul nostru program

Hai să scriem primul nostru program!

Tradiția spune că primul program pe care trebuie să-l scrii într-un limbaj nou de programare
este "Hello World!". Ne începem și noi drumul spre a deveni programatori, scriind propria
noastră versiune, pe care o numim "Hello Elixir!".

Prin acest program vrem să instruim calculatorul să afișeze pe ecran textul "Hello Elixir!".
De acord, nu e cel mai interesant lucru de făcut, nici cel mai entuziasmant program pe care
l-am văzut vreodată, însă așa începe totul, cu lucruri simple.

Înainte de a ne apuca să instalăm pe calculatorul nostru aplicațiile ce țin de programarea
cu Elixir, hai să folosim un instrument pe care l-am găsit *online* și care ne ajută să
scriem rapid niște *cod* în Elixir.

Accesează website-ul următor: [http://try-elixir.herokuapp.com](http://try-elixir.herokuapp.com).

Vedem că se deschide o pagină ce are în mijloc un chenar de culoare crem.

![Pagină interactivă Elixir](images/lesson-001/interactive-elixir.png "Pagină interactivă Elixir")

În acest dreptunghi putem scrie comenzi Elixir. Pentru a face acest lucru, dăm click în
interiorul chenarului. În dreapta textului care spune `iex(1)>` vedem că apare un mic dreptunghi
colorat în gri. Acesta este *cursorul* care ne indică unde urmează să scriem următoarea
comandă.

Acum putem scrie programul nostru, "Hello Elixir!". Primul nostru program va conține un singur
rând:

```elixir
"Hello Elixir!"
```

O dată ce am scris comanda de mai sus, apăsăm tasta *Enter*. De fiecare dată cand vrem să rulăm o
comandă, apăsăm *Enter*. Vom vedea mai târziu că o comandă se poate întinde pe mai multe rânduri.
Dar deocamdată să ne concentrăm pe comenzi scurte și simple.

După ce am apăsat *Enter*, programul nostru a fost rulat, iar calculatorul a executat comanda pe
care am scris-o. Rezultatul a fost afisat cu un rând mai jos, lucru pe care-l putem vedea în
captura de ecran:

![Hello Elixir!](images/lesson-001/hello-elixir.png "Hello Elixir!")

__Felicitări! Tocmai ai scris primul tău program pe calculator!__

Poate faptul că ai afișat un text pe ecran nu pare a fi mare lucru. Totuși, la fel ca în cazul unei
piese de teatru, în culise se petrec o grămadă de activități.

## Să învățăm niște sintaxă

Hai să vedem ce s-a întâmplat de fapt.

În primul rând, trebuie să remarcăm că atunci când vrem să lucrăm cu text în Elixir, trebuie să
îl punem între ghilimele drepte. În programare, un astfel de text cuprins între ghilimele se numește
un *string*. Un *string* nu este nimic altceva decât o înșiruire de caractere, puse laolaltă în
ordinea pe care o vrem noi. Ori de câte ori vrem să lucrăm cu text, practic lucrăm cu *string*-uri.

Acum că știm ce reprezintă "Hello Elixir!" între ghilimele, următorul lucru pe care trebuie să îl
știm e faptul că acest *string* reprezintă o __expresie__. O expresie este o instrucțiune care este
evaluată la o valoare. Adică ne uităm la acea instrucțiune și putem să înțelegem ce valoare are ca
rezultat. O valoare poate fi, de exemplu, un *string* sau un număr.

Când am spus instrucțiune, m-am referit la faptul că poate fi o instrucțiune simplă,
cum este cea pe care tocmai am scris-o, sau complexă, formată din mai multe instrucțiuni simple
puse laolaltă. În orice caz, simplă sau complicată, instrucțiunea, adică expresia, este redusă,
în final, la o valoare.

Un lucru pe care trebuie să-l reținem este că 

{% include pullquote.html quote="în Elixir fiecare instrucțiune este o expresie" %}, adică

fiecare instrucțiune, atunci când este evaluată, dă ca rezultat o valoare. Acest lucru este foarte
important și vom vedea că ne ajută foarte mult.

În cazul expresiei noastre "Hello Elixir!", care este un *string*, valoarea ei este chiar *string*-ul
în sine. Asta pentru că, putem spune, e o valoare fundamentală, pe care nu o putem evalua mai mult
decât atât, ca să o reducem mai mult.

Vom vedea în lecția următoare un alt exemplu de expresie, ceva mai complicat, și vom începe să
învățăm cum să evaluăm expresiile, pentru a le calcula valoarea.

Deci, atunci când am scris expresia "Hello Elixir!" și am apăsat *Enter*, Elixir a evaluat
- sau, am putea spune, calculat - valoarea ei și a afișat-o pe ecran, cu un rând mai jos.

## Concluzie

Primul nostru program a fost scurt, alcătuit dintr-o singură expresie simplă. Dar uite câte lucruri
interesante se pot spune despre el! Putem privi o expresie de genul acesta ca pe o cărămidă într-o
construcție. Dacă ne uităm la o singură cărămidă, ea nu e deloc interesantă, nici nu ne este
prea folositoare. Dar dacă punem laolaltă mai multe cărămizi și le aranjăm într-un mod inventiv,
putem construi clădiri impresionante, interesante, frumoase și cu o mare utilitate.

Să nu uităm că fiecare program e alcătuit din cărămizi mici și neinteresante, precum expresia
"Hello Elixir!", dar dacă le legăm între ele, obținem programe extraordinare!

În postarea următoare vom scrie un nou program și vom învăța să evaluăm expresii un pic mai complexe.

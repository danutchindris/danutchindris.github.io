---
layout: post
title: Expression vs Statement
categories: [Java,Programare,Cod,Expression,Statement]
excerpt: Avem tendința să programăm pe fugă, să terminăm un task rapid, pentru că suntem contra timp și noua versiune trebuie livrată în curând. E foarte ușor să facem compromisuri de design și să uităm că până și cele mai mici decizii pot influența rezultatul muncii noastre.
---

Avem tendința să programăm pe fugă, să terminăm un *task* rapid, pentru că suntem contra timp
și noua versiune trebuie livrată în curând. E foarte ușor să facem compromisuri de *design* și să
uităm că până și cele mai mici decizii pot influența rezultatul muncii noastre.

Unul dintre compromisurile mici pe care tindem să le facem în programarea orientată pe obiecte
este să programăm preponderent folosind *statement*-uri, în deficitul expresiilor.
Să definim cei doi termeni, în cuvinte simple.

## Definiții

### *Statement*

Un *statement* este o instrucțiune
care execută o sarcină, dar nu returnează o valoare semnificativă. Cu alte cuvinte, rulăm un
*statement* pentru efectele lui. Atenție, este foarte ușor ca aceste efecte să devină efecte
secundare, nedorite într-un program riguros.

În locul cuvântului *statement* cred că am putea folosi "afirmație" în limba română. Totuși,
folosesc în continuare cuvântul în engleză fiindcă nu am găsit un echivalent satisfăcător,
care să arate semnificația lui. La fel procedez și în cazul altor termeni informatici,
marcându-i prin caractere italice.

Un exemplu de *statement* ar putea fi instrucțiunea de a scrie pe ecran, cu ajutorul metodei `println()`:

```java
System.out.println("The result of println() is a void");
```

Efectul execuției acestei metode este de a scrie un text la *standard output*. Interesant este că
nu putem extrage nicio valoare în urma acestui apel; nu primim o valoare pe care să o putem folosi
mai departe.

În Java, un indiciu al faptului că avem de-a face cu un statement este atunci când tipul de retur
al unei metode este `void`.

Un alt exemplu de *statement* ar fi instrucțiunea de apelare a unei metode de tip *setter*.
Aceasta modifică valoarea unei proprietăți a unei clase, dar nu îi returnează valoarea. Concret,
putem avea ceva de genul:

```java
class Order {

   private String name;
   private BigDecimal price;

   public String getName() {
      return name;
   }
   
   public void setName(String name) {
      this.name = name;
   }
   
   public BigDecimal getPrice() {
      return price;
   }

   public void setPrice(BigDecimal price) {
      this.price = price;
   }
}

...

final Order o = new Order;
o.setName("Rechizite");
o.setPrice(new java.math.BigDecimal(99.43));
```

Apelurile metodelor `setName()` și `setPrice()` sunt *statement*-uri, deoarece returnează `void`.
Deci nu returnează nicio valoare utilă. Aceste apeluri se efectuează pentru efectele lor, acelea de
a seta valori proprietăților obiectului.

### Expresie

O expresie este o instrucțiune sau o compunere a mai multor instrucțiuni ce returnează o valoare.
De exemplu, aplicarea operatorului ternar este evaluată la o expresie. Să urmărim exemplul următor:

```java
import java.time.DayOfWeek;
import java.time.LocalDate;

...

final LocalDate localDate = LocalDate.now();
final DayOfWeek dayOfWeek = localDate.getDayOfWeek();

final String today = (dayOfWeek == DayOfWeek.SATURDAY || dow == DayOfWeek.SUNDAY)
						? "It's weekend!"
							: "Time to work!";
```

Vedem cum execuția construcției ce folosește operatorul ternar returnează o valoare de tip `String`,
deci este o expresie.

Un alt exemplu de expresie ar fi apelul metodelor `getName()` si `getPrice()` din clasa `Order`,
definită mai sus. Vedem că acestea returnează valori de tip `String`, respectiv `BigDecimal`.

De fapt, chiar și `1 + 1` este o expresie, fiindcă returnează o valoare.

Încă un exemplu interesant de expresii în Java ar fi asignarea valorilor:

```java
int x, y;
x = y = 10;
```

Exprimarea de mai sus cu dubla asignare este validă. Fiindcă operatorul de asignare este asociativ
la dreapta, prima dată se execută expresia `y = 10`. Aceasta returnează valoarea lui `y`, care este
asignată în continuare variabilei `x`. Bineînțeles, și expresia în care este implicat `x` returnează
o valoare, dar aceasta nu este folosită imediat.


Bazându-ne pe aceste idei, putem să identificăm în orice situație dacă avem de-a face cu *statement*-uri
sau expresii.

## Ce să folosim?

Experiența proiectelor pe care am lucrat mi-a arătat că este mult mai ușor să înțeleg un algoritm
urmărind tipurile și valorile evaluate ale expresiilor. Uneori, aceste expresii se compun între ele
pentru a obține alte expresii, mai complexe. În final, obținem valoarea finală, rezultată în urma
rulării algoritmului.

Acum, am putea folosi un *statement* pentru a prezenta rezultatul obținut lumii exterioare.
Putem scrie "valoarea" pe ecran, o putem stoca într-o bază de date, o putem trimite către un consumator
extern prin rețea etc. Toate aceste operații sunt __efecte__.

Abordarea prezentată mai sus poate fi extrapolată pentru funcții, care neapărat returnează valori
și pot fi compuse. Cu ajutorul lor, obținem soluții riguroase pentru orice problemă.

Pe de altă parte, dacă alegem să presărăm prin programul nostru multe *statement*-uri, descoperim că
este greu să mai înțelegem exact ce face algoritmul și care este starea datelor cu care lucrăm.
Efectele *statement*-urilor devin efecte secundare (*side effects* în engleză), efecte nedorite,
pentru că nu mai deținem cu adevărat controlul algoritmului. În această situație este foarte ușor să
introducem defecte, care trec neobservate.

De exemplu, ar trebui evitat, pe cât posibil, apelul metodelor de tip *setter*. Dacă putem modifica
valorile proprietăților unui obiect oriunde în program, nu mai avem nicio garanție despre starea
obiectului. Proprietățile ar putea conține orice, inclusiv `null`! Acum, algoritmul e la mila
programatorului, care poate și-a adus aminte să testeze dacă proprietățile au valoare. Și chiar dacă
există valori, e greu să urmărim derularea algoritmului, să știm care sunt acestea.

Această idee merge mână în mână cu un alt concept, care se numește __imutabilitate__; un subiect pe
care-l vom aborda într-o altă postare.

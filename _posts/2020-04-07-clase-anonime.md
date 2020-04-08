---
layout: post
title:  Clase anonime
categories: [Java,Programare,Cod,Clasa anonima]
excerpt: În designul orientat pe obiecte, există situații în care avem nevoie de o implementare specializată a unei clase, despre care știm că nu va fi folosită în niciun alt loc. În astfel de ocazii, avem la îndemână clasele anonime.
---

În designul orientat pe obiecte, există situații în care avem nevoie de o implementare specializată a unei clase, despre care știm că nu va fi folosită în niciun alt loc. În astfel de ocazii, avem la îndemână clasele anonime.

## Situația 1

### Subclasă anonimă a unei clase specificate

Să presupunem că avem o clasă `Food` definită astfel:

```java
class Food implements Eatable {

  @Override
  public String serve() {
      return "food";
  }
}
```
      
Dacă avem nevoie de o subclasă a acesteia, în mod normal o extindem într-o nouă clasă, folosind cuvântul `extends`.
Totuși, în cazul în care avem nevoie de o subclasă despre care știm că nu va mai fi utilă și în alte locuri,
putem crea o implementare anonimă, astfel:

```java
// create an instance of an anonymous subclass of Food
final Food food = new Food() {

  @Override
  public String serve() {
      return "new food";
  }
};
```

Atunci când apelăm `food.serve()`, valoarea returnată va fi `"new food"`, datorită polimorfismului dinamic.
Într-adevăr, tipul variabilei `food` este`Food`, dar obiectul pe care îl referențiază este o instanță a clasei anonime
ce extinde `Food`.
Aici, cuvântul `extends` este implicit, dar noi știm că această clasă anonimă extinde clasa `Food`. Deci,
instanța clasei anonime, creată *in-place*, are o relație de tipul *is-a* cu `Food`.

Scopul unei astfel de clase anonime este de a suprascrie (*override*) una sau mai multe dintre metodele superclasei.
În cazul nostru, clasa anonimă suprascrie metoda `serve()`.

## Situația 2

### Clasă ce implementează în mod anonim o interfață specificată

Similar primului caz, putem crea o clasă anonimă care implementează o interfață *in-place*.
De exemplu, având interfața:

```java
interface Eatable {

  String serve();
}
```

putem crea o implementare anonimă a acesteia, astfel:

```java
final Eatable eatable = new Eatable() {

  @Override
  public String serve() {
      return "some food";
  }
};
```

La prima vedere, poate părea ciudat să folosim cuvântul `new` împreună cu numele unei interfețe - `new Eatable()`.
Mai mult decât atât, vedem că am aplicat paranteze rotunde numelui interfeței - `Eatable()` -, ca și când am apelat
un constructor.

Totuși, exprimarea este validă pentru că, în continuare, am furnizat implementarea anonimă a interfeței. Am făcut
lucrul acesta între acolade. Aici observăm caracterul punct-și-virgulă după acolada de sfârșit, pentru că este sfârșitul
*statement*-ului început o dată cu declarația variabilei `eatable` - în Java fiecare *statement* trebuie terminat cu
punct-și-virgulă.

Așadar, aici cuvântul `implements` este implicit, dar știm că e vorba despre o implementare anonimă a interfeței `Eatable`.
Deci, cuvantul `new` îl aplicăm constructorului clasei anonime - constructor apelat prin `()` - prezente dupa `Eatable`,
care este numele interfeței pe care o implementăm aici.

O observație ar fi că o clasă anonimă definită astfel nu poate implementa decât o interfață, cea numită în definiția clasei.
Acest lucru e restrictiv, pentru că o clasă definită în mod obișnuit - `class MyClass {...}` - poate implementa mai multe
interfețe. 

## Situația 3

### Clasă internă anonimă, definită pe locul unui argument

De multe ori nu avem nevoie de o variabilă care să referențieze o instanță de clasă anonimă. Așa că definim clasa
și o instanțiem pe loc, acolo unde vrem s-o transmitem ca parametru unei metode.
De exemplu, implementăm ad-hoc interfața `Comparator`, instanțiem clasa anonimă și transmitem ca parametru
această instanță metodei `sort()`, astfel:

```java
Collections.sort(Arrays.asList("ghi", "abc", "def"), new Comparator<String>() {

  @Override
  public int compare(String a, String b) {
      return a.compareTo(b);
  }
});
```

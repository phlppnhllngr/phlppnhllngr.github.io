---
tags: [Notebooks/Java]
title: Design Patterns
created: '2021-09-08T12:55:46.466Z'
modified: '2021-09-08T12:56:26.772Z'
parent: Java
---

# Design Patterns
- [https://github.com/iluwatar/java-design-patterns](https://github.com/iluwatar/java-design-patterns)
- [https://github.com/bethrobson/Head-First-Design-Patterns](https://github.com/bethrobson/Head-First-Design-Patterns)

## Factory method
```java
class SomeFactory {
  public SomeInterface newInstance() {
    return new SomeImpl();
  }
}
```


## Observer+Listener vs Publisher/Subscriber
- **Observer+Listener**
*...an object, called the subject, maintains a list of its dependents, called observers, and notifies them automatically of any state changes, usually by calling one of their methods.*

```java
class Subject {

  List<Observer> observers;

  void register(Observer observer) {
    this.observers.add(observer);
  }

  void onStateChange() {
    this.observers.forEach(Observer::notify);
  }

}

class Observer {

  void notify() { ... }

  void listen(Subject subj) {
    subj.register(this);
  }

}
```

- **Publisher/Subscriber**
*In ‘Publisher-Subscriber’ pattern, senders of messages, called publishers, do not program the messages to be sent directly to specific receivers, called subscribers. This means that the publisher and subscriber don’t know about the existence of one another. There is a third component, called broker or message broker or event bus, which is known by both the publisher and subscriber, which filters all incoming messages and distributes them accordingly.*


## Flyweight
Verwendung bei großer Anzahl an (immutablen) Objekten, die sich nicht oder kaum unterscheiden. Anstatt ein weiteres identisches zu erzeugen, wird eine Referenz auf ein schon bestehendes (im Cache) geliefert. Umsetzung: Factory mit Map,
Code: [https://github.com/iluwatar/java-design-patterns/tree/master/flyweight](https://github.com/iluwatar/java-design-patterns/tree/master/flyweight)


## Template
Abstrakte Klasse, die einen bestimmten Ablauf beschreibt. Konkrete Implementierungen müssen Methoden bereitstellen.

```java
abstract class Template {

  abstract void prepare();
  abstract void execute();
  abstract void cleanup();

  public void run() {
    prepare();
    execute();
    cleanup();
  }

}
```


## State machine
- https://www.baeldung.com/java-state-design-pattern


## Step Builder
- https://svlada.com/step-builder-pattern/
- ```java
  Email email = Email.builder().from(EmailAddress.of("Microservices Weekly <mw@microservicesweekly.com>"))
	.to(EmailAddress.of("svlada@gmail.com"))
	.subject(Subject.of("Subject"))
	.content(Content.of("Test email"))
	.build();
  ```


## Delegate
- siehe auch Lombok->Delegate
---
title: Code
parent: Java
---

# Code

## Allgemein

- Null
  - Lombok @NonNull, Spring @NonNull / @Nullable
  - lieber Leerstring, empty collection o.Ä. statt null returnen
  - *You should only be checking for null when there's something meaningful that you can do about it, and that's typically only on the entry points into your system / app.*

## Exceptions
- *checked exceptions are used when we access something from outside JVM boundry i.e. reading from file, database and network*
- Alternativen: false, null, Optional, Empty
- Nachteile
  - Stacktrace serialisieren teuer
- Vorteile
    - zentrales Error-handling (z. B. Spring->@ExceptionHandler)
- "Effective Java", Joshua Bloch:
  1. *Use exceptions only for exceptional conditions*
  2. *Use checked exceptions for recoverable conditions and runtime exceptions for programming errors*
      - *Runtime exceptions indicates programming errors that can be prevented by checking some preconditions, such as array boundary and nullness checks.*
  3. *Avoid unnecessary use of checked exceptions*
      - *checked exceptions brings the burden to callers for handling the exceptional conditions*
  4. *Favor the use of standard exceptions*
      - *IO, IllegalArgument, java.text.Parse, IllegalState, Arithmetic, NullPointer*
  5. *Throw exceptions appropriate to the abstraction*
  6. *Document all exceptions thrown by each method*
      - *javadoc @throws*
  7. *Include failure-capture information in detail messages*
  8. *Strive for failure atomicity*
  9. *Don't ignore exceptions*
 

### Checked Exceptions als unchecked behandeln
```java
@SuppressWarnings("unchecked")
public static <T, X extends Throwable> T unchecked(Callable<T> c) throws X {
    try {
        return c.call();
    } catch (Exception e) {
        throw (X) e;
    }
}
// ...
unchecked(() -> new URL("foo));
```


## Klassennamen
<section style="font-size: .8em">
  <b>Utility</b>
  <ul>
    <li>&lt;Type&gt; + 's': Exceptions, Strings, ...</li>
  </ul>
  <b>Prefix</b>
  <ul>
    <li>Abstract</li>
    <li>Generic</li>
    <li>Simple</li>
    <li>Default</li>
    <li>Pre</li>
    <li>Post</li>
    <li>Async</li>
  </ul>
  <b>Suffix</b>
  <ul>
    <li>Client</li>
    <li>Container</li>
    <li>Manager</li>
    <li>Processor</li>
    <li>Handler</li>
    <li>Info</li>
    <li>Details</li>
    <li>Transformer</li>
    <li>Configurer</li>
    <li>Configuration</li>
    <li>Extractor</li>
    <li>Parser</li>
    <li>Creator</li>
    <li>Factory</li>
    <li>Behavior</li>
    <li>Parser</li>
    <li>Reader</li>
    <li>Repository</li>
    <li>Strategy</li>
    <li>Wrapper</li>
  </ul>
</section>


## BigDecimal
*A BigDecimal is defined by two values: an arbitrary precision integer and a 32-bit integer scale. The value of the BigDecimal is defined to be `unscaledValue * 10^(-scale)`*
- precision and scale
  - **precision**
    - <u>Total number of significant digits</u>
    - is the number of digits in the unscaled value. For instance, for the number 123.45, the precision returned is 5.
    - signifikante Stellen
      - *DIN 1333 definiert die signifikanten Stellen als die erste von Null verschiedene Stelle bis zur Rundungsstelle.*
      - 0,009876 -> 4 sign. Stellen
      - Faustregeln zur Präzision des Ergebnisses bei Rechnungen
        - Das Ergebnis einer Addition/Subtraktion bekommt genauso viele Nachkommastellen wie die Zahl mit den wenigsten Nachkommastellen.
        - Das Ergebnis einer Multiplikation/Division bekommt genauso viele signifikante Stellen wie die Zahl mit den wenigsten signifikanten Stellen.
  - **scale**
    - <u>Number of digits to the right of the decimal point</u>
    - If zero or positive, the scale is the number of digits to the right of the decimal point.
      If negative, the unscaled value of the number is multiplied by ten to the power of the negation of the scale. For example, a scale of -3 means the unscaled value is multiplied by 1000.
    - examples
      - 12345 with scale 5 = 0.12345
      - 12345 with scale 4 = 1.2345
      - 12345 with scale 0 = 12345
      - 12345 with scale -1 = 1.2345E+5
  - examples
    - 12345 / 100000 = 0.12345 // scale = 5, precision = 5
    - 12340 / 100000 = 0.1234 // scale = 5, precision = 4
    - 1 / 100000 = 0.00001 // scale = 5, precision = 1
- Caveats
  - double-Constructor
    ```java
    new BigDecimal(0.1); // 0.1000000000000000055511151231257827021181583404541015625
    BigDecimal.valueOf(0.1); // 0.1 - can lose precision if many fraction digits
    new BigDecimal("0.1"); // 0.1 - preferred over valueOf (no precision lost)
    ```
  - *the equals method considers two BigDecimal objects equal only if they are equal in both value and scale*
  - *compareTo: Two BigDecimal objects that are equal in value but have a different scale (like 2.0 and 2.00) are considered equal by this method.*
- Fixe Anzahl Nachkommastellen
  ```java
  value = value.setScale(2, RoundingMode.XY)
  ```


## Strings, Chars, Numbers
- ASCII<br/>
  Char | Dec<br/>
  \----------<br/>
  '0'  | 48<br/>
  '9'  | 57<br/>
  'a'  | 97<br/>
  'z'  | 122<br/>
  'A'  | 65<br/>
  'Z'  | 90
- `"az09AZ".chars() // IntStream: 97, 122, 48, 57, 65, 90`
- `Integer.parseInt("B", 16) // 11`
- `char c = (char) 65 // 'A'`
- `int i = 'A' // 65`
- `"A".charAt(0) // 'A'`
- `65 == 'A' // true`

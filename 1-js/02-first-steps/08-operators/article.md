# Basis operators, wiskunde

We kennen veel operators van school. Het zijn dingen zoals optellen `+`, vermenigvuldigen `*`, aftrekking `-`, enzovoort.

In dit hoofdstuk beginnen we met eenvoudige operators, en concentreren we ons vervolgens op JavaScript-specifieke aspecten, niet gedekt door schoolrekenen.

## Termen: "unair", "binair", "operand"

Voordat we gaan verder, laten we eerst wat algemene terminologie begrijpen.

- *Een operand* -- is waar operators op worden toegepast. Bijvoorbeeld, in de vermenigvuldiging van `5 * 2` zijn er twee operanden: de linker operand is `5` en de rechter operand is `2`. Soms noemen mensen deze "argumenten" in plaats van "operanden".
- Een operator is *unair* als hij een enkele operand heeft. Bijvoorbeeld, de unaire ontkenning `-` keert het teken van een getal om: 

    ```js run
    let x = 1;

    *!*
    x = -x;
    */!*
    alert( x ); // -1, unaire ontkenning is toegepast
    ```
- Een operator is *binair* als hij twee operanden heeft. Dezelfde min bestaat ook in binaire vorm:

    ```js run no-beautify
    let x = 1, y = 3;
    alert( y - x ); // 2, binaire min trekt waarden af
    ```

    Formeel hebben we in de bovenstaande voorbeelden twee verschillende operators die hetzelfde symbool delen: de ontkenningsoperator, een unaire operator die het teken omkeert, en de aftrekkingsoperator, een binaire operator die het ene getal van het andere aftrekt.

## Wiskunde

De volgende wiskundige bewerkingen worden ondersteund:

- Optellen `+`,
- Aftrekken `-`,
- Vermenigvuldigen `*`,
- Afdeling `/`,
- Rest `%`,
- Exponentiatie `**`.

De eerste vier zijn eenvoudig, terwijl `%` en `**` er een paar woorden over nodig hebben.

### Rest %

De rest-operator `%` is, ondanks zijn uiterlijk, niet gerelateerd aan procenten.

Het resultaat van `a % b` is de [rest](https://nl.wikipedia.org/wiki/Rest) van de gehele deling van `a` door `b`.

Bijvoorbeeld:

```js run
alert( 5 % 2 ); // 1, een rest van 5 gedeeld door 2
alert( 8 % 3 ); // 2, een rest van 8 gedeeld door 3
```

### Exponentiatie **

De exponentiatie-operator `a ** b` vermenigvuldigt `a` met zichzelf `b` keer.

Bijvoorbeeld:

```js run
alert( 2 ** 2 ); // 4  (2 vermenigvuldigd met zichzelf 2 keer)
alert( 2 ** 3 ); // 8  (2 * 2 * 2, 3 keer)
alert( 2 ** 4 ); // 16 (2 * 2 * 2 * 2, 4 keer)
```

Wiskundig is de exponentiatie ook gedefineerd voor niet-gehele getallen. Een vierkantswortel is bijvoorbeeld een exponentiatie met `1/2`: 

```js run
alert( 4 ** (1/2) ); // 2 (macht van 1/2 is hetzelfde als een vierkantswortel)
alert( 8 ** (1/3) ); // 2 (macht van 1/3 is hetzelfde als een kubieke wortel)
```


## Tekenreeks samenvoeging met binaire +

Laten we eens kennismaken met functies van JavaScript operators die verder gaan dan schoolrekenen.

Gewoonlijk telt de plus operator `+` getallen op.

Maar, als de binaire `+` wordt toegepast op tekenreeksen, worden ze samengevoegd:

```js
let s = "mijn" + "tekenreeks";
alert(s); // mijntekenreeks
```

Merk op dat als er een van de operanden een tekenreeks is, de andere ook naar een tekenreeks wordt geconverteerd.

Bijvoorbeeld:

```js run
alert( '1' + 2 ); // "12"
alert( 2 + '1' ); // "21"
```

Kijk, het maakt niet uit of de eerste operand is een tekenreeks of de tweede.

Hier is een complexer voorbeeld:

```js run
alert( 2 + 2 + '1' ); // "41" en niet "221"
```

Hier werken de operators na elkaar. De eerste `+` telt twee getallen op, dus het geeft `4` terug, dan voegt de volgende `+` de tekenreeks `1` eraan toe, dus het is als `4 + '1' = 41`.

De binaire `+` is de enige operator die tekenreeksen op een dergelijke manier ondersteunt. Andere rekenkundige operators werken alleen met getallen en zetten hun operanden altijd om in getallen.

Hier is de demo voor aftrekken en delen:

```js run
alert( 6 - '2' ); // 4, converteert '2' naar een getal
alert( '6' / '2' ); // 3, converteert beide operanden naar getallen
```

## Numerieke conversie, unaire +

De plus `+` bestaat in twee vormen: de binaire vorm die we hierboven gebruikten en de unaire vorm.

De unaire plus of, met andere woorden, de plus operator `+` toegepast op een enkele waarde, doet niets met getallen. Maar als de operand geen getal is, converteert de unaire plus het naar een getal.

Bijvoorbeeld:

```js run
// Geen effect op getallen
let x = 1;
alert( +x ); // 1

let y = -2;
alert( +y ); // -2

*!*
// Converteert niet-getallen
alert( +true ); // 1
alert( +"" );   // 0
*/!*
```

Hij doet eigenlijk hetzelfde als `Number(...)` (Getal), maar is korter.

De behoefte om tekenreeksen naar getallen te converteren doet zich zeer vaak voor. Als we bijvoorbeeld waarden van HTML-formuliervelden krijgen, zijn dit meestal tekenreeksen. Wat als we ze willen optellen?

De binaire plus zou ze als tekenreeksen toegevoegen:

```js run
let apples = "2";
let oranges = "3";

alert( apples + oranges ); // "23", de binaire plus voegt tekenreeksen samen
```

Als we ze als getallen willen behandelen, moeten we ze converteren en dan optellen:

```js run
let apples = "2";
let oranges = "3";

*!*
// beide waarden geconverteerd naar getallen vóór de binaire plus
alert( +apples + +oranges ); // 5
*/!*

// de langere variant
// alert( Number(apples) + Number(oranges) ); // 5
```

Vanuit het standput van een wiskundige kan de overvloed aan pluspunten vreemd lijken. Maar vanuit het standput van een programmeur is er niets bijzonders: unaire plussen worden eerst toegepast, ze converteren tekenreeksen naar getallen, en dan telt de binaire plus ze op.

Waarom worden unaire plussen toegepast op waarden vóór de binaire? Zoals we zullen zien, is dat vanwege hun *hogere prioriteit*.

## Operator precedence

If an expression has more than one operator, the execution order is defined by their *precedence*, or, in other words, the default priority order of operators.

From school, we all know that the multiplication in the expression `1 + 2 * 2` should be calculated before the addition. That's exactly the precedence thing. The multiplication is said to have *a higher precedence* than the addition.

Parentheses override any precedence, so if we're not satisfied with the default order, we can use them to change it. For example, write `(1 + 2) * 2`.

There are many operators in JavaScript. Every operator has a corresponding precedence number. The one with the larger number executes first. If the precedence is the same, the execution order is from left to right.

Here's an extract from the [precedence table](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Operator_Precedence) (you don't need to remember this, but note that unary operators are higher than corresponding binary ones):

| Precedence | Name | Sign |
|------------|------|------|
| ... | ... | ... |
| 17 | unary plus | `+` |
| 17 | unary negation | `-` |
| 16 | exponentiation | `**` |
| 15 | multiplication | `*` |
| 15 | division | `/` |
| 13 | addition | `+` |
| 13 | subtraction | `-` |
| ... | ... | ... |
| 3 | assignment | `=` |
| ... | ... | ... |

As we can see, the "unary plus" has a priority of `17` which is higher than the `13` of "addition" (binary plus). That's why, in the expression `"+apples + +oranges"`, unary pluses work before the addition.

## Assignment

Let's note that an assignment `=` is also an operator. It is listed in the precedence table with the very low priority of `3`.

That's why, when we assign a variable, like `x = 2 * 2 + 1`, the calculations are done first and then the `=` is evaluated, storing the result in `x`.

```js
let x = 2 * 2 + 1;

alert( x ); // 5
```

### Assignment = returns a value

The fact of `=` being an operator, not a "magical" language construct has an interesting implication.

Most operators in JavaScript return a value. That's obvious for `+` and `-`, but also true for `=`.

The call `x = value` writes the `value` into `x` *and then returns it*.

Here's a demo that uses an assignment as part of a more complex expression:

```js run
let a = 1;
let b = 2;

*!*
let c = 3 - (a = b + 1);
*/!*

alert( a ); // 3
alert( c ); // 0
```

In the example above, the result of expression `(a = b + 1)` is the value which was assigned to `a` (that is `3`). It is then used for further evaluations.

Funny code, isn't it? We should understand how it works, because sometimes we see it in JavaScript libraries.

Although, please don't write the code like that. Such tricks definitely don't make code clearer or readable.

### Chaining assignments

Another interesting feature is the ability to chain assignments:

```js run
let a, b, c;

*!*
a = b = c = 2 + 2;
*/!*

alert( a ); // 4
alert( b ); // 4
alert( c ); // 4
```

Chained assignments evaluate from right to left. First, the rightmost expression `2 + 2` is evaluated and then assigned to the variables on the left: `c`, `b` and `a`. At the end, all the variables share a single value.

Once again, for the purposes of readability it's better to split such code into few lines:

```js
c = 2 + 2;
b = c;
a = c;
```
That's easier to read, especially when eye-scanning the code fast.

## Modify-in-place

We often need to apply an operator to a variable and store the new result in that same variable.

For example:

```js
let n = 2;
n = n + 5;
n = n * 2;
```

This notation can be shortened using the operators `+=` and `*=`:

```js run
let n = 2;
n += 5; // now n = 7 (same as n = n + 5)
n *= 2; // now n = 14 (same as n = n * 2)

alert( n ); // 14
```

Short "modify-and-assign" operators exist for all arithmetical and bitwise operators: `/=`, `-=`, etc.

Such operators have the same precedence as a normal assignment, so they run after most other calculations:

```js run
let n = 2;

n *= 3 + 5;

alert( n ); // 16  (right part evaluated first, same as n *= 8)
```

## Increment/decrement

<!-- Can't use -- in title, because the built-in parser turns it into a 'long dash' – -->

Increasing or decreasing a number by one is among the most common numerical operations.

So, there are special operators for it:

- **Increment** `++` increases a variable by 1:

    ```js run no-beautify
    let counter = 2;
    counter++;        // works the same as counter = counter + 1, but is shorter
    alert( counter ); // 3
    ```
- **Decrement** `--` decreases a variable by 1:

    ```js run no-beautify
    let counter = 2;
    counter--;        // works the same as counter = counter - 1, but is shorter
    alert( counter ); // 1
    ```

```warn
Increment/decrement can only be applied to variables. Trying to use it on a value like `5++` will give an error.
```

The operators `++` and `--` can be placed either before or after a variable.

- When the operator goes after the variable, it is in "postfix form": `counter++`.
- The "prefix form" is when the operator goes before the variable: `++counter`.

Both of these statements do the same thing: increase `counter` by `1`.

Is there any difference? Yes, but we can only see it if we use the returned value of `++/--`.

Let's clarify. As we know, all operators return a value. Increment/decrement is no exception. The prefix form returns the new value while the postfix form returns the old value (prior to increment/decrement).

To see the difference, here's an example:

```js run
let counter = 1;
let a = ++counter; // (*)

alert(a); // *!*2*/!*
```

In the line `(*)`, the *prefix* form `++counter` increments `counter` and returns the new value, `2`. So, the `alert` shows `2`.

Now, let's use the postfix form:

```js run
let counter = 1;
let a = counter++; // (*) changed ++counter to counter++

alert(a); // *!*1*/!*
```

In the line `(*)`, the *postfix* form `counter++` also increments `counter` but returns the *old* value (prior to increment). So, the `alert` shows `1`.

To summarize:

- If the result of increment/decrement is not used, there is no difference in which form to use:

    ```js run
    let counter = 0;
    counter++;
    ++counter;
    alert( counter ); // 2, the lines above did the same
    ```
- If we'd like to increase a value *and* immediately use the result of the operator, we need the prefix form:

    ```js run
    let counter = 0;
    alert( ++counter ); // 1
    ```
- If we'd like to increment a value but use its previous value, we need the postfix form:

    ```js run
    let counter = 0;
    alert( counter++ ); // 0
    ```

````smart header="Increment/decrement among other operators"
The operators `++/--` can be used inside expressions as well. Their precedence is higher than most other arithmetical operations.

For instance:

```js run
let counter = 1;
alert( 2 * ++counter ); // 4
```

Compare with:

```js run
let counter = 1;
alert( 2 * counter++ ); // 2, because counter++ returns the "old" value
```

Though technically okay, such notation usually makes code less readable. One line does multiple things -- not good.

While reading code, a fast "vertical" eye-scan can easily miss something like `counter++` and it won't be obvious that the variable increased.

We advise a style of "one line -- one action":

```js run
let counter = 1;
alert( 2 * counter );
counter++;
```
````

## Bitwise operators

Bitwise operators treat arguments as 32-bit integer numbers and work on the level of their binary representation.

These operators are not JavaScript-specific. They are supported in most programming languages.

The list of operators:

- AND ( `&` )
- OR ( `|` )
- XOR ( `^` )
- NOT ( `~` )
- LEFT SHIFT ( `<<` )
- RIGHT SHIFT ( `>>` )
- ZERO-FILL RIGHT SHIFT ( `>>>` )

These operators are used very rarely, when we need to fiddle with numbers on the very lowest (bitwise) level. We won't need these operators any time soon, as web development has little use of them, but in some special areas, such as cryptography, they are useful. You can read the [Bitwise Operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#Bitwise) chapter on MDN when a need arises.

## Comma

The comma operator `,` is one of the rarest and most unusual operators. Sometimes, it's used to write shorter code, so we need to know it in order to understand what's going on.

The comma operator allows us to evaluate several expressions, dividing them with a comma `,`. Each of them is evaluated but only the result of the last one is returned.

For example:

```js run
*!*
let a = (1 + 2, 3 + 4);
*/!*

alert( a ); // 7 (the result of 3 + 4)
```

Here, the first expression `1 + 2` is evaluated and its result is thrown away. Then, `3 + 4` is evaluated and returned as the result.

```smart header="Comma has a very low precedence"
Please note that the comma operator has very low precedence, lower than `=`, so parentheses are important in the example above.

Without them: `a = 1 + 2, 3 + 4` evaluates `+` first, summing the numbers into `a = 3, 7`, then the assignment operator `=` assigns `a = 3`, and the rest is ignored. It's like `(a = 1 + 2), 3 + 4`.
```

Why do we need an operator that throws away everything except the last expression?

Sometimes, people use it in more complex constructs to put several actions in one line.

For example:

```js
// three operations in one line
for (*!*a = 1, b = 3, c = a * b*/!*; a < 10; a++) {
 ...
}
```

Such tricks are used in many JavaScript frameworks. That's why we're mentioning them. But usually they don't improve code readability so we should think well before using them.

## Teoría de la información

### definición de una medida de información

Sea $E$ algún evento que ocurre con probabilidad $P(E)$. Si nos dicen que el evento $E$ ocurrió, decimos que recibimos

$$I(E) = \log\frac{1}{P(E)}$$

unidades de información.

- Si usamos base $2$, la unidad es *bits*.
- Si usamos base $e$ es *nats*.
- Si usamos base $10$ es *hartleys*
- En general, con base $r$, son *bits $r$-arios*.

Notar que, si $P(E) = 1/2$, $I(E) = 1$ bit. Es decir: $1$ bit es la cantidad de información que recibimos cuando una de dos alternativas igualmente probables se nos comunica.

### Fuentes de información de memoria nula

Un objeto que 'emite' simbolos de un alfabeto finito $S$ en base a una ley de probabilidad fija, independiente de emisiones anteriores. 

#### Entropía (memoria nula)

La cantidad de información promedio obtenida por símbolo de $S$.

$$H(S) := \sum_S P(s_i)I(s_i)$$
 
Notar que podemos pensar a $I(s_i)$ como una medida de la información necesaria para asegurar que ocurrió el evento $E$. Mientras que $H(S)$ es la cantidad promedio de incertidumbre que el observador tiene respecto al mensaje emitido por la fuente.

Se puede derivar (p. 17 del libro) que 

$$H(S) \leq \log |S| $$

donde la igualdad se mantiene si y sólo si $P(s_i) = 1/|S|$ para todo $s_i \in S$. I.e. La entropía es máxima si todos los símbolos son equiprobables.

Notar que esto implica que se requieren $|S|^2$ simbolos para duplicar la cantidad máxima de información por símbolo en la fuente.

#### Ejemplo: fuente binaria de memoria nula

Definimos $S = \{0,\ 1\}$ con $P(0) = \omega$ y $P(1) = 1 - \omega =: \bar\omega$. Luego,

$$H(S) = \omega \log\frac{1}{\omega} + (\bar\omega)\log\frac{1}{\bar\omega}$$

Observar que si $\omega = 0$ o $\omega = 1$, entonces $S$ no provee información (y está mal definido $H(S)$).

Notar también que $H(S) \leq \log(2) = 1$ bit.

#### N-ésima extensión de S

Dada una fuente de información de memoria nula $S$, su $n$-ésima extensión $S^n$ contiene $|S|^n$ simbolos, cada cual que concatena $n$ símbolos de $S$, tal que $$P(s^n_i) = \prod_{s_j \in s^n_i} P(s_j)$$

Se puede derivar (p. 21, libro) que

$$H(S^n) = nH(S)$$

### Códigos

Un código es un mapeo de todas las posibles secuencias de simbolos del *alfabeto fuente* $S$ a secuencias de simbolos de otro alfabeto $X$, el *código*.


```
codigo
/  \
    bloque
    /  \
        singular
        /  \
            univoco
            /  \
                instantaneo
```

- estas características también se pueden ver por separado.

#### Código bloque

Un código que mapea cada uno de los símbolos de $S$ a secuencias fijas de símbolos de $X$ (no necesariamente del mismo largo). Cada una se denomina una *palabra clave*. 

$$s_i \to X_i = x_{j_1}\ ...\ x_{j_k}$$

#### Códigos No singulares

Un código *bloque* es *no singular* si todas las palabras del código son distintas.

#### N-ésima extensión de un código bloque

El código *bloque* que mapea las secuencias de $n$ simbolos de la fuente $S$ a secuencias de $n$ palabras código de $X$.

#### Códigos univocamente decodificables

Un código *no singular* es únivocamente decodificable si la $n$-ésima extensión del código es *no singular* para todo $n$ finito.

Esto es, dos secuencias diferentes de símbolos del mismo largo resultan en secuencias diferentes de símbolos del código. 

Se puede demostrar (p. 49, libro) que esta condición es suficiente para garantizar que secuencias de distinto largo también resulten en códigos diferentes.

Notar que es muy útil saber cúando termina una palabra y comienza otra.

##### ejemplos: 

- un código *no singular* con palabras de largo fijo.
- un código *coma* (i.e. hay un símbolo separador) no singular.  

#### Códigos Instantáneos

Un código *univocamente decodificable* que permite decodificar cada palabra en una secuencia sin necesitar referir a símbolos posteriores.

Una condición necesaria y suficiente de esta propiedad es que no haya ninguna palabra del código que sea un prefijo de otra.

Además, instantáneo implica univocamente decodificable.

### Largo promedio de un código

Un criterio para elegir entre codificaciones posibles.

$$L_S(C) = \sum_{s\in S} P(s)\cdot|C(s)|$$

donde $C: S \to X^*$ es un código de $S$ sobre el alfabeto $X$.

#### Códigos compactos / óptimos

Aquellos códigos $C: S \to X^*$  tal que $L(C) = \min_C\{L_S(C)\}$.

Es decir, usan en promedio el menor número posible de bits para codificar un mensaje.

#### Relación con Entropía

Si la fuente es de memoria nula y el código a considerar es instantáneo, $C: S \to X^*$, se puede derivar (p. 67, libro) que

$$H(S) \leq L_S(C) \log |X|.$$

En particular, si $X$ es binario, 

$$H(S) \leq L_S(C)$$

Un código genérico $C$ que satisface esta inequación codifica *sin pérdida de información*.

Notar que la igualdad se da si y sólo si

$$I(s) = \log_{|X|} \frac{1}{P(s)} = |C(s)|$$

para todo $s \in S$.

y esto sucede si y sólo si $P(s) = 1/|X|^{|C(s)|}$ (más allá del código $C$, si el exponente es natural). 

### Canales de transmisión de memoria nula

Un Canales de transmisión de memoria nula se puede describir por medio de: 

- un alfabeto de entrada $A$
- un alfabeto de salida $B$
- un set de probabilidades condicionales $P(b/a)$ -la probabilidad de que se reciba el símbolo $b$ dado que se envío el $a$- para todo $a \in A$, $b \in B$.

#### Capacidad de carga

La capacidad $C$ de un canal es la velocidad teórica máxima de transmisión, la misma se describe como

$$C = B\cdot \log (1 + SNR)$$

donde
- $B$ es el ancho de banda (en Hz).
- $SNR$ es la tasa señal-ruido (en *veces*).
    - también expresada en Db, $SNR = 10^{Db/10}$

#### Delay

El tiempo total que tardamos en enviar información de un punto a otro

$$Delay = T_{tx}(n) + T_{prop}$$

donde:
- $T_{tx}(n) = n / V_{tx}$ es el tiempo de transmisión de $n$ bits.
- $T_{prop} = Delay / V_{prop}$ 

#### Capacidad de volumen

La cantidad de bits que entran en el medio desde que se envía el primer bit hasta que éste llega al receptor.

$$C_{vol} = Delay \cdot V_{tx}$$

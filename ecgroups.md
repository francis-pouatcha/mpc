
# Groups
An algebraic group is:
- a set with $\mathbb{S}$ with
- a binary operation $\circ$

such that the group $(\mathbb{S}, \circ)$:
- is closed: $\forall_{A,B \in \mathbb{S}}, \exists_{C \in \mathbb{S}}, A \circ B = C$
- is associative: $\forall_{A,B,C \in \mathbb{S}}, (A \circ (B \circ C))=((A \circ B) \circ C)$
- has an identity element: $\forall_{A \in \mathbb{S}}, \exists_{E \in \mathbb{S}}, A \circ E = A$
- has an inverse for each element: $\forall_{A \in \mathbb{S}}, \exists_{I \in \mathbb{S}}, A \circ I = E$ meaning that $I$ is the inverse of $A$.

A group is said to be finite if we know the number of elements of the set $\mathbb{S}$. This number is called the order of the group and writen $|\mathbb{S}|$.

## Field
A field is 
- a set $\mathbb{F}$ with
- two compatible binary operations $+, \times$

and where
- $(\mathbb{F}, +)$ is a group
- $(\mathbb{F}-\{0\}, \times)$ is a group, where $0$ is the identity element of $(\mathbb{F}, +)$
- $+$ is commutative: $\forall_{a,b \in \mathbb{F}}, a + b = b + a$
- $\times$ is commutative: $\forall_{a,b \in \mathbb{F}}, a \times b = b \times a$
- $+, \times$ are compatible: $\forall_{a,b,c \in \mathbb{F}}, a \times (b + c) = (a \times b) + (a \times c)$

## Notational Clarification
Remark that we use capital letters $A, B, E$ to represent group elements and small letters $a, b, c$ to represent field elements. This notation will be consistently applied throughout this document.

## Modular Arithmetic
- Let $\mathbb{Z}$ denote the set of integers, $\{-\infty\, \dots, -2,-1,0,1,2, \dots, +\infty\}$.
- Let $n\mathbb{Z}$ denote the set of integers divisible by $n$, where $n \in \mathbb{Z}$. For example $\mathbb{_2Z}$ is the set of all even numbers.

The notation $a \equiv b \pmod n$ means both integers $a$ and $b$ have the same remainder when divided by $n$. This means $a \sim b$ (or $a$ is equivalent to $b$) when it commes to the remainder of the division by $n$.

The equivalence calss of $\overline {a}_n$ is the set of integers $\{x \in \mathbb{Z} : a \equiv x \pmod n\}$. 

$\mathbb{Z}/n\mathbb{Z} = \{\overline {a}_n | a \in \mathbb{Z}\} = \{ \overline {0}_n, \overline {1}_n, \overline {2}_n, \dots, \overline {n-1}_n\}$ is the __set of integers modulo n__.

If $n$ is a prime number (let call it $p$), $(\mathbb{Z}/p\mathbb{Z}, +, \times)$ forms a field over the prime number $p$. We will use $\mathbb{Z_p}$ to shorten the representation of $\mathbb{Z}/p\mathbb{Z}$ in the rest of this document.

Let look deeper into the concept of a group, as the modular arithmetic allows the formation of groups that are essential for the construction of cryptographicaly relevant hardness assumptions.

## Cyclic Group
A cyclic group is a group $(\mathbb{G}, \circ)$ where each group member can be generated by applying the group operation $n$-times, $n \in (\mathbb{Z}, +, \times)$ to a single group element $G$, giving each member the representation $nG$. Recall that:
- $n$ is an element of the field $(\mathbb{Z}, +, \times)$ and
- $G$ is an element of the group $(\mathbb{G}, \circ)$.

e.g.: $G \circ G \circ G = 3G$

The group element $G$ is called the generator of the group.

For notational simplification, we will refer to the field $(\mathbb{Z}, +, \times)$ as simply $\mathbb{Z}$, and to the finite field $(\mathbb{Z}/p\mathbb{Z}, +, \times)$ as $\mathbb{Z_p}$.

## Finite Cyclic Group
This is a group $(\mathbb{G}, \circ)$ on the set $\mathbb{G}=\{E, G, 2G, 3G, \dots, (q-1)G\}$, with a finite number of elements $q \in \mathbb{Z}$, where:
- $E$ is the identity element,
- $\forall_{i \in \mathbb{Z_q}, j \in {\mathbb{Z}}}, i \equiv j \pmod q \implies iG=jG$,
- $qG=0G=E$ and
- $(-1)G = (q-1)G$ is the inverse of the generator, meaning 
  - $(1)G \circ (-1)G = (1-1)G=0G=E$ or
  - $(1)G \circ (q-1)G = (1+q-1)G=qG=E$

It turns out that $(\mathbb{G}, \circ)$ has exactly $q$ elements. The number $q$ is called the order of the generator $G$, leading to the representation $(\mathbb{G}, \circ, q, G)$.

## Prime Order Group
Let $(\mathbb{G}, \circ, q, G)$ be a group with generator $G$ of order $q$, on the binary group operation $\circ$. If $q$ is a prime number, then $(\mathbb{G}, \circ, q, G)$ is a prime order group.

### Group Operation vs. Notation
While reading scientific papers, it is essential to have a clear understanding of the term __group operation__ and the term __notation__ of that group operation.

If the group operation is the addition, the group representation generally looks like $(\mathbb{G}, +, q, G)$, where each group element can be expressed with the notation $nG$, that stands for taking $E$ and adding $G$ $n$-times to it.

If the group operation is the multiplication, the group representation generally looks like $(\mathbb{G}, \times, q, G)$, each group element can be expressed with the notation $G^n$ that stands for multiplying with $G$ $n$-times or $G$ to the power of $n$.

# Elliptic-Curves (EC)
Formally, an [elliptic curve](https://mathworld.wolfram.com/EllipticCurve.html) over a field $K$ is a nonsingular cubic curve in two variables, $f(X,Y)=0$, with a $K$-rational point (which may be a point at infinity). The field $K$ is usually taken to be the complex numbers $\mathbb{C}$, reals $\mathbb{R}$, rationals $\mathbb{Q}$, algebraic extensions of $\mathbb{Q}$, $p$-adic numbers $\mathbb{Q_p}$, or a finite field.

For the purpose of this document, let jump to the simple definition of elliptic curves (EC), which are a special types of equation with the form $y^2=x^3+ax+b$, whose elements known as points $(x, y)$. Enriched with a well defined points addition operation, they share some algebraic properties useful for the construction of cryptographic primitives.

## Elliptic-Curves Arithmetic (ECA)
The following picture display the artihmetic on elliptic curves:

![EC Aritmetic](./img/ECClines.svg)

This picture defines following assuptions:

__ECA-0__: defines an imaginary point $O$ on the curve so that $\forall_{P \in \mathbb{E}}, P + O = P$, and calls it the __Point at Infinity__.

__ECA-1__: On an elliptic curve, a strait line can cross up to $3$ points $P, Q, R$. ECA defines the sum of those three points to be $O$, means $P + Q + R = O$.

__ECA-2__: If a strait line crosses only two points $P, Q$, and is tangent to $Q$, ECA assumes it crosses $Q$ two times and defines $P + Q + Q = O$.

__ECA-3__: If a line crosses only two points $P, Q$, and is neither tangent to $P$ nor to $Q$, ECA assumes it crosses the third imaginary point $O$ and defines $P + Q + O = O$.

__ECA-4__: If a line line crosses only one point $P$, then that line is tangent to the curve at $P$. ECA assumes that line crosses $P$ twice and crosses the imaginary point $O$ and ECA defines $P + P + O = O$.

Based on the assumption above, following arithmetic operation can be implemented on elliptic-curves.

### Additive Inverse
Based on ECA-3, the inversion of a point can be defined as the reflection of the point over the $x$ axis. Means the inverse of the point $P=(x_p, y_p)$ is the point $Q = -P=(x_p, -y_p)$.
$$P+Q+O=O \implies Q=-P$$

Based on ECA-4, if the point $P$ is tangent to the curve at $x_p=0$, then the point $P$ is its proper inverse, leading to: 
$$P + P + O = O \implies P = -P$$

### Addition
Based on ECA-1, each strait line touching $3$ distinct points $P, Q, R$ defines the addition of two distinct points, such that:
$$P + Q + R = O \implies P + Q = -R$$

where $-R$ is the inverse of $R$.

### Doubling
Based on ECA-2, a strait line tangent at point $Q$ and crossing a second point $P \ne O$, produces the doubling of $Q$, such that:
$$P + Q + Q = O \implies Q + Q = 2Q = -P$$

## Finite Groups over Elliptic-Curve
With the addition operation and the additive inverse defined above, the ECA allows the construction of finite groups over elements of an elliptic curve.

The ECA allows the construction of the relation $\mathbb{Z_q}$ x $\mathbb{E} \implies \mathbb{E}$, where for a point $P \in \mathbb{E}$ and a number $n \in \mathbb{Z_q}$, the point $Q=nP \in \mathbb{E}$ can be generated, where $\mathbb{Z_q}$ is a finite field $(\mathbb{Z}, +, \times, q)$ of order $q$.

Therefore, from a generator point $G$, ECA allows the construction of finite cyclic groups on an elliptic curve $(\mathbb{E}_{(\mathbb{Z_q})}, +, p, G)$, where 
- $+$ is the points addition operation defined above, including the additive inverse and the identity element at $O$, 
- $G$ is the generator point,
- $p$ is the order of the group generator $G$, or the number of points on curve $\mathbb{E}$ that can be generated from $G$,
- $\mathbb{Z_q}$ is the field of integers of order $q \in \mathbb{Z}$ such that $\forall_{P=(x_p,y_p)}, \forall_{Q=nP=(x_q, y_q)}, x_p, y_p, n, x_q, y_q \in \mathbb{Z_q}$. With this, we mean not only the number of operation $n$, but also all point coordinates $x$ and $y$ have to be elements of $\mathbb{Z_q}$. This means $q$ is used to keep the computation of group elements in bounds.

Let 
- $n \in \mathbb{Z_q}$ and 
- $G \in \mathbb{E_{(\mathbb{Z_q})}}$, then 
- $nG = P \in \mathbb{E_{(\mathbb{Z_q})}}$ stands for the $n$-times addition of the point $G$ to the identity element, or $nG = O \circ_{1} G \circ_{2} G \dots \circ_{n-1} G \circ_{n} G$

The group property of elliptic-curves allows the statement like: 
- $nG + mG = (n + m)G$ and 
- $n(mG) = (n \times m)G$

The first statement $nG + mG = (n + m)G$ tell us that, knowing the point $nG$ and $mG$, we can compute $(n+m)G$, without knowing neither $n$ nor $m$.

The second statement $n(mG) = (n \times m)G$ tell us that: knwoing the scalar $n$ and the point $mG$, we can compute the point $(n \times m)G$ without having to know $m$.

# EC based Hardness Assumption
## Elliptic-Curve Discrete Log Problem (ECDLP)
Working on the cyclic, finite, additive elliptic-curve group $(\mathbb{E}_{(\mathbb{Z_q})}, +, p, G)$, and given a point $Q \in \mathbb{E}$, it is hard to find the number $n$ such that $Q=nG$. Means it is hard to compute how many times we have to add the point $G$ to itself to get to the point $Q$.

Following integer arithmetic, we would say $G = {1 \over n} Q = mQ$ where $m={1 \over n}$ is the additive inverse of $n$ in $\mathbb{Z_q}$. If $n$ is unknown, there is no easy way to find $m$ without just incrementally adding $Q$ to itself.

## Elliptic-curve Diffie–Hellman Assumption (ECDH)
ECDH is built on top of the ECDLP and assumes that:
- given the group $(\mathbb{E}_{(\mathbb{Z_q})}, \circ, p, G)$, where $O$ is the identity element, and 
- given two group elements $aG$ and $bG$,
- it is hard to compute $(a \times b)G$, without knowing either $a$ or $b$.

For example: 
- Alice randomly selects a number $a \in \mathbb{Z_q}$, computes and sends the group element $aG$ to Bob, and
- Bob randomly selects a number $b \in \mathbb{Z_q}$, computes and sends the group element $bG$ to Alice, 
- Alice compute $S = O \circ_{1} bG, \dots, \circ_{a-1} bG \circ_{a} bG$, where $\circ_{i}$ stands for the $i^{th}$ application of $bG$ to the cummulative result,
- Bob compute $S = O \circ_{1} aG, \dots, \circ_{b-1} aG \circ_{b} aG$, where $\circ_{j}$ stands for the $j^{th}$ application of $G$ to the cummulative result,
- Alice and Bob would have applied $G$ to the initial identity element $(a \times b)$-times and will both obtain the same group element $(a \times b)G$.

For disambiguation:
  - recall that $(a \times b)G = a(bG) = b(aG)$ (see below), 
  - recall $a, b \in \mathbb{Z_q}$, results to $(a \times b) \in \mathbb{Z_q}$, as $\mathbb{Z_q}$ is a field, so $(a \times b)G$ is an element of the group,
  - recall is it easy to compute $(a+b)G = aG + bG$, as it is a simple point addition (EC points in this case), but this is not the subject of the hardness assumption.

Knowing $aG$ and $bG$, any other person will have to factorize $a$ from $aG$ or $b$ from $bG$ to gain access to a computation of $(a \times b)G$. Recall again that computing $(a+b)G = aG + bG$ will disclose no futher information on the values of $a, b$ or $(a \times b)$ or $(a + b)$.

## N-Parties ECDH
Recall that ECDH can be extended to run among $n$ parties with $n-1$ with $n-1$ communication rounds. E.g.: $aG, bG, cG$ are sent around. Then $(a \times b)G, (b \times c)G, (a \times c)G$ are sent arround. Finally all parties can compute $(a \times b \times c)G$.

# Elliptic-Curve Domain Parameter
EcDSA, EdDSA (all valiants of [DSA](https://en.wikipedia.org/wiki/Digital_Signature_Algorithm)), some Schnorr signatures (like BIP340), are all built on top of ECDLP.

They are all based on the [cyclic, finite, additive elliptic-curve groups](./cha.md#finite-groups-over-elliptic-curve) $(\mathbb{E}_{(\mathbb{F_q})}, +, p, G)$, where:
- $\mathbb{E}_{(\mathbb{F_q}})$ represent a set of points $P=(x_p, y_p)$ on the elliptic curve $E$,
- $+$ is the points addition operation, including the additive inverse and the neutral element $O$ (point at infinity), 
- $G$ is the generator point, all points of the group can be computed by multiplying this point by a scalar number $n \in \mathbb{F_q}$,
- $\mathbb{F_q}$ is the field of order $q \in \mathbb{Z}$, such that $\forall_{P=(x,y)}, \forall_{Q=nP}, x, y, n \in \mathbb{F_q}$. This means all point coordinates and all scalar numbers used to produced group elements are element of $\mathbb{F_q}$,
- $p$ is the order of the generator $G$, or the number of points so that $\forall_{n \in \mathbb{F_q}}, nG \in \mathbb{E}_{(\mathbb{F_q})}$.

For the construction of cryptographic primitives, special secure curves have to be defined. Elliptic-curve construction distinguishes between prime case and binary case curves.

## Binary Case Elliptic-Curves
In the binary case, the elliptic-curve group $(\mathbb{E}_{(\mathbb{F_{2^m}})}, +, n, G)$ can be defined using the notation $(m,f,a,b,G,n,h)$ where:
- $m$ is the extension of the field $\mathbb{F_{2^m}}$. E.g $\mathbb{F_{2^8}}$ or $\mathbb{F_{256}}$ is used to implement AES,
- $f$ is the auxiliary curve, and
- other parameters have a similar definition to primary case curves bellow.

## Prime Case Elliptic-Curves
In the prime case, the elliptic-curve group $(\mathbb{E}_{(\mathbb{F_p})}, +, n, G)$ can be defined using the notation $(p,a,b,G,n,h)$ where:
- $p$ is a large prime and the order of the field $\mathbb{F_p}$ (number of elements in $\mathbb{F_p} \texttt{ or } |\mathbb{F_p}|$),
- $\mathbb{F_p}$ is the field of order $p \in \mathbb{Z}$, such that $\forall_{P=(x_p,y_p)}, \forall_{Q=nP=(x_q, y_q)}, x_p, y_p, n, x_q, y_q \in \mathbb{F_q}$,
- $a, b$ are the parameters of the curve equation $y^2= x^3 + ax + b$ (known as Weierstrass form),
- $G$ is the generator point,
- $n$ is the order of the point $G$, meaning that the smallest number $k \in \mathbb{F_p}$ such that $kG = O$,
- $h$ the cofactor, given $h={1 \over n}|\mathbb{E_{(\mathbb{F_p})}}|$. h is used to limit subgroup of points on which to operate, for some security reasons e.g: [Pohlig–Hellman algorithm](https://en.wikipedia.org/wiki/Pohlig%E2%80%93Hellman_algorithm) on curve25519.

## Sample Prime Case Curve secp256k1
An example is the curve used by bitcoin is secp256k1 and has follwoing parameters:
- $p = \texttt{FFFFFFFF FFFFFFFF FFFFFFFF FFFFFFFF FFFFFFFF FFFFFFFF FFFFFFFE FFFFFC2F}$
- This is $2^{256} - 2^{32} - 2^9 - 2^8 - 2^7 - 2^6 - 2^4 -1$

The curve equation $y^2= x^3 + ax + b$ over $\mathbb{F_p}$ is defined by $y^2=x^3 + 7$, meaning:
- $\texttt{a = 00000000 00000000 00000000 00000000 00000000 00000000 00000000 00000000}$
- $\texttt{b = 00000000 00000000 00000000 00000000 00000000 00000000 00000000 00000007}$

The generator point $G$ in uncompressed form is:
- $\texttt{G = 04 79BE667E F9DCBBAC 55A06295 CE870B07 029BFCDB 2DCE28D9 59F2815B 16F81798 483ADA77 26A3C465 5DA4FBFC 0E1108A8 FD17B448 A6855419 9C47D08F FB10D4B8
}$

The generator point $G$ in compressed form is:
- $\texttt{G = 02 79BE667E F9DCBBAC 55A06295 CE870B07 029BFCDB 2DCE28D9 59F2815B 16F81798}$

Recall that the compressed representation of a curve point only provides the $x\text{-coordinate}$ and the indication of the sign of the $y\text{-coordinate } \mathtt{0x02} \text{ or } \mathtt{0x03}$ (least significant bit). As the $y\text{-coordinate}$ can be computed using the curve equation $y=E(x)$.

The order $n$ of the generator $G$ is the number of points in the group $(\mathbb{E}_{(\mathbb{F_p})}, +, n, G)$ that can be generated from $G$, and is:
- $\text{n = FFFFFFFF FFFFFFFF FFFFFFFF FFFFFFFE BAAEDCE6 AF48A03B BFD25E8C D0364141}$

It is the smalles number $n \in \mathbb{F_q}$ such that $nG=O$.

The cofactor $h$ defines the subgroup $\mathbb{S_{r}}$ of prime order $r= { n \over h}$. Meaning for each element $kG$ of the subgroup, $k$ is a multiple of $h$. In case of secp256k1:
- $h=01$. Means all points of the group can be used.

secp256k1 is the foundation of the bitcoin EcDSA and BIP340 (Schnorr Signature).

## Sample Prime Case Curve with non Trivial Cofactor curve25519
An elliptic-curve with a non trivial cofactor is the Montgomery curve [curve25519](https://en.wikipedia.org/wiki/Curve25519), with following properties:
- curve equation $y^2 = x^3 + 486662x^2 + x$. Recall that montgomry curves have the general equation $M_{A,B}: By^2 = x^3 + Ax^2 + x$ over $\mathbb{F_q}$, where $A,B \in \mathbb{F_q} \text{ and } B(A^2 -4) \ne 0$,
- curve25519 uses the generator point at $x=9$ and a cofactor $h=8$ to generate a cyclic group with prime order $p = 2^{252} + 27742317777372353535851937790883648493$.

Using a subgroup in this case prevents the [Pohlig–Hellman algorithm](https://en.wikipedia.org/wiki/Pohlig%E2%80%93Hellman_algorithm) attack. 
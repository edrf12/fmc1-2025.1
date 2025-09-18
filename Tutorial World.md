
## The rfl tactic

Nesse nível aprendemos como usar a tática `rfl`, a qual chamamos nas aulas de `Refl` (Reflexividade)

Nesse nível nossa prova é somente:

```
rfl
```

Provando que `37x + q = 37x + q`

Traduzindo para a linguagem que estamos usando nas aulas:

```
Θ Demonstre: (∀x : Int)(∀q : Int)[37x + q = 37x + q]

Demons.

Sejam x, q : Int
Calculamos:
37x + q
		= 37x + q
∎
```

## The rw tactic

Nesse nível aprendemos como usar a tática `rw`, a qual chamamos nas aulas de `Subst`

Prova:

```
rw [h]
rfl
```

Sendo `h : y = x + 7`
`rw [h]` substitui `y` por `x + 7` no teorema
`rw [← h]` substitui `x + 7` por `y` no teorema

## Numbers

Nesse nível apenas fazemos uso das táticas que já possuímos, tendo 4 novos teoremas válidos `one_eq_succ_zero`, `two_eq_succ_one`, `three_eq_succ_two`, `four_eq_succ_three`, com os quais temos agora a definição de 1, 2, 3 e 4.

Prova:

```
rw [two_eq_succ_one]
rw [one_eq_succ_zero]
rfl
```

## Rewriting backwards

Nesse nível é simplesmente apresentado o que eu já havia percebido anteriormente lendo a descrição do comando `rw`, é possível usar ← para reescrever de forma contrária.

Prova:

```
rw [← one_eq_succ_zero]
rw [← two_eq_succ_one]
rfl
```

Provamos então o teorema do nível anterior de maneira contrária

## Adding zero

Nesse nível nos é disponibilizado o teorema `add_zero`, o qual chamamos nas aulas de `(+).1`

Prova:

```
repeat rw [add_zero]
rfl
```

Ou com nossa linguagem:

```
Θ Demonstre: (∀a, b, c : Int)[a + (b + 0) + (c + 0) = a + b + c]

Demons.

Sejam a, b, c : Int
Calculamos: 
a + (b + 0) + (c + 0)
					= a + b + (c + 0) [(+).1 b]
					= a + b + c [(+).1 c]
∎

```

## Precision Rewriting

Nesse nível é ensinado que podemos fornecer uma variável para `rw` se quisermos reescrever uma parte específica do teorema que não seja a primeira

Prova:

```
rw [add_zero c]
rw [add_zero]
rfl
```

## add_succ

Nesse nível nos é apresentado `add_succ`, ou como chamamos em sala `n + succ m = succ(n + m) (+).2`
Além disso, provamos que `succ n = n + 1`, um dos *homeworks*!

Prova:

```
rw [one_eq_succ_zero]
rw[add_succ]
rw[add_zero]
rfl
```

Ou com nossa linguagem:

```
Θ Demonstre: (∀n : Int)[S n = n + 1]
Seja n : Int
Calculamos 
n + 12
     ≡ n + S 0
	 = S (n + 0) [(+).2]
	 = S n
Imediato.
∎
```

## 2 + 2 = 4

Nesse nível temos que demonstrar que `2 + 2 = 4`
Também nos é apresentado o comando `nth_rewrite n [h]`, que reescreve a n-ésima ocorrência por h.

Prova, trocando `4` por `succ(succ(2))`:

```
nth_rewrite 2 [two_eq_succ_one]
rw [one_eq_succ_zero]
repeat rw [add_succ]
rw [add_zero]
rw [four_eq_succ_three]
rw [three_eq_succ_two]
rfl
```

Prova, trocando `2 + 2` por `4`:

```
nth_rewrite 2 [two_eq_succ_one]
rw [add_succ]
rw [one_eq_succ_zero]
rw [add_succ]
rw [add_zero]
rw [← three_eq_succ_two]
rw [← four_eq_succ_three]
rfl
```
# S.O.L.I.D

Conjunto de princípios que auxiliam o dev a criar código orientado a objetos de uma forma mais sustentável, flexível e compreensível.

Mas antes de entrar nos detalhes de cada princípio, temos que entender quais são as características de um código mal feito e multiplicar por -1 pra entender os problemas que o SOLID ajuda a resolver. Também temos que entender o que é OOP. Apesar de estar presente no nosso dia-dia, às vezes esquecemos os conceitos que compõem a mesma.

## BAD CODE

### Rigidity

> When you touch the code and you must now modify massive amounts of other code to come back into consistency with this modification you made - Uncle Bob

### Fragility

> Tendency of the code to break in many places even when you only change it in one place - Uncle Bob

### Immobility

Inability to reuse software from other parts of the system.

## OOP

> You may have heard that OO is modeling the real world. Nonsense - Uncle Bob

> You may have heard that OO is closer to the way we think. :thumbsdown: - Uncle Bob

Para uma linguagem ser orientada a objetos, ela deve suportar **Herança**, **Encapsulamento**, **Abstração** e **Polimorfismo**. Para os fins dessa talk, destaca-se o **polimorfismo**.

> O polimorfismo é caracterizado quando duas ou mais classes distintas têm métodos de mesmo nome, de forma que uma função possa utilizar um objeto de qualquer uma das classes polimórficas, sem necessidade de tratar de forma diferenciada conforme a classe do objeto

Em linguagens fortemente tipadas conseguimos realizar o polimorfismo através de **herança**, já em linguagens dinamicamente tipadas temos o conceito de **Duck Typing** que desburocratiza bastante esse processo.

<img src="https://pics.me.me/duck-typing-duck-typing-2429782.png" width="300" height="300" alt="Duck Typing"/>

# Disclaimer

Os princípios não compõem um mantra, portanto não se deve buscar o atingimento de todos obrigatoriamente. Há casos e linguagens em que a implementação de alguns dos princípios não é justificável, ou mesmo possível. Use-os a seu favor para construir um software mais robusto, mas sempre de olho no over engineering.
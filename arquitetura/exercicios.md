# Arquitetura de Software: Exercícios

**Disciplina:** Engenharia de Software II
**Professor:** Mehran Misaghi · IFC Campus Araquari

> **Nesta série:** [1. Fundamentos](01-fundamentos.md) · [2. Camadas](02-camadas.md) · [3. MVC](03-mvc.md) · [4. Microsserviços](04-microsservicos.md) · [5. Comunicação assíncrona](05-comunicacao-assincrona.md) · [6. Anti-padrões e evolução](06-antipadroes-e-evolucao.md) · **Exercícios**

Resolva os exercícios antes de consultar o [gabarito](gabarito.md). Ao lado de cada bloco está a página das notas que trata do assunto.

---

## Fundamentos ([página 1](01-fundamentos.md))

**1.** Apresente as duas definições de arquitetura de software vistas em aula e dê um exemplo de decisão arquitetural difícil de reverter.

**2.** Um módulo de persistência é sempre parte da arquitetura? Justifique com um exemplo.

**3.** *(POSCOMP 2019, adaptada)* Marque V (verdadeiro) ou F (falso):

- ( ) No MVC, o Controller fica entre View e Model e concentra as regras de negócio.
- ( ) O padrão Broker media clientes e servidores em ambientes distribuídos, desacoplando-os.
- ( ) Um padrão pode resolver o problema e ainda assim não ser adequado ao contexto.

**4.** Que lição sobre decisões arquiteturais podemos tirar do debate Tanenbaum × Torvalds (1992–2009)?

---

## Camadas ([página 2](02-camadas.md))

**5.** Num sistema acadêmico em três camadas, indique em qual camada fica cada responsabilidade:

| Responsabilidade | Camada |
|---|---|
| (a) Formulário de lançamento de notas | |
| (b) Validar que a nota está entre 0 e 10 | |
| (c) Enviar e-mail ao aluno após o lançamento | |
| (d) Gravar a nota | |

**6.** Compare as arquiteturas de duas e três camadas, apontando uma vantagem e uma desvantagem de cada.

---

## MVC ([página 3](03-mvc.md))

**7.** Descreva três vantagens da arquitetura MVC.

**8.** Qual a diferença entre o papel do Controller no MVC clássico (Smalltalk) e em um framework Web como Rails ou Django?

**9.** Explique a diferença entre uma aplicação web tradicional (MPA) e uma SPA. Por que o Gmail precisa de comunicação assíncrona com o servidor?

---

## Microsserviços ([página 4](04-microsservicos.md))

**10.** Descreva quatro vantagens dos microsserviços em relação a um monolito.

**11.** Uma startup com 4 desenvolvedores quer começar seu produto já com 12 microsserviços. Que riscos você apontaria? Use pelo menos três desvantagens vistas em aula.

**12.** Enuncie a Lei de Conway e explique sua relação com microsserviços.

---

## Comunicação assíncrona ([página 5](05-comunicacao-assincrona.md))

**13.** Explique desacoplamento no espaço e no tempo. Num e-commerce, quando usar uma fila e quando usar pub/sub para o evento “pedido confirmado”?

---

## Anti-padrões e evolução ([página 6](06-antipadroes-e-evolucao.md))

**14.** O que caracteriza o anti-padrão big ball of mud? Relacione-o com o ciclo vicioso da dívida técnica arquitetural.

**15.** Você deve extrair o módulo de pagamentos de um monolito de e-commerce usando Strangler Fig. Que decisões precisa tomar quanto à comunicação e ao banco de dados?

---

**Respostas sugeridas:** [gabarito](gabarito.md)

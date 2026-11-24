# Refactoring: Exercícios

**Disciplina:** Engenharia de Software II
**Professor:** Mehran Misaghi · IFC Campus Araquari

> **Nesta série:** [1. Introdução](01-introducao.md) · [2. Catálogo](02-catalogo.md) · [3. Prática](03-pratica.md) · [4. Code smells](04-code-smells.md) · [5. Dívida técnica](05-divida-tecnica.md) · **Exercícios** · [Gabarito](gabarito.md)

Os exercícios 1 a 10 são adaptados dos exercícios de fixação do [Capítulo 9 do livro *Engenharia de Software Moderna*](https://engsoftmoderna.info/cap9.html).

---

## Bloco A: Conceitos

**1.** Qual das alternativas abaixo **não** é um benefício esperado de refactorings? Justifique.

- (a) Melhorar o design do sistema.
- (b) Tornar o código mais fácil de ler e entender.
- (c) Facilitar a localização de bugs.
- (d) Melhorar o desempenho do sistema em tempo de execução.
- (e) Permitir que novas funcionalidades sejam implementadas mais rapidamente.

**2.** Imagine um gráfico com o número acumulado de funcionalidades entregues por dois sistemas, A e B, ao longo de 24 meses. No sistema A, a curva cresce quase em linha reta. No sistema B, a curva cresce rápido no início e depois fica cada vez mais achatada. Em qual dos dois sistemas é mais provável que tenham sido feitos refactorings de forma sistemática? Relacione sua resposta com as Leis de Lehman.

**3.** Qual a diferença entre refactorings **oportunistas** e **planejados**? Qual dos dois deve ser mais comum? Por quê?

**4.** Dê dois exemplos de pares de refactorings A e B em que **B reverte A**, ou seja, aplicar A e depois B devolve o código ao estado original.

**5.** Por que testes de unidade são importantes para a prática de refactoring? O que tende a acontecer em um sistema sem testes?

---

## Bloco B: Aplicando refactorings

**6.** Aplique **Extração de Método** nos trechos abaixo, extraindo as linhas marcadas com `// extrair` para um método `g`. Indique os parâmetros e o retorno de `g`.

```java
// (a)
void f() {
  int x = 10;
  x++;                       // extrair
  System.out.println(x);     // extrair
}

// (b)
void f() {
  int x = 10;
  x++;                       // extrair
  System.out.println(x);     // extrair
  int y = x + 1;
}

// (c)
void f() {
  int x = 10;
  int y;                     // extrair
  y = h() * 2;               // extrair
  System.out.println(y);     // extrair
  int z = y + 1;
}
```

**7.** Considere a classe a seguir. Qual code smell ela apresenta? Proponha um refactoring e mostre como ficaria o código.

```java
class Pedido {
  String rua;
  String numero;
  String cidade;
  String cepEntrega;
  String ruaCobranca;
  String numeroCobranca;
  String cidadeCobranca;
  String cepCobranca;
  double valor;
  ...
}
```

**8.** Reescreva o trecho abaixo usando **Remoção de Flags**:

```java
int posicao(String[] nomes, String alvo) {
  int pos = -1;
  boolean fim = false;
  int i = 0;
  while (!fim && i < nomes.length) {
    if (nomes[i].equals(alvo)) {
      pos = i;
      fim = true;
    }
    i++;
  }
  return pos;
}
```

---

## Bloco C: Code smells

**9.** Considere a função recursiva abaixo, que calcula o n-ésimo termo da sequência de Fibonacci. **Descreva** (não precisa implementar) um clone de cada tipo (1, 2, 3 e 4) para ela.

```java
int fib(int n) {
  if (n == 1) return 1;
  if (n == 2) return 1;
  return fib(n-1) + fib(n-2);
}
```

**10.** Considere a classe `Moeda`:

```java
class Moeda {
  private double valor = 0.0;

  void add(Moeda m) {
    this.valor = this.valor + m.getValor();
  }

  double getValor() {
    return valor;
  }
}
```

- (a) Por que objetos dessa classe são **mutáveis**?
- (b) Reimplemente a classe de forma que seus objetos sejam **imutáveis**.

**11.** Por que os comentários da classe abaixo são desnecessários? Que tipo de comentário seria útil nela?

```java
// classe Aluno
class Aluno {
  // matrícula do aluno
  int matricula;
  // nome do aluno
  String nome;

  // construtor da classe Aluno
  Aluno(int matricula, String nome) { ... }
}
```

---

## Bloco D: Prática com IDE

**12.** Em uma IDE de sua escolha (IntelliJ, Eclipse ou VS Code), reproduza o exemplo de Steimann e Thies da [página 3](03-pratica.md#verificação-de-pré-condições): crie os pacotes `P1` e `P2`, as classes `A` e `B`, e use o refactoring automatizado de **mover classe** para levar `B` de `P1` para `P2`.

- (a) A IDE alertou sobre a mudança de comportamento?
- (b) Execute o programa antes e depois. Qual método `m` é chamado em cada caso?
- (c) Essa operação é um refactoring? Justifique.

---

**Página anterior:** [← 5. Dívida técnica](05-divida-tecnica.md) · **Próxima:** [Gabarito →](gabarito.md)

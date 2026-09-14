---
title: 'UML'
description: 'UML'
permalink: uml.md
---

## Notas de Aula — UML (Unified Modeling Language)


>Baseado em: **Slides da aula**  e no livro **Engenharia de Software Moderna** (Marco Tulio Valente, UFMG) — Capítulo 4: Modelos https://engsoftmoderna.info/cap4.html
---

## 1. Por quê usar modelos?

Existe uma **lacuna (gap)** entre dois mundos:

- **Requisitos** → descrevem *o que* o sistema faz (nível de abstração alto).
- **Código** → descreve *como* o sistema faz isso (nível de abstração baixo).

Os **modelos de software** servem para preencher essa lacuna: são mais detalhados que requisitos, porém mais simples que o código-fonte completo.

> "Todos os modelos estão errados, mas alguns são úteis." — George Box

Modelos são comuns em outras engenharias (ex.: maquetes e modelos matemáticos de pontes em Engenharia Civil), mas em Engenharia de Software eles são **menos efetivos**, porque, ao abstrair detalhes, acabam descartando parte da complexidade que é **essencial** ao sistema (Frederick Brooks, *Não Existe Bala de Prata*).

Modelos de software podem ser:

- **Formais** — usam notação matemática (lógica, teoria dos conjuntos, Redes de Petri). Permitem provar propriedades do sistema antes da implementação, mas são pouco usados na prática (exceto em sistemas de missão crítica).
- **Gráficos** — a **UML** é a notação gráfica mais usada.

---

## 2. UML: Unified Modeling Language

- Proposta em **1995**, fruto da unificação de notações criadas de forma independente por três engenheiros de software: **Grady Booch, Jim Rumbaugh e Ivar Jacobson**.
- Surgiu no contexto do modelo **Waterfall** (anos 80), quando havia uma grande fase de *design* antes da codificação.
- Em **1997**, tornou-se padrão gerenciado pela **OMG** (Object Management Group).
- Surgiram também as **ferramentas CASE** (*Computer-Aided Software Engineering*), equivalentes às ferramentas CAD usadas em outras engenharias.

### 2.1 Como usar UML? (classificação de Martin Fowler)

Martin Fowler (livro *UML Distilled*) propõe três formas de uso da UML:

| Uso | Descrição | Quando é usado |
|---|---|---|
| **Blueprint** (planta técnica) | Modelos detalhados e completos, criados antes da codificação e repassados a programadores | Processos Waterfall / Processo Unificado (UP) |
| **Linguagem de programação** | Geração automática de código a partir dos modelos (*Model Driven Development* — MDD) | Pouco usado na prática; tornou UML "pesada" |
| **Sketch (esboço)** | Diagramas leves e informais, usados para comunicação entre desenvolvedores | **Métodos ágeis** — é o uso que estudamos nesta disciplina |

**UML como esboço** é usada em duas situações:

- **Engenharia Avante (*Forward Engineering*)**: o modelo é usado para discutir e validar alternativas de projeto **antes** de existir qualquer código.
- **Engenharia Reversa (*Reverse Engineering*)**: o modelo é usado para **explicar um código já existente** (ex.: manutenção, ajudar um novo desenvolvedor a entender o sistema).

> Dado real (pesquisa com 394 desenvolvedores, Baltes & Diehl, 2013): 48% dos esboços continham algum elemento de UML, mas apenas 9% eram integralmente baseados em UML — reforçando o uso de UML como notação parcial e informal, não como blueprint.

### 2.2 Tipos de diagramas UML

UML classifica seus diagramas em dois grandes grupos:

- **Diagramas Estáticos (estruturais)** — modelam a **estrutura** do sistema (classes, atributos, métodos, pacotes). Não mudam durante a execução.
  - Diagrama de Classes
  - Diagrama de Pacotes
- **Diagramas Dinâmicos (comportamentais)** — modelam a **execução/comportamento** do sistema. Podem variar a cada execução.
  - Diagrama de Sequência
  - Diagrama de Atividades
  - (Diagrama de Casos de Uso, visto no capítulo de Requisitos)

**Versão de UML estudada:** a adotada no livro *UML Distilled* (3ª edição), de Martin Fowler — um subconjunto pequeno da versão 2.0/2.5.1 da UML (que, na íntegra, possui quase 800 páginas de especificação).

---

## 3. Diagrama de Classes

O diagrama mais usado da UML. Representa classes, atributos, métodos e os relacionamentos entre elas.

### 3.1 Estrutura básica

Cada classe é um retângulo com **três compartimentos**:

```
┌───────────────┐
│   NomeClasse   │
├───────────────┤
│  - atributo1   │
│  - atributo2   │
├───────────────┤
│  + metodo1()   │
│  + metodo2()   │
└───────────────┘
```

### 3.2 Visibilidade

| Símbolo | Significado |
|---|---|
| `+` | público (*public*) |
| `-` | privado (*private*) |

*(Em esboços informais, esses símbolos podem ser omitidos — não é preciso rigor sintático total.)*

### 3.3 Relacionamentos entre classes

UML define três tipos principais de relacionamento em diagramas de classes:

#### a) Associação

Quando uma classe **A** possui um atributo `b` do tipo **B**, existe uma associação de A para B, representada por uma **seta contínua** de A para B, com o nome do atributo próximo à ponta.

```java
class A {
   private B b;
}
class B { }
```

- **Multiplicidade**: indica quantos objetos podem participar da associação.
  - `1` → exatamente um objeto
  - `0..1` → zero ou um objeto
  - `*` → zero ou mais objetos
- Uma associação pode ser **unidirecional** (uma seta) ou **bidirecional** (seta em ambas as pontas — quando é preciso "navegar" nos dois sentidos).

Exemplo: `Pessoa` (0..1) —— `fone` ——> (*) `Fone`
Significa: uma Pessoa tem no máximo um Fone; um Fone pode pertencer a várias Pessoas.

> **Composição e agregação**: são variações do conceito de associação frequentemente citadas (composição = a classe "parte" não existe sem o "todo"; agregação = ciclos de vida independentes). O livro-texto recomenda **não se aprofundar demais nessa distinção**, pois ela costuma gerar confusão — inclusive Fowler considera o conceito de agregação praticamente sem utilidade prática nos esboços do dia a dia.

#### b) Herança

Representada por uma **seta contínua com ponta vazada (triangular)**, apontando da subclasse para a superclasse.

```
PessoaFisica ──▷ Pessoa ◁── PessoaJuridica
```

Subclasses herdam atributos/métodos da superclasse e podem adicionar membros próprios (ex.: `PessoaFisica` tem `cpf`; `PessoaJuridica` tem `cnpj`).

#### c) Dependência

Representada por uma **seta tracejada**. Existe quando a classe A usa a classe B, mas **não** por associação (atributo) nem herança — por exemplo, quando um método de A recebe um parâmetro do tipo B, declara uma variável local do tipo B, ou lança uma exceção do tipo B.

```java
class MinhaClasse {
   void metodoX() {
      Stack stack = new Stack(); // dependência para java.util.Stack
   }
}
```

Pode-se anotar o **tipo de dependência** entre `<<` e `>>`, como `<<create>>` (instanciação) ou `<<call>>` (chamada de método).

### 3.4 Resumo visual dos relacionamentos

| Relacionamento | Tipo de seta | Significado |
|---|---|---|
| Associação | Contínua, ponta simples | "tem um atributo do tipo" |
| Herança | Contínua, ponta triangular vazada | "é um subtipo de" |
| Dependência | Tracejada | "usa temporariamente" (parâmetro, variável local, exceção) |

---

## 4. Diagrama de Pacotes

Usado para dar uma visão de **mais alto nível**, agrupando classes em **pacotes** e mostrando as dependências entre esses pacotes.

- Representado por um retângulo com uma "aba" no topo (formato de pasta/trapézio), contendo apenas o **nome do pacote**.
- Único tipo de seta: **tracejada**, representando qualquer relação (associação, herança ou dependência) entre os pacotes agrupados.
- Dependências entre pacotes **não** indicam quantas classes internas estão envolvidas — mesmo uma única classe de P1 usando uma única classe de P2 já caracteriza uma dependência de P1 para P2.

Exemplo típico (visto em aula): sistema com pacotes `MobileView`, `WebView`, `BusinessLayer` e `Persistence`, em que as Views dependem de `BusinessLayer` (e vice-versa, para notificações), e apenas `BusinessLayer` depende de `Persistence`.

---

## 5. Diagrama de Sequência

Diagrama **dinâmico/comportamental**: modela **objetos** (não classes) e as chamadas de método entre eles ao longo do tempo, em um cenário específico.

### 5.1 Notação

- Cada **objeto** é um retângulo no topo do diagrama.
- Abaixo de cada objeto, uma **linha de vida vertical**:
  - **Tracejada** → objeto inativo (nenhum método em execução).
  - **Retângulo estreito (barra de ativação)** → um método do objeto está em execução.
- **Chamada de método**: seta horizontal contínua, com o nome do método.
- **Retorno de método**: seta tracejada (frequentemente **omitida**, quando o método é `void` ou o retorno não é relevante para a explicação).

> "Algumas pessoas usam setas de retorno para todas as chamadas, mas prefiro usá-las apenas quando adicionam informação; caso contrário, elas só poluem o diagrama." — Martin Fowler

### 5.2 Chamadas internas (this)

Quando um objeto chama um método de si mesmo (ex.: `f()` chama `g()` internamente), isso é representado por uma nova barra de ativação que "nasce" da barra do método chamador.

### 5.3 Exemplo típico

Cenário de caixa eletrônico: cliente solicita um saque/depósito → modela-se a sequência de chamadas entre os objetos envolvidos (ex.: interface, conta, banco de dados).

---

## 6. Diagrama de Atividades

Diagrama **dinâmico/comportamental**, usado para modelar em **alto nível um processo ou fluxo de negócio** (não chamadas entre objetos, como no diagrama de sequência).

**Analogia usada em aula:** existe uma **ficha (token)** imaginária que "caminha" pelos nós do diagrama.

| Elemento | Símbolo | Comportamento |
|---|---|---|
| **Nó inicial** | círculo preenchido | Cria a ficha e a envia ao único fluxo de saída. Não tem fluxo de entrada. |
| **Ação** | retângulo de cantos arredondados | Um fluxo de entrada, um de saída. Executa e repassa a ficha adiante. |
| **Decisão** | losango | Um fluxo de entrada, dois ou mais de saída, cada um com uma condição (guarda). Envia a ficha apenas pelo fluxo cuja condição é verdadeira. |
| **Merge** | losango | Vários fluxos de entrada, um de saída. Repassa a ficha assim que ela chega em qualquer entrada. Usado para "fechar" decisões. |
| **Fork** | barra sólida | Um fluxo de entrada, vários de saída. Multiplica a ficha — cria execução paralela. |
| **Join** | barra sólida | Vários fluxos de entrada, um de saída. Espera todas as fichas chegarem antes de repassar (sincronização). |
| **Nó final** | círculo com borda (alvo) | Um ou mais fluxos de entrada, nenhum de saída. Encerra a execução ao receber qualquer ficha. |

**Cuidado comum (erro clássico):** confundir **merge** (não sincroniza, apenas une fluxos alternativos de uma decisão) com **join** (sincroniza fluxos paralelos criados por um fork). Um join usado erroneamente em um lugar de merge (ou vice-versa) trava ou distorce o fluxo lógico do processo.

### Alternativas a diagramas de atividades

- **Fluxogramas**: mais antigos, mas não suportam concorrência (sem fork/join).
- **Redes de Petri** (Carl Adam Petri, 1962): notação mais formal para sistemas concorrentes, também baseada em fichas (tokens).
- **BPMN** (*Business Process Model and Notation*): notação mais amigável para processos de negócio, voltada a analistas de negócio.

---

## 7. Resumo geral: quando usar cada diagrama

| Diagrama | Tipo | O que modela |
|---|---|---|
| Classes | Estático | Estrutura: classes, atributos, métodos, relacionamentos |
| Pacotes | Estático | Organização em alto nível: grupos de classes e dependências |
| Sequência | Dinâmico | Ordem temporal de chamadas de método entre objetos |
| Atividades | Dinâmico | Fluxo/processo de negócio, incluindo decisões e paralelismo |

**Ferramenta usada em aula:** LucidChart (https://www.lucidchart.com/pages/pt) — para exercícios práticos (ex.: sistema de zoológico, carrinho de compras online).

---

## 8. Exercícios

### Bloco A — Conceituais

1. Explique as três formas de uso da UML segundo Fowler (blueprint, sketch e linguagem de programação) e diga em qual contexto (ágil ou tradicional) cada uma faz mais sentido.
2. Diferencie Engenharia Avante e Engenharia Reversa, dando um exemplo de uso de UML em cada uma.
3. Explique a diferença entre diagramas estáticos e diagramas dinâmicos da UML, citando dois exemplos de cada grupo.
4. Em um diagrama de atividades, explique a diferença entre um nó de **merge** e um nó de **join**.
5. Por que o livro-texto recomenda cautela ao usar os conceitos de composição e agregação em diagramas de classes?

### Bloco B — Diagrama de Classes (prática)

6. Modele em um Diagrama de Classes UML os seguintes cenários:
   a. `ContaBancaria` possui exatamente um `Cliente`. Um `Cliente` pode ter várias `ContaBancaria`. Existe navegabilidade em ambos os sentidos.
   b. `ContaPoupanca` e `ContaSalario` são subclasses de `ContaBancaria`.
   c. No código de `ContaBancaria`, declara-se uma variável local do tipo `BancoDados`.
   d. Um `ItemPedido` se refere a um único `Produto` (sem navegabilidade). Um `Produto` pode ter vários `ItemPedido` (com navegabilidade).
   e. A classe `Aluno` possui atributos `nome`, `matricula`, `curso` (todos privados) e métodos públicos `getCurso()` e `cancelaMatricula()`.

7. **(ENADE 2014, adaptado)** Construa um diagrama de classes para:
   - Uma `RevistaCientifica` possui título, ISSN e periodicidade.
   - Essa revista publica diversas `Edicao`, cada uma com número, volume e data. Cada edição pertence a exatamente uma revista, e não pode se relacionar com outra.
   - Um `Artigo` possui título e nome do autor, e é conteúdo exclusivo de uma edição. Uma edição deve ter entre 10 e 15 artigos.

8. Crie diagramas de classes para os seguintes trechos de código Java:

   ```java
   // (a)
   public class HelloWorldSwing {
      public static void main(String[] args) {
         JFrame frame = new JFrame("Hello world!");
         frame.setVisible(true);
      }
   }
   ```

   ```java
   // (b)
   class HelloWorldSwing extends JFrame {
      public HelloWorldSwing() {
         super("Hello world!");
      }
      public static void main(String[] args) {
         HelloWorldSwing frame = new HelloWorldSwing();
         frame.setVisible(true);
      }
   }
   ```

### Bloco C — Diagrama de Sequência (prática)

9. Desenhe o diagrama de sequência referente ao código abaixo, começando pela chamada `a.m5()`:

   ```java
   A a = new A();
   B b = new B();
   C c = new C();

   class C {
      void m1() { ... }
   }
   class B {
      void m2() { ... c.m1(); ... this.m3(); ... }
      void m3() { ... c.m1(); ... }
      void m4() { ... }
   }
   class A {
      void m5() { ... b.m2(); ... b.m3(); ... b.m4(); ... }
   }
   ```

### Bloco D — Diagrama de Atividades (prática)

10. Um diagrama de atividades foi desenhado incorretamente, usando um nó de *join* onde deveria haver um *merge* (ou vice-versa), causando um comportamento indesejado no fluxo. Descreva que tipo de erro de lógica isso causaria e como corrigi-lo.
11. Modele, usando um Diagrama de Atividades, o processo de finalização de uma compra em uma loja virtual: verificação de estoque, cálculo do frete, escolha da forma de pagamento (decisão: cartão ou boleto) e confirmação do pedido.

### Bloco E — Diagrama de Pacotes (prática)

12. Um sistema possui os pacotes `UI`, `BusinessLayer` e `Persistence`. `UI` depende de `BusinessLayer` para acionar regras de negócio, e `BusinessLayer` notifica `UI` sobre eventos (ex.: erro de validação). Apenas `BusinessLayer` acessa `Persistence`. Desenhe o diagrama de pacotes correspondente, indicando corretamente a direção das dependências.

### Bloco F — Estudo dirigido / discussão

13. Segundo a pesquisa de Baltes & Diehl (2013) citada no livro-texto, apenas 9% dos esboços de projeto eram integralmente baseados em UML, mas 48% continham *algum* elemento da notação. Na sua opinião, isso enfraquece ou reforça a importância de se ensinar UML formalmente? Justifique.
14. Cite as vantagens dos diagramas de atividades da UML em relação a fluxogramas tradicionais.

---

## Referências

- VALENTE, Marco Tulio. **Engenharia de Software Moderna** — Capítulo 4: Modelos. Disponível em: https://engsoftmoderna.info/cap4.html
- FOWLER, Martin. *UML Distilled: A Brief Guide to the Standard Object Modeling Language*, 3ª ed. Addison-Wesley, 2003.
- BOOCH, Grady; RUMBAUGH, James; JACOBSON, Ivar. *The Unified Modeling Language User Guide*. Addison-Wesley, 2005.
- LARMAN, Craig. *Applying UML and Patterns: An Introduction to Object-Oriented Analysis and Design and Iterative Development*. Prentice-Hall, 2004.
- Slides de aula: Aula 3.2 (UML — Parte I) e Aula 3.3 (UML — Parte II), Profs. Marco Tulio Valente e Mehran Misaghi.

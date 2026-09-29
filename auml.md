# Trabalho de Diagramas UML — 01/10 (Nova data)

**Disciplina:** Engenharia de Software II

**Professor:** Mehran Misaghi

**Base:** slides 74, 75 e 76 da apresentação *ESWII — UML*

---

## Sumário

1. [Objetivo do trabalho](#1-objetivo-do-trabalho)
2. [O mapa dos diagramas UML (slide 74)](#2-o-mapa-dos-diagramas-uml-slide-74)
3. [Formação de grupos e temas (slide 75)](#3-formação-de-grupos-e-temas-slide-75)
4. [Descrição do trabalho e cronograma (slide 76)](#4-descrição-do-trabalho-e-cronograma-slide-76)
5. [Como estruturar a apresentação](#6-como-estruturar-a-apresentação)
6. [Como encontrar exemplos em artigos](#7-como-encontrar-exemplos-em-artigos)
7. [Checklist antes de apresentar](#8-checklist-antes-de-apresentar)
8. [Pontos-chave para revisão](#9-pontos-chave-para-revisão)
9. [Material para estudar](#10-material-para-estudar)

---

## 1. Objetivo do trabalho

Nas aulas anteriores estudamos os diagramas UML mais usados no dia a dia (classes, pacotes, sequência, atividades, casos de uso). A UML 2.x, porém, define **14 tipos de diagramas**, e vários deles são pouco conhecidos, embora sejam muito úteis em contextos específicos — sistemas distribuídos, sistemas embarcados e de tempo real, arquitetura de componentes, entre outros.

O objetivo deste trabalho é que cada grupo **estude a fundo um desses diagramas menos explorados** e o **ensine à turma**, apresentando:

- os **aspectos teóricos** do diagrama (para que serve, quais são seus elementos e sua notação);
- um **cenário concreto** com um **diagrama de exemplo** construído ou analisado pelo grupo.

Assim, ao final das apresentações, a turma terá uma visão completa da família de diagramas da UML.

---

## 2. O mapa dos diagramas UML (slide 74)

Os diagramas da UML dividem-se em dois grandes grupos:

- **Diagramas estruturais** — descrevem a parte **estática** do sistema: quais elementos existem e como se relacionam.
- **Diagramas comportamentais** — descrevem a parte **dinâmica**: o que acontece ao longo do tempo, como os elementos interagem e mudam de estado. Dentro deles há um subgrupo, os **diagramas de interação**.

A árvore abaixo reproduz a hierarquia do slide 74. Os números em **vermelho** no slide (aqui entre colchetes) indicam os **sete temas sorteáveis** do trabalho:

```
Diagramas da UML
├── Diagramas Estruturais
│   ├── Diagrama de Objetos
│   ├── Diagrama de Classes
│   ├── Diagrama de Pacotes
│   ├── Diagrama de Estrutura Composta  [6]   (introduzido pela UML 2.0)
│   └── Diagramas de Implementação
│       ├── Diagrama de Componentes      [7]
│       └── Diagrama de Implantação      [1]
└── Diagramas Comportamentais
    ├── Diagrama de Atividades
    ├── Diagrama de Casos de Uso
    ├── Diagrama de Transições de Estados [5]
    └── Diagramas de Interação
        ├── Diagrama de Sequência
        ├── Diagrama de Visão Geral da Interação [2]  (introduzido pela UML 2.0)
        ├── Diagrama de Temporização     [3]  (introduzido pela UML 2.0)
        └── Diagrama de Colaboração      [4]
```

| Nº | Diagrama | Categoria | Novo na UML 2.0? |
|---|---|---|---|
| 1 | Implantação | Estrutural (implementação) | Não |
| 2 | Visão Geral da Interação | Comportamental (interação) | **Sim** |
| 3 | Temporização | Comportamental (interação) | **Sim** |
| 4 | Colaboração | Comportamental (interação) | Não (renomeado) |
| 5 | Transições de Estados | Comportamental | Não |
| 6 | Estrutura Composta | Estrutural | **Sim** |
| 7 | Componentes | Estrutural (implementação) | Não |

> **Nota de nomenclatura.** Alguns nomes do slide vêm da UML 1.x e aparecem com outro nome na especificação atual (UML 2.5):
> - *Diagrama de Colaboração* → **Diagrama de Comunicação**;
> - *Diagrama de Transições de Estados* → **Diagrama de Máquina de Estados**.
>
> Ao pesquisar, procurem pelos dois nomes — a literatura usa ambos.

---

## 3. Formação de grupos e temas (slide 75)

**Regras:**

1. Grupos de **até 4 pessoas**.
2. O número do tema foi **sorteado** em <https://sorteador.com.br/>.

**Grupos e temas definidos:**

| Grupo | Integrantes | Tema | Nº no mapa |
|---|---|---|---|
| a | Hugo, Vitor | Diagrama de Componentes | 7 |
| b | Guilherme, Maurício e Kelvin | Diagrama de Colaboração (Comunicação) | 4 |
| c | Heloísa e Mirella | Diagrama de Implantação | 1 |
| d | Henrique, Paulo e Tomas | Diagrama de Temporização | 3 |
| e | Luís, José e Leonardo | Diagrama de Transição de Estados (Máquina de Estados) | 5 |
| f | Arthur e Brunno | Diagrama de Interação — Visão Geral da Interação | 2 |
| g | Thiago, Felipe e Carlos | Diagrama de Estrutura Composta | 6 |

Os sete temas numerados no mapa foram todos distribuídos — cada grupo é "dono" de um diagrama diferente.

---

## 4. Descrição do trabalho e cronograma (slide 76)

### 4.1 O que cada grupo deve fazer

1. **Apresentar os aspectos teóricos** do diagrama sorteado.
2. **Preparar um cenário** e apresentar um **diagrama exemplo** do tipo sorteado. Podem ser usados casos e exemplos prontos, baseados em **artigos** (Google Acadêmico e/ou outras bases).
3. A apresentação pode ser em **slides** (Google Slides ou Canva) ou por **outros meios** (por exemplo, no quadro).
4. **Enviar o link** da apresentação dentro do prazo.
5. **Registrar no grupo da turma** a preferência de ordem de apresentação.

### 4.2 Cronograma

| Data | Atividade |
|---|---|
| **24/09** | Aula reservada para o **desenvolvimento do trabalho** |
| **28/09** | Prazo final para **enviar o link** da apresentação |
| **29/09** | **Correção e término das Apresentações** dos grupos |
| **01/10** | **Apresentações** |



---

## 5. Como estruturar a apresentação

Um roteiro sugerido:

1. **Abertura** — nome do diagrama, categoria (estrutural/comportamental) e posição no mapa do slide 74.
2. **Para que serve** — qual problema o diagrama resolve; em que tipo de sistema ele aparece.
3. **Notação** — cada elemento com seu símbolo, explicado **um a um**.
4. **Cenário** — descrever o sistema/problema em linguagem natural **antes** de mostrar o diagrama.
5. **Diagrama exemplo** — apresentar e "ler" o diagrama junto com a turma.
6. **Relação com outros diagramas** — com quais diagramas ele se complementa ou se confunde.
7. **Vantagens e limitações** — quando **não** vale a pena usá-lo.
8. **Referências** — livros, artigos e ferramentas utilizadas.

**Ferramentas para desenhar o diagrama:** draw.io (diagrams.net), PlantUML, Astah, StarUML, Lucidchart ou até o quadro.

---

## 6. Como encontrar exemplos em artigos

O item 2 do slide 76 permite usar exemplos prontos de artigos. Para buscar no **Google Acadêmico** (<https://scholar.google.com>):

- Combine o nome do diagrama com um domínio de aplicação, em português e em inglês:
  - `"diagrama de implantação" UML estudo de caso`
  - `"UML timing diagram" embedded system`
  - `"interaction overview diagram" case study`
  - `"UML state machine" modeling`
  - `"composite structure diagram" UML`
- Lembre dos **nomes alternativos** (Colaboração/Comunicação, Transição de Estados/Máquina de Estados).
- Ao usar um diagrama de artigo, **cite a fonte** no slide e explique o contexto do sistema modelado.
- Outras bases úteis: IEEE Xplore, ACM Digital Library, SBC OpenLib (SOL) e Portal de Periódicos CAPES.

---

## 7. Checklist antes de apresentar

- [ ] A teoria cobre **propósito, elementos e notação** do diagrama?
- [ ] Existe um **cenário** descrito com clareza?
- [ ] O **diagrama exemplo** usa a notação correta da UML 2.x?
- [ ] O grupo sabe relacionar o diagrama com os demais (mapa do slide 74)?
- [ ] As **fontes** (livros/artigos) estão citadas?
- [ ] O **link** foi enviado até **28/09**?
- [ ] A **preferência de ordem** foi registrada no grupo?
- [ ] Todos os integrantes sabem explicar qualquer parte da apresentação?
- [ ] **Tempo de apresentação ficou em 10 minutos**?

---

## 8. Pontos-chave para revisão

- A UML divide seus diagramas em **estruturais** (estáticos) e **comportamentais** (dinâmicos); os **diagramas de interação** são um subgrupo dos comportamentais.
- **Estrutura Composta**, **Visão Geral da Interação** e **Temporização** foram **introduzidos na UML 2.0**.
- **Componentes** e **Implantação** formam os **diagramas de implementação**: lógica × física.
- O **Diagrama de Colaboração** chama-se hoje **Diagrama de Comunicação** e mostra as mesmas mensagens de um diagrama de sequência, organizadas pelos vínculos entre objetos.
- O **Diagrama de Transições de Estados** chama-se hoje **Diagrama de Máquina de Estados**.
- Entregas: **link até 28/09**, **apresentações em 29/09**.

---

## 9. Material para estudar

- VALENTE, Marco Tulio. **Engenharia de Software Moderna**. Capítulo 4 — Modelos (UML). Disponível em: <https://engsoftmoderna.info>.
- FOWLER, Martin. **UML Essencial: um breve guia para a linguagem-padrão de modelagem de objetos**. 3. ed. Porto Alegre: Bookman, 2005.
- BOOCH, Grady; RUMBAUGH, James; JACOBSON, Ivar. **UML: guia do usuário**. 2. ed. Rio de Janeiro: Elsevier/Campus, 2006.
- OMG — Object Management Group. **Unified Modeling Language (UML) Specification, version 2.5.1**. Disponível em: <https://www.omg.org/spec/UML/>.

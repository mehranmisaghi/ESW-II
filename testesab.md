---
title: 'Testes A/B'
description: 'Testes A/B'
permalink: testesab.md

---

## Sumário

1. [O que é um teste A/B](#1-o-que-é-um-teste-ab)
2. [Quando usar testes A/B](#2-quando-usar-testes-ab)
3. [Como funciona: grupo de controle e grupo de tratamento](#3-como-funciona-grupo-de-controle-e-grupo-de-tratamento)
4. [Dimensionando a amostra](#4-dimensionando-a-amostra)
5. [Fundamento estatístico](#5-fundamento-estatístico)
6. [Variações: A/B/n e testes A/A](#6-variações-abn-e-testes-aa)
7. [Exemplos reais de empresas](#7-exemplos-reais-de-empresas)
8. [Erros comuns e boas práticas](#8-erros-comuns-e-boas-práticas)
9. [Pontos-chave para revisão](#9-pontos-chave-para-revisão)
10. [Para pensar (exercícios)](#10-para-pensar-exercícios)
11. [Material para estudar](#11-material-para-estudar)

---
> Material preparado com auxílio de IA, revisado por Mehran Misaghi
## 1. O que é um teste A/B

Um **teste A/B** (também chamado de *split test*) é uma técnica para decidir, **com dados reais de uso**, qual de duas versões de um sistema é melhor. As duas versões são idênticas em tudo, exceto por **um único requisito** que muda entre elas — uma implementa o requisito **A**, a outra o requisito **B** — e A e B são mutuamente exclusivos.

Diferente de abordagens tradicionais de engenharia de requisitos (entrevistas, casos de uso, histórias de usuário), o teste A/B **não pergunta ao usuário o que ele prefere** — ele **observa o comportamento real** de usuários reais, divididos em dois grupos, e deixa os dados decidirem.

> A origem do nome e da metodologia vem dos **experimentos randomizados controlados** (*randomized controlled trials*) usados há décadas na medicina e na indústria farmacêutica para testar se um novo tratamento é realmente mais eficaz que o atual.

**Ideia central:** ao invés de decidir por opinião ou intuição qual versão é melhor, mede-se o efeito de cada versão em usuários reais e mantém-se a versão vencedora, descartando a perdedora.

---

## 2. Quando usar testes A/B

Testes A/B fazem sentido sempre que existe uma **dúvida real** sobre qual entre duas alternativas gera mais valor. Os contextos mais comuns são:

- **Validação de MVP:** comparar um MVP inicial (conjunto de requisitos A) com uma versão melhorada (requisitos B) — ver [notas de aula sobre MVP](mvp_notas_de_aula.md);
- **Componentes de interface:** leiaute de uma página, cor e posição de um botão, texto de uma mensagem, ordem de apresentação de itens;
- **Algoritmos:** por exemplo, comparar dois algoritmos de recomendação para ver qual gera mais engajamento.

Assim como o MVP, o teste A/B é mais útil justamente quando **ainda não se sabe** a resposta — se já houver certeza de qual alternativa é melhor, testar não agrega valor.

---

## 3. Como funciona: grupo de controle e grupo de tratamento

Um teste A/B precisa de três elementos:

| Elemento | Descrição |
|---|---|
| **Versão de controle** | O sistema como ele já é hoje (requisitos A) |
| **Versão de tratamento** | O sistema com o novo requisito sendo testado (requisitos B) |
| **Taxa de conversão** | Métrica que mede o "sucesso" em cada grupo (ex.: % de cliques, % de compras, tempo de uso) |

O tráfego de usuários reais é **dividido aleatoriamente** entre os dois grupos — normalmente 50%/50%, embora outras proporções sejam possíveis — e a taxa de conversão de cada grupo é comparada ao final do experimento.

![Estrutura de um teste A/B: usuários divididos aleatoriamente entre grupo de controle e grupo de tratamento, com a taxa de conversão medida em cada grupo](images/img_estrutura_teste_ab.png)

### 3.1 Exemplo de código: divisão aleatória

A divisão dos usuários entre os grupos é normalmente feita em código, de forma simples. Um exemplo didático (pseudocódigo, adaptado do material de referência):

```javascript
// Decide, para cada usuário, qual versão do sistema ele vai ver
function escolherVersao() {
  const sorteio = Math.random(); // número aleatório entre 0 e 1

  if (sorteio < 0.5) {
    return "controle";   // grupo A — versão atual
  } else {
    return "tratamento"; // grupo B — versão nova
  }
}
```

Na prática, ferramentas de experimentação (como Optimizely, Google Optimize — descontinuado —, ou soluções internas de grandes empresas) cuidam dessa divisão, garantem que o **mesmo usuário sempre veja a mesma versão** durante o experimento (para não distorcer os dados) e coletam as métricas automaticamente.

### 3.2 Exemplo prático simples

Imagine uma loja virtual testando dois botões de "Finalizar compra":

- **Grupo A (controle):** botão cinza, texto "Finalizar compra";
- **Grupo B (tratamento):** botão verde, texto "Comprar agora".

Depois de rodar o teste com usuários reais durante um período, mede-se a taxa de conversão (usuários que finalizaram a compra) em cada grupo. Se o Grupo B converter significativamente mais, o botão verde com o novo texto é adotado para todos os usuários.

---

## 4. Dimensionando a amostra

Uma das partes **mais difíceis e mais mal compreendidas** de um teste A/B é decidir **quantos usuários** cada grupo precisa ter antes que o resultado seja confiável. O tamanho da amostra depende, entre outros fatores, da taxa de conversão atual e do menor ganho que se deseja detectar. Dois exemplos ilustram como esse número pode variar bastante:

| Cenário | Taxa de conversão atual | Ganho mínimo a detectar | Amostra necessária (por grupo) |
|---|---|---|---|
| 1 | 1% | 10% | ≈ 200.000 usuários |
| 2 | 10% | 25% | ≈ 1.800 usuários |

Quanto **menor** a taxa de conversão atual e **menor** o ganho que se quer detectar, **maior** precisa ser a amostra. Calcular esse número manualmente é complexo — por isso, na prática, usa-se uma **calculadora de tamanho de amostra**, como a [calculadora da Optimizely](https://www.optimizely.com/sample-size-calculator/), que a partir da taxa de conversão atual, do ganho mínimo esperado e do nível de confiança desejado, informa quantos usuários por grupo são necessários.

**Regra importante:** definido o tamanho da amostra, o experimento deve rodar até atingi-lo — **não se deve interromper um teste A/B antes do tempo**, mesmo que os resultados pareçam favoráveis logo no início. Resultados parciais podem inverter completamente ao longo do experimento, e parar cedo é uma das causas mais comuns de conclusões erradas (ver Seção 8).

---

## 5. Fundamento estatístico

Um teste A/B é, formalmente, um **teste de hipóteses**:

- **Hipótese nula (H0):** a versão B **não é** melhor que a versão A (a diferença observada é só ruído/acaso);
- **Hipótese alternativa (H1):** a versão B **é** melhor que a versão A.

Dois conceitos-chave guiam a decisão:

- **Nível de significância (α):** a probabilidade que estamos dispostos a aceitar de errar dizendo "B é melhor" quando na verdade não é (esse erro é chamado de **Erro Tipo I**, ou falso positivo). O valor mais usado na prática é **α = 5%**;
- **Nível de confiança:** o complemento do α — geralmente **95%** — é o parâmetro que aparece nas calculadoras de teste A/B como "confidence level".

Na prática (sem entrar no cálculo estatístico formal), o resultado costuma ser visualizado com **intervalos de confiança**: cada grupo tem uma taxa de conversão média, com uma margem de erro para cima e para baixo. Quando os intervalos dos dois grupos **se sobrepõem**, o resultado é inconclusivo; quando **não se sobrepõem**, há evidência estatística de que um grupo é realmente melhor que o outro.

![Dois gráficos comparando taxa de conversão do grupo A e do grupo B: no primeiro os intervalos de confiança se sobrepõem (resultado inconclusivo); no segundo não se sobrepõem (resultado estatisticamente significativo)](images/img_significancia_estatistica.png)

---

## 6. Variações: A/B/n e testes A/A

- **Teste A/B/n:** em vez de testar apenas duas versões, testam-se **três ou mais variações simultaneamente** (A, B, C, ... n). A lógica é a mesma, só que o tráfego é dividido entre mais grupos — o que exige amostras ainda maiores por grupo.
- **Teste A/A:** os **dois grupos recebem exatamente a mesma versão** do sistema (não há diferença real entre eles). Isso serve para **validar o próprio procedimento do experimento** (a ferramenta de divisão de tráfego, a coleta de métricas etc.) — como não há diferença real, o teste **deveria, quase sempre, dar "empate"** (não detectar diferença significativa). Se um teste A/A indicar diferença significativa com frequência, é sinal de que há um problema na metodologia ou na infraestrutura de experimentação.

---

## 7. Exemplos reais de empresas

Testes A/B são amplamente usados por empresas de tecnologia para validar mudanças antes de liberá-las para todos os usuários:

- **Facebook:** novas funcionalidades são liberadas para uso real e comparadas com a versão anterior ("caso base"). Isso evita a necessidade de elicitar todos os requisitos antecipadamente e ajuda a detectar usos inesperados de uma funcionalidade.
- **Netflix:** cada funcionalidade nova é tratada como um experimento — inclusive pode ser removida ("morrer") após o lançamento, se os dados mostrarem baixo uso. A empresa também testa sistematicamente variações de **miniaturas (thumbnails)** de séries e filmes para ver quais geram mais cliques.
- **Microsoft Bing:** já chegou a rodar, em 2013, **mais de 200 experimentos A/B simultâneos por dia** — um sistema de experimentação que a empresa credita por acelerar a inovação e aumentar a receita em milhões de dólares.
- **Google — "41 tons de azul":** um dos exemplos mais citados no mercado. Em 2009, a equipe de Marissa Mayer testou **41 variações da cor azul** usada nos links dos resultados de busca, para descobrir qual tonalidade gerava mais cliques — um teste que, segundo relatos da época, teria gerado um ganho estimado em **centenas de milhões de dólares** em receita de publicidade.
- **YouTube:** disponibiliza para os criadores de conteúdo uma ferramenta nativa de teste A/B para comparar **títulos e miniaturas** de vídeos, mostrando cada variação para uma fração dos espectadores antes de escolher a vencedora.

---

## 8. Erros comuns e boas práticas

Com base na literatura sobre experimentação controlada (ver Seção 11), alguns cuidados essenciais:

1. **Não interrompa o teste antes do tamanho de amostra planejado.** Olhar o resultado parcial repetidamente e parar assim que ele "parecer bom" (conhecido como *peeking*) infla a taxa de falsos positivos.
2. **Garanta aleatoriedade de verdade** na divisão dos grupos, e mantenha o mesmo usuário sempre no mesmo grupo durante todo o experimento.
3. **Rode testes A/A periodicamente** para validar se a própria infraestrutura de experimentação está funcionando corretamente.
4. **Um resultado "sem significância" não é o mesmo que "não faz diferença"** — pode simplesmente significar que a amostra foi pequena demais para detectar o efeito.
5. **Significância estatística não é o mesmo que relevância prática.** Um ganho de 0,01% pode ser estatisticamente significativo em amostras enormes, mas não justificar o custo de implementar a mudança.
6. **Cuidado com métricas de vaidade.** A métrica de conversão escolhida deve refletir valor real para o negócio/usuário, não apenas um número fácil de mover.

---

## 9. Pontos-chave para revisão

- Teste A/B compara duas versões de um sistema, diferindo em **um único requisito**, dividindo usuários reais aleatoriamente entre **grupo de controle (A)** e **grupo de tratamento (B)**.
- A origem do método está nos **experimentos randomizados controlados** da medicina.
- A decisão é baseada na **taxa de conversão** de cada grupo, comparada estatisticamente.
- O **tamanho da amostra** deve ser calculado antes do teste (ex.: calculadora da Optimizely) e o experimento **não deve ser interrompido antes desse tamanho ser atingido**.
- É um **teste de hipóteses**: H0 (B não é melhor) vs. H1 (B é melhor), com nível de significância tipicamente de **5%** (confiança de 95%).
- **Teste A/B/n** compara mais de duas variações; **teste A/A** compara duas versões idênticas, servindo para validar a metodologia do experimento.
- Empresas como Facebook, Netflix, Microsoft (Bing), Google e YouTube usam testes A/B em larga escala no dia a dia.
- Erros comuns: parar o teste cedo demais, amostra insuficiente, confundir significância estatística com relevância prática.

---

## 10. Para pensar (exercícios)

1. Qual a principal diferença entre um teste A/B e simplesmente perguntar aos usuários, por meio de uma pesquisa de satisfação, qual versão eles preferem?
2. Uma equipe roda um teste A/B por dois dias, vê que o grupo B está convertendo mais, e decide encerrar o teste antecipadamente e adotar a versão B para todos. Que problema(s) essa decisão pode causar? Relacione com o conteúdo da Seção 4 e da Seção 8.
3. Explique, com suas palavras, para que serve um **teste A/A** e por que ele normalmente deveria "não encontrar diferença" entre os grupos.
4. Um e-commerce tem hoje uma taxa de conversão de 1% e quer detectar um ganho mínimo de 10% com um novo layout de página. Sem fazer o cálculo estatístico exato, seria razoável esperar que esse teste precise de uma amostra pequena (algumas centenas de usuários) ou muito grande? Justifique com base na Seção 4.
5. Dê um exemplo (real ou hipotético, diferente dos citados na Seção 7) de uma situação em um sistema de software em que um teste A/B faria mais sentido do que simplesmente perguntar a opinião dos usuários.
6. Um teste A/B mostra que o Grupo B teve uma taxa de conversão de 5,4% contra 5,1% do Grupo A, mas os intervalos de confiança dos dois grupos se sobrepõem bastante. O que se pode concluir sobre esse resultado? A equipe deveria adotar a versão B?
7. Um teste A/B/n testa 4 variações de uma página ao mesmo tempo, dividindo os usuários igualmente entre elas. Como isso afeta o tamanho de amostra necessário por grupo, comparado a um teste A/B tradicional com apenas 2 grupos?

---

## 11. Material para estudar 

-  ### [Slides da aula](https://canva.link/dixah35o9t01lwk)
- **Capítulo-base:** Valente, Marco Tulio. *Engenharia de Software Moderna: Princípios e Práticas para Desenvolvimento de Software com Produtividade* — Capítulo 3, seção sobre Testes A/B: [engsoftmoderna.info/cap3.html](https://engsoftmoderna.info/cap3.html)
- **Calculadora de tamanho de amostra:** [Sample Size Calculator — Optimizely](https://www.optimizely.com/sample-size-calculator/)
- **Artigo:** Kohavi, R., Deng, A., Frasca, B., Walker, T., Xu, Y., Pohlmann, N. (2013). *Online Controlled Experiments at Large Scale.* KDD 2013. DOI: [10.1145/2487575.2488217](https://doi.org/10.1145/2487575.2488217)
- **Artigo:** Kohavi, R., Deng, A. (2014). *Seven Rules of Thumb for Web Site Experimenters.* KDD 2014. DOI: [10.1145/2623330.2623341](https://doi.org/10.1145/2623330.2623341) — resumo acessível em [exp-platform.com/rules-of-thumb](https://exp-platform.com/rules-of-thumb/)
- **Artigo sobre testes A/A:** referenciado no capítulo-base. DOI: [10.1109/ICSE-SEIP.2019.00009](https://doi.org/10.1109/ICSE-SEIP.2019.00009)
- **Livro (leitura complementar):** Kohavi, R., Tang, D., Xu, Y. (2020). *Trustworthy Online Controlled Experiments: A Practical Guide to A/B Testing.* Cambridge University Press.
- **Caso "41 tons de azul" do Google:** ["Google's Marissa Mayer Assaults Designers With Data"](https://www.fastcompany.com/1403230/googles-marissa-mayer-assaults-designers-data) — Fast Company, 2009.
- **Teste A/B de títulos e miniaturas no YouTube:** ["Avaliar títulos e miniaturas com o teste A/B"](https://support.google.com/youtube/answer/16391400?hl=pt-Br) — Central de Ajuda do YouTube.
- **Notas de aula relacionadas:** [MVP — Notas de Aula](mvp_notas_de_aula.md), no mesmo repositório.

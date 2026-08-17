# Exercícios de Casos de Uso


> Estes exercícios complementam o conteúdo aprendido de [Casos de Uso](./casos-de-uso.md). 

---

## Como deve resolver cada exercício?

Para cada caso de uso solicitado, entregue:

1. **Nome** — no formato `UC<NNN> - <descrição>` (verbo no infinitivo)
2. **Ator(es)** envolvido(s)
3. **Objetivo** (1-2 frases)
4. **Pré-condições**
5. **Fluxo Normal** (passos numerados, voz ativa, sem detalhes de interface)
6. **Fluxos Alternativos/Exceção** (pelo menos 2, indicando em qual passo se ramificam)
7. **Pós-condições** (para o fluxo normal e para cada exceção relevante)

> 💡 Dica: revise a seção [Pré-Condições](./casos-de-uso.md#pré-condições) antes de começar — pré-condições **não** podem depender de cliques em botões ou seleções de menu.
---

## Bloco 1 — Exercícios com dicas (em trio)

### Exercício 1.1 — Cadastrar Produto (E-commerce)

Um sistema de e-commerce permite que o **Vendedor** cadastre produtos para venda. Ao cadastrar, ele informa nome, descrição, preço, categoria e quantidade em estoque. O sistema valida se o preço é maior que zero e se a categoria existe. Se tudo estiver correto, o produto é publicado na loja.

**Elabore o caso de uso completo**, incluindo:
- O que acontece se o preço informado for inválido (≤ 0)?
- O que acontece se a categoria informada não existir?

<details>
<summary>💡 Dica (clique para expandir)</summary>

- Pense se "categoria não existe" deveria oferecer a opção de criar uma nova categoria.
- A pré-condição pode envolver o vendedor estar autenticado e com uma loja ativa no sistema.
</details>

---

### Exercício 1.2 — Avaliar Produto (E-commerce)

Após receber um produto, o **Cliente** pode avaliá-lo, atribuindo uma nota de 1 a 5 estrelas e, opcionalmente, um comentário. O sistema só permite avaliação de produtos que o cliente efetivamente comprou.

**Elabore o caso de uso completo**, incluindo:
- O que ocorre se o cliente tentar avaliar um produto que não comprou?
- O que ocorre se o cliente tentar avaliar o mesmo produto duas vezes?

<details>
<summary>💡 Dica (clique para expandir)</summary>

- A pré-condição "produto foi comprado pelo cliente" é uma pré-condição legítima (não depende de clique de botão).
- Considere se o sistema permite **editar** uma avaliação já feita, ao invés de duplicá-la.
</details>

---

## Bloco 2 — Escolhe um dos casos para fazer em trio

Escolha (ou seu professor irá atribuir) **um sistema** por vez. Para cada caso de uso listado, elabore a documentação completa.

### 2.1 — Sistema de Biblioteca

**Atores sugeridos:** Bibliotecário, Usuário (leitor), Sistema de Cobrança

Casos de uso a elaborar:

1. **Emprestar Livro**
   - Considere: livro disponível vs. indisponível; usuário com pendências (multas) vs. sem pendências.
2. **Devolver Livro**
   - Considere: devolução dentro do prazo vs. devolução com atraso (gera multa).
3. **Reservar Livro**
   - Considere: todos os exemplares emprestados; notificação quando o livro for devolvido.

---

### 2.2 — Sistema de Restaurante (Delivery)

**Atores sugeridos:** Cliente, Restaurante, Entregador, Sistema de Pagamento

Casos de uso a elaborar:

1. **Realizar Pedido**
   - Considere: itens fora do cardápio do dia; restaurante fechado no momento do pedido.
2. **Acompanhar Entrega**
   - Considere: atraso na entrega; entregador não localiza o endereço.
3. **Cancelar Pedido**
   - Considere: cancelamento antes vs. depois do preparo iniciado (pode haver taxa).

---

### 2.3 — Sistema de Academia

**Atores sugeridos:** Aluno, Instrutor, Recepcionista, Sistema de Cobrança

Casos de uso a elaborar:

1. **Matricular Aluno em Plano**
   - Considere: aluno menor de idade (necessita responsável); plano com vagas esgotadas.
2. **Agendar Aula com Personal**
   - Considere: conflito de horário do instrutor; cancelamento com menos de 2h de antecedência.
3. **Registrar Frequência (Check-in)**
   - Considere: aluno com mensalidade em atraso; tentativa de check-in fora do horário de funcionamento.

---

### 2.4 — Sistema de Estacionamento

**Atores sugeridos:** Motorista, Sistema de Cobrança, Câmera/Sensor (equipamento)

Casos de uso a elaborar:

1. **Registrar Entrada de Veículo**
   - Considere: estacionamento lotado; placa não reconhecida pela câmera.
2. **Registrar Saída e Calcular Cobrança**
   - Considere: ticket perdido; desconto por convênio.
3. **Emitir Mensalidade**
   - Considere: renovação automática; vaga fixa ocupada por terceiro.

---

## Bloco 3 — Exercícios de Identificação (Atores e Casos de Uso) em trio

Para os sistemas abaixo, **antes de escrever os casos de uso**, responda:

- Quem são os atores (humanos, sistemas externos, equipamentos)?
- Quais são os casos de uso de alto nível (liste ao menos 5 por sistema)?

Use como guia as perguntas da seção [Identificando Atores e Casos de Uso](./casos-de-uso.md#identificando-atores-e-casos-de-uso).

### 3.1 — Sistema de Votação Eletrônica (Urna)

Pense em: eleitor, mesário, sistema de apuração, sistema de biometria.

### 3.2 — Sistema de Gestão Hospitalar

Pense em: recepcionista, enfermeiro, médico, paciente, plano de saúde (sistema externo).

### 3.3 — Sistema de Streaming de Vídeo

Pense em: usuário assinante, usuário visitante, produtor de conteúdo, sistema de pagamento, sistema de recomendação.

> Após identificar atores e casos de uso, **escolha 2 casos de uso de cada sistema** e elabore a documentação completa (nome, ator, objetivo, pré-condições, fluxo normal, extensões e pós-condições).

---

## Bloco 4 — Casos de Uso completo  (apresentações)

Escolha **um** dos temas abaixo em trio e elabore um **modelo de casos de uso completo**, contendo:

- Diagrama de casos de uso (pode usar Mermaid, conforme exemplos do material teórico)
- No mínimo **5 casos de uso** distintos
- Para **cada** caso de uso: nome, ator, objetivo, pré-condições, fluxo normal e ao menos 1 fluxo alternativo/exceção, e pós-condições
- Para **2** desses casos de uso, elabore também um **fluxograma Mermaid** representando o fluxo normal e as ramificações

### Temas apresentados no dia 18 de agosto

- 🚌 Aplicativo de consulta e compra de passagens de ônibus - Guilherme, Kelvin e Maurício
- 📦 Sistema de gestão de estoque para uma pequena loja - Hugo, Thiago e Vitor
- 🏠 Aplicativo de aluguel de imóveis por temporada - Henrique, Paulo e Tomas

### Temas apresentados nos dia de agosto

- 🏥 Aplicativo de agendamento de consultas médicas - Arhur, Heloisa e Mirella
- 🎓 Sistema de inscrição e gestão de eventos acadêmicos (congressos, seminários) - Brunno, Carlos e Felipe
- 🐾 Sistema de gestão de uma clínica veterinária - José, Luis e Leonardo

---

## Referências

Consulte o material teórico completo em [`Casos de Uso`](./casos-de-uso.md) para relembrar conceitos, formatos de descrição e exemplos resolvidos antes de iniciar os exercícios.

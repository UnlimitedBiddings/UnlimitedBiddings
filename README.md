# Lucas Candido Silva

**Desenvolvedor júnior em formação · Python, dados públicos e agentes de IA · Guarapari, ES**

Construo ferramentas que leem dados públicos em escala e os transformam em informação que qualquer pessoa entende. Antes de programar, passei três anos dentro de licitações públicas, do lado de quem fornece ao governo. Hoje uno as duas coisas: código em Python, agentes de IA e conhecimento real da Lei 14.133/21.

Estou procurando minha **primeira vaga júnior, de preferência remota**, em Python, dados, automação com IA ou tecnologia para o setor público.

---

## Projetos

### Observatório de Contratações de Guarapari
`Python` · `APIs públicas` · `PDF` · `CSV` · `testes automatizados` · código privado, demonstração sob pedido

Coleta, cruza e explica o dinheiro público de Guarapari a partir de quatro fontes oficiais:

| Fonte | O que o Observatório extrai |
| --- | --- |
| [PNCP](https://pncp.gov.br) | Licitações, contratações diretas, contratos, atas e aditivos de 9 órgãos municipais, desde 2023 |
| [Portal da Transparência de Guarapari](https://transparencia.guarapari.es.gov.br) | Todos os empenhos desde 2010, licitações item por item, contratos com fiscal, convênios, diárias, obras e fornecedores penalizados |
| [Painel de Controle do TCE-ES](https://paineldecontrole.tcees.tc.br) | Alertas da Lei de Responsabilidade Fiscal e comparação com os 78 municípios do estado |
| [Diário Oficial dos Municípios do ES](https://ioes.dio.es.gov.br/dom) | Leis, decretos, extratos de contrato e avisos de licitação, lidos dos PDFs diários |

O que ele faz:

- **Roda sozinho todo dia às 6h**, pelo Agendador de Tarefas do Windows, com log de cada execução e cache que não baixa de novo os anos já encerrados.
- **Calcula o prazo de impugnação** de cada licitação (3 dias úteis antes da abertura, art. 164 da Lei 14.133/21) e marca dispensas e inexigibilidades como "não cabe".
- **Aponta o que merece conferência:** contratação sem licitação, dispensas repetidas com o mesmo fornecedor no ano (possível fracionamento), aditivos acima de 25%, fornecedor com 25% ou mais das compras de um órgão, empenho a fornecedor durante penalidade e contratos que vencem em 90 dias.
- **Confere os próprios números:** os repasses batem ao centavo com a declaração do município ao Tesouro (Siconfi) de 2020 a 2025, e as divergências entre fontes oficiais ficam documentadas.
- **Funciona para outras cidades:** tudo o que muda de um município para outro fica numa ficha JSON. A mesma API atende Vitória, Vila Velha, Serra e Cariacica.
- Gera relatórios em HTML, planilhas CSV e uma base em Markdown que alimenta o Cérebro Virtual.

> Um ponto de atenção indica algo a conferir, não uma irregularidade. Antes de publicar qualquer conclusão, o documento original é aberto e confirmado.

### Placar Guarapari
`Python` · `JavaScript` · `Cloudflare Workers` · `Cloudflare D1` · `SQL` · `node:test`

Site público gerado a partir dos dados do Observatório. Um gerador em Python monta as páginas estáticas, e um Cloudflare Worker serve o site e a página **Participe**, onde moradores registram demandas num banco D1.

- Os dados pessoais dos moradores nunca saem do banco: só contagens são usadas nas análises.
- Testes do Worker com `node --test` e da página Participe com `unittest`, mais um teste de regressão que compara o site gerado antes e depois de cada mudança.

### Cérebro Virtual
`Python` · `SQLite FTS5` · `Ollama` · `RAG` · `C#`

Assistente que responde perguntas sobre o acervo do Observatório **sem mandar nenhum dado para a nuvem**.

- Busca nos documentos com SQLite FTS5 e responde com modelos abertos rodando no próprio PC (Ollama, qwen3.5 de 4B e 35B), escolhidos numa avaliação que comparou citação de fontes e velocidade.
- Toda resposta cita o trecho de onde veio. Se a informação não está no acervo, ele diz que não sabe.
- Conversa por voz, com um atalho de área de trabalho feito em C#.

### Instruir
`TypeScript` · `React` · `Vite` · `shadcn/ui` · `Supabase (PostgreSQL)` · `Stripe` · `MCP` · [repositório](https://github.com/UnlimitedBiddings/Instruir)

Marketplace que conecta alunos a instrutores verificados (direção, idiomas, música) e a autoescolas.

- Mapa com instrutores próximos, agenda de aulas, avaliações e selo de verificação.
- Banco no Supabase com funções em PL/pgSQL.
- Checkout, assinatura e portal do cliente com Stripe.
- Servidor MCP com OAuth e tela de consentimento, para que agentes de IA possam usar a plataforma.
- Prototipado com Lovable e evoluído em mais de 100 commits.

---

## Como eu trabalho com IA

Programo com o **Claude Code** como par de programação, e trato o agente como parte da equipe, com regras escritas:

- **Instruções de projeto** em `CLAUDE.md` e um `ENGENHARIA.md` com os módulos, os donos de cada parte e como validar.
- **Subagentes por módulo:** um engenheiro para o Observatório, outro para o Placar e outro para o Cérebro, além de agentes de QA e de segurança. Cada um tem escopo de arquivos e uma lista do que precisa rodar antes de dizer "pronto".
- **Hooks de segurança:** um hook bloqueia qualquer comando que publique ou escreva fora do PC sem aprovação (deploy, segredos, banco remoto). O hook tem os próprios testes.
- **Skills** para tarefas que se repetem, como diagnóstico de negócios e delegação de leitura em volume para o modelo local.

Regras que sigo em todo projeto:

1. Nada inventado: todo número tem fonte e toda citação tem link.
2. Uma pessoa revisa antes de entregar.
3. Dados pessoais protegidos desde o primeiro dia (LGPD).
4. Testes antes de considerar uma tarefa concluída.

---

## Tecnologias

| Área | Ferramentas |
| --- | --- |
| Linguagens | Python, JavaScript, TypeScript, HTML e CSS, SQL, C#, PowerShell |
| Dados | APIs REST, leitura de PDF, CSV, SQLite (FTS5), PostgreSQL (Supabase), Cloudflare D1 |
| IA | Claude Code, agentes e subagentes, hooks, skills, MCP, RAG, modelos locais com Ollama, engenharia de prompt |
| Web | React, Vite, shadcn/ui, Cloudflare Workers, service workers |
| Ferramentas | Git e GitHub, Linux (Ubuntu, Parrot OS), Agendador de Tarefas do Windows |
| Domínio | Lei 14.133/21, PNCP, portais de transparência, orçamento público (PPA, LDO, LOA, RREO, RGF) |

---

## Experiência

**Consultor e fornecedor em licitações públicas** · negócio próprio · jan. 2023 a set. 2025

- Participei de licitações sob a Lei 14.133/21, da análise do edital à execução do contrato.
- Elaborei pedidos de esclarecimento e impugnações, organizei habilitação e propostas e atuei na fase de lances.
- Assessorei outras empresas fornecedoras, com planos de até 30 licitações por mês.
- Controlei estoque, logística, fluxo de caixa e obrigações fiscais (ICMS e substituição tributária).

É dessa experiência que vêm as regras de negócio do Observatório: sei o que um prazo de impugnação significa na prática e onde um contrato costuma dar problema.

---

## Formação

- **Ciência da Computação, estudo autodidata** · desde 2023
- **Alura** · desde set. 2025: 15 cursos concluídos, entre eles Pensamento Computacional, JavaScript, HTML e CSS, Git e GitHub, Linux e DevOps na linha de comando, Dart, Claude Code, Engenharia de Prompt e Cibersegurança com IA. Em andamento: Python: Inteligência Artificial Aplicada.
- **Escola Nacional de Administração Pública (Enap)** · 2026: 33 cursos, 794 horas, nota média acima de 95, em orçamento público, contratações e obras pela Lei 14.133/21, governança de dados, IA no setor público e liderança.
- **IBM SkillsBuild** · Fundamentos de Segurança Cibernética (2026)
- Ensino médio completo

---

## O que estou estudando agora

- Python aplicado a IA (curso em andamento na Alura)
- C# e SQL, para vagas com sistemas legados
- Testes automatizados e boas práticas de código

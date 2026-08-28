# Dicas e truques para os AI Credits durarem até ao final do mês.

## Novo cenário na Industria de IA

Imagine se foguetes fossem baratos. A NASA poderia simplesmente enviar 20 foguetes mais ou menos na direção da lua.
Se um deles pousasse, perfeito. Se nenhum pousasse, era só lançar os próximos 20.

![Como estão seus foguetes ?](nasa.png)

Isso mapeia exatamente como agents são frequentemente usados:

- Você dá apenas um pouco de contexto.
- Você escreve um prompt, mas não coloca muito esforço nele.
- Você envia o agent.
- Se voltar com um bom resultado, ótimo. Se não, você simplesmente envia o próximo agent.

>🚀 Você quer enviar poucos foguetes (agentes) com alta precisão - o que automaticamente otimiza o combustível (AI Credits). 

>💡 Otimize o uso de AI Credits — mas não motivado pelo custo, e sim pela qualidade.

![Faça cada token contar !](token.png)

## Cobrança do Copilot Baseada em Uso

O preço da licença continua o mesmo
- Business $19 usuário/mês, 
- Enterprise $39/usuário/mês.

Next edit suggestions e code-completion 
  - Não consomem AI Credits em planos Business e Enterprise.

AI Credits por licença (mensais)
- Copilot Business: $19 AI Credits
- Copilot Enterprise: $39 AI Credits

Nos meses de junho, julho, e agosto 2026 os AI Credits mensais serão aumentados de forma promocional (para usuários que já estavam ativos antes de 1 de junho) para:

- Copilot Business: $30 AI Credits
- Copilot Enterprise: $70 AI Credits

Cada token tem preço baseado no modelo usado, e o total é convertido em AI credits, onde:
> 1 AI credit = $0,01 USD

Esses créditos são adicionados a organização para ser distribuidos.

Links para mais informações:

- [GitHub Copilot is moving to usage-based billing](https://github.blog/news-insights/company-news/github-copilot-is-moving-to-usage-based-billing/)

- [Usage-based billing for organizations and enterprises](https://docs.github.com/en/copilot/concepts/billing/usage-based-billing-for-organizations-and-enterprises)

- [Budgets for usage-based billing](https://docs.github.com/en/copilot/concepts/billing/budgets-for-usage-based-billing)

- [Getting started with budget controls](https://docs.github.com/en/copilot/tutorials/budgets/getting-started-with-budget-controls)

- [Optimizing your budget configuration](https://docs.github.com/en/copilot/tutorials/budgets/optimizing-your-budget-configuration)

# O que essa mudança desbloqueia para você

- AI Credits compartilhados
- Evitar que usuários individuais causem cobranças excedentes
- Possibilita novas funcionalidades como
  - Janelas de contexto maiores
  - Melhor desempenho do Copilot e qualidade de resultados
  - Acesso a modelos mais novos e capazes conforme são lançados

## Otimização de agentes 🦾

### Entendendo do motor

#### LLM: Determinístico vs Probabilístico 

Um LLM é uma **máquina text-in, text-out**. 
- Por baixo dos panos, é uma **máquina de probabilidade de palavras**: dado o input + dados de treinamento, ele prevê a próxima palavra mais provável, depois a próxima, até formar uma frase.

- É claro que os modelos foram ficando cada vez melhores ao longo dos últimos anos e muitos detalhes adicionais foram adicionados para mais compute, maior precisão, vieses para desenvolvimento de software etc. – mas o princípio e as capacidades subjacentes ainda são basicamente isso.

<a id="dica-01" ><strong>🫶 Pense em Código, Prefira criar scripts para analisar arquivos em vez de entregá-los à IA.</strong></a>

<a id="dica-02" ><strong>🫶 Implemente controles determinísticos sempre que possível,para guiar a IA. (Testes unitários, validações, sinais de parada, etc...)</strong></a>

> 💡 A matemática não faz distinção entre alucinação e fato. É por isso que **context engineering** é a habilidade fundamental para trabalhar com agents. 


#### Contexto demais:
Informações irrelevantes conduzem o modelo para respostas incorretas. O LLM não consegue distinguir dados relevantes de irrelevantes—ele considera tudo ao calcular probabilidades.

![Contexto Bagunçado](room.png)

#### Contexto de menos:
A falta de informação crítica afasta o modelo do conhecimento correto. Pior, o modelo pode alucinar para preencher lacunas—e não há nenhuma mensagem de erro indicando que ele estava sem informação.

![travolta](travolta.gif)

> 💡 Com agentes, o contexto importa ainda mais — porque não é mais um único ida e volta. O agent conversa com o LLM em seu nome, dezenas de vezes, antes de voltar até você.

<a id="dica-03" ><strong>🫶 Refine -> Planeje -> Implemente</strong></a>
> Essa abordagem economiza tempo e tokens, pois os agents não carregam conhecimento desnecessário para a tarefa específica deles.

#### Agent Loop

![Agent Loop](https://code.visualstudio.com/assets/blogs/2026/05/15/agent-loop.png)
https://code.visualstudio.com/blogs/2026/05/15/agent-harnesses-github-copilot-vscode#_the-agent-loop

## 💎 Bora otimizar !!!

### 🤖 Otimize seu projeto para IA 

Certeza que já teve que dar manutenção em um repositório de código legado que não tinha nem se quer um README? Ou talvez até com um README, mas super desatualizado?

😅 Chato, né?

> 👀 Não desconte na IA ! 

![T800](https://static.wikia.nocookie.net/robotsupremacy/images/8/85/T800-endo.jpg/revision/latest?cb=20240701093346)

Se o seu projeto não tem um AGENTS.md ou um .github/copilot-instructions.md

<a id="dica-04" ><strong>🫶 Use o /init para sugerir instruções, e use seu conhecimento para validar !</strong></a>

Ao invés de em cada vez que for usar um agente ele ter que se contextualizar sobre o projeto, o que pode consumir muitos tokens, use o comando /init para dar um contexto inicial ao agente. Assim, ele já começa com uma boa base de conhecimento sobre o projeto e pode se concentrar em tarefas específicas, economizando tokens e melhorando a eficiência.

Ele vai criar um arquivo chamado AGENTS.MD, que vai estar sempre no contexto do agente, por isso ele deve ser sempre otimizado e atualizado. Pense nele como o README.md do seu projeto, mas otimizado para o agente.

### 👨‍💻 Otimize sua IDE para IA

<a id="dica-04" ><strong>🫶 Remova tools e MCPs desnecessários</strong></a>

#### Context Assembly

![https://code.visualstudio.com/docs/agents/concepts/context#_how-vs-code-assembles-context](https://code.visualstudio.com/assets/docs/agents/concepts/context-assembly.png)

A cada execução do agente ele tem que se contextualizar sobre as tools e MCPs disponíveis, o que pode consumir muitos tokens. Se você tem muitas tools e MCPs, o agente pode ficar confuso e ter dificuldade em escolher a ferramenta certa para a tarefa certa.


> 🔨 Pega o martelo pra mim !
![toolbox](toolbox.png)

### 🧾 Confira os logs do agente

> 👀 O agente tem logs ?

Sim, se conferimos os logs de uma aplicação, por que não conferir os logs de um agente ?

<a id="dica-05" ><strong>🫶 Confira os logs !!!</strong></a>

![output-logs](output-logs.png)

![https://code.visualstudio.com/docs/agents/agent-troubleshooting/chat-debug-view](https://code.visualstudio.com/assets/docs/agents/chat-debug-view/agent-flow-chart-v2.png)

![https://code.visualstudio.com/docs/agents/agent-troubleshooting/chat-debug-view#_logs-view](https://code.visualstudio.com/assets/docs/agents/chat-debug-view/agent-logs.png)

### Output Token

![output-token](output.png)

Você sabia que o custo de um output token pode ser 5x mais caro que um input token ?

Podemos evitar esse comportamento verboso e muitas vezes desnecessário, definindo o formato de resposta que queremos receber.

![pricing-tables](pricing.png)

- [copilot](https://docs.github.com/en/copilot/reference/copilot-billing/models-and-pricing#pricing-tables)

- [openai](https://openai.com/api/pricing/)

- [claude](https://platform.claude.com/docs/en/about-claude/pricing)

<a id="dica-06" ><strong>🫶 Economize no output token, defina o formato de resposta.</strong></a>

### Model Engenieering

![Matando barata com bazuca](opus.png)

Nem só de **Claude Opus** vive um agente !

- Use **modelos mais leves** para edições rápidas, geração de código padrão e perguntas diretas.
- Use **modelos de raciocínio** para refatoração complexa, decisões arquiteturais e debugging em múltiplas etapas.
- Use **seleção automática** de modelo para deixar o VS Code rotear cada requisição para um modelo eficiente que equilibre qualidade e custo.
- Use **agentes personalizados** com um modelo definido para rotear subtarefas específicas para modelos especializados e econômicos. Quando você invoca um agente personalizado como subagente, ele usa seu próprio modelo configurado em vez do modelo da sessão de chat.

[Guia de Modelos - GitHub](https://docs.github.com/en/copilot/reference/ai-models/model-comparison)

<a id="dica-07" ><strong>🫶 Nem toda tarefa precisa do Claude Opus !!!</strong></a>

<a id="dica-08" ><strong>🫶 Configure o esforço cognitivo e contexto do modelo quando necessário</strong></a>

### Cuidado com o Context Rot

![Perigo](https://static.wikia.nocookie.net/chespirito/images/c/cf/Chaves7532_480.jpg/revision/latest?cb=20180420231802&path-prefix=pt)
> ☠️ **PE-RI-GO**

Temos dois grandes problemas com a janela de contexto:

#### 1. Lost in the Middle (<50% dos tokens)
![lost-in-middle](lost-in-middle.png)

O modelo favorece o conteúdo no início e no fim da context window, não no meio. Isso geralmente é bom porque:
- Início = suas instruções, objetivos e plano (você quer isso priorizado)
- Fim = fluxo de trabalho atual (também importante)
- Meio = trabalho passado (menos relevante)

O problema aparece quando você troca de tarefa no meio da sessão. Exemplo: você começa com uma correção de bug, depois, no meio da conversa, diz "agora vamos implementar uma feature". À medida que a janela cresce, o modelo pode subitamente voltar para a correção de bug porque enviesa a declaração inicial em detrimento das recentes. 

**Solução**: use uma nova context window para cada tarefa distinta.

<a id="dica-09" ><strong>🫶 Uma tarefa, um contexto</strong></a>

<a id="dica-10" ><strong>🫶 Se quiser reaproveitar o contexto, use /fork</strong></a>


#### 2. Recency Bias (>50% dos tokens)*

![recent-bias](recent-bias.png)

Acima de 50% da capacidade, o modelo começa a favorecer apenas o fim da conversa. Ele esquece suas system instructions, custom instructions e o prompt original. O modelo desvia—fazendo coisas que você não entende baseado apenas no contexto recente.

**Solução**: não deixe sua token window crescer além do necessário. Dividir e conquistar as tarefas desde o início é a melhor forma de combater esse problema, seguido potencialmente por compactar uma conversa. 

>💡 Não encare isso como regra, sim como uma **tendência**. Não significa que o modelo **vai** esquecer tudo no meio. Não trabalhe com absolutos aqui. É claro que há cenários em que você precisará ir além de 50% da janela de contexto, e tudo bem. É só algo a ter em mente para otimizar seu uso.

<a id="dica-11" ><strong>🫶 Tarefas pequenas são mais fáceis de gerenciar</strong></a>

<a id="dica-12" ><strong>🫶 Caso tenha que manualmente compactar o contexto, pode se chamar o /compact com uma instrução, mas trate como excessão, não como regra.</strong></a>

## 🫶 DICAS

- [🫶 Pense em Código, Prefira criar scripts para analisar arquivos em vez de entregá-los à IA.](#dica-01)
- [🫶 Refine -> Planeje -> Implemente](#dica-02)
- [🫶 Use o /init para sugerir instruções, e use seu conhecimento para validar !](#dica-03)
- [🫶 Remova tools e MCPs desnecessários](#dica-04)
- [🫶 Confira os logs !!!](#dica-05)
- [🫶 Economize no output token, defina o formato de resposta.](#dica-06)
- [🫶 Nem toda tarefa precisa do Claude Opus !!!](#dica-07)
- [🫶 Configure o esforço cognitivo e contexto do modelo quando necessário](#dica-08)
- [🫶 Uma tarefa, um contexto](#dica-09)
- [🫶 Se quiser reaproveitar o contexto, use /fork](#dica-10)
- [🫶 Tarefas pequenas são mais fáceis de gerenciar](#dica-11)
- [🫶 Caso tenha que manualmente compactar o contexto, pode se chamar o /compact com uma instrução, mas trate como excessão, não como regra.](#dica-12)


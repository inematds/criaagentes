# OS Coach Memory

**Goal:** criar um agente para atender dúvidas das pessoas na minha clínica usando WhatsApp
**Who it is for:** quem escreve no WhatsApp da clínica. Público misto, mas a maioria é gente nova perguntando preço e horário. Também atende paciente já da casa.
**O que ele deve fazer (nas palavras do dono):** responder na hora quem pergunta preço, horário e convênio, e avisar uma pessoa quando o assunto for sério.
**Created:** 2026-07-15   **Updated:** 2026-07-15
**Current layer:** substrate (rebaixada na auditoria de 2026-07-15)
**Next action:** corrigir a tabela de preços do substrate/compendium.md com os valores reais da clínica. Só ela, primeiro.

## Layer status
- Identity: solid - Clínica Sorriso Prime, odontologia. Público misto com maioria nova perguntando preço e horário. Escala pelo Telegram, nunca opina sobre saúde, nunca negocia desconto, nunca afirma que tem vaga. Artefato: CLAUDE.md
- Substrate: in progress - bem organizado, mas os dados são fictícios. Contra o objetivo real, acerta zero perguntas hoje. Artefatos: substrate/sources.md, substrate/compendium.md, substrate/subject-matter-expertise/substrato-oficial-clinica.md
- Rules: solid - pior erro nomeado (afirmar como oficial o que não sabe) e um reflexo automático identificado (alerta de Telegram a cada escalonamento). Artefatos: rules/never.md, rules/always.md
- Skills: solid - uma skill real, com passos e critério de qualidade. Artefato: skills/responder-duvida-whatsapp/SKILL.md
- Tools: in progress - Google Agenda e Telegram bem definidos, mas o WhatsApp, canal do próprio objetivo, não está listado. Artefato: tools.md
- Agents: solid - um papel, uma skill orquestrada, portão de revisão de 5 perguntas antes de qualquer resposta sair. Artefato: agents/recepcionista-whatsapp/AGENT.md

## Decisions (append, newest last)
- 2026-07-15 OS iniciado na pasta criaagentes com o objetivo de atender dúvidas via WhatsApp.
- 2026-07-15 Público confirmado: os dois, com maioria de gente nova perguntando preço e horário. Isso define a prioridade do substrato: as respostas de preço, horário e convênio vêm primeiro.
- 2026-07-15 Função principal escolhida pelo dono: responder na hora as dúvidas repetidas e escalar para uma pessoa quando o assunto for sério. Ou seja, o assistente não é autônomo, ele tem um portão de saída para humano.
- 2026-07-15 É clínica de odontologia. Isso define o substrato: preço por procedimento, horário, convênios.
- 2026-07-15 Dois "nunca" definidos pelo dono: nada de opinião sobre sintoma/diagnóstico/tratamento, e nada de desconto ou negociação de pagamento. Ambos viram escalonamento para humano.
- 2026-07-15 Escalonamento é pelo TELEGRAM, não pelo WhatsApp, por escolha do dono: o WhatsApp é o canal do cliente e o aviso interno não pode poluir essa conversa. Isso já define uma conexão futura na camada de Tools.
- 2026-07-15 Identity marcada como solid: CLAUDE.md criado e passa no done-check (um estranho lê e sabe pra que serve e o que ele recusa).
- 2026-07-15 O dono entregou um substrato oficial pronto (arquivo fictício de teste, ~970 linhas). Guardado como fonte em subject-matter-expertise/ e destilado em compendium.md. Não foi copiado inteiro de propósito: o compêndio é o que o atendente lê no dia a dia, a fonte é o material completo para consulta e atualização.
- 2026-07-15 Substrate marcado como solid para informação: o compêndio responde as 10 perguntas mais repetidas com texto oficial. A parte de "tem vaga tal dia" não é resolvível por texto, depende da agenda, e por isso vira encaminhamento até a camada de Tools decidir.
- 2026-07-15 CLAUDE.md ajustado a partir do substrato: nome da clínica, e dois nunca novos (não afirmar disponibilidade de agenda, não usar a palavra confirmada sem a agenda oficial). O substrato mostrou que "clínica aberta" ser lido como "tem vaga" é o erro mais provável do assistente.

- 2026-07-15 Rules escritas a partir das próprias listas do dono (capítulos 21, 22, 24, 26 e 27 do substrato), sem re-perguntar. O pior erro foi nomeado como a regra mãe: afirmar como oficial algo que não está no compêndio. Todos os outros nunca derivam dele.
- 2026-07-15 Reflexo automático (hook) definido: o alerta de Telegram tem que disparar sozinho no momento do encaminhamento, não depender de o assistente lembrar de fazer. Sem isso, "vou encaminhar" pode virar ninguém avisado.
- 2026-07-15 Regra de prioridade acrescentada por decisão de projeto: na dúvida entre duas prioridades, sobe. Alerta alto demais custa um susto, baixo demais custa um paciente.

- 2026-07-15 Primeira skill escrita: responder-duvida-whatsapp. É um trabalho que a recepção já faz à mão todo dia, então a skill foi ganha, não inventada. Estrutura: classificar em 3 caixas (responde sozinho / depende da agenda / é de gente) e agir conforme a caixa.
- 2026-07-15 Só uma skill por enquanto, de propósito. Agendamento e reagendamento parecem candidatos a skill própria, mas dependem da agenda, e sem a decisão de Tools eles são apenas o passo 4 desta skill (registrar e encaminhar).
- 2026-07-15 Critério de "resposta boa" definido em 5 checagens, com um teste rápido: onde é que isso está escrito? Se não dá pra apontar a linha no compêndio, o assistente inventou.

- 2026-07-15 Alerta do Telegram vai para um GRUPO com o dono e a recepção, escolha do dono. Resolve o gargalo de depender do dono ver a mensagem, mas cria o risco clássico de grupo (todo mundo acha que o outro pegou). Regra combinada para compensar: quem pegar escreve "peguei" no grupo.
- 2026-07-15 A agenda é o GOOGLE AGENDA, e o acesso será SOMENTE LEITURA. Isso muda o passo 4 da skill: ele passa a poder dizer "quinta de tarde tem horário" em vez de encaminhar todo pedido de horário. O que não muda: ver horário livre não é consulta marcada, a palavra "confirmada" continua sendo da recepção.
- 2026-07-15 Escrita na agenda recusada por enquanto, de propósito. Erro de leitura custa um "vou confirmar" à toa. Erro de escrita custa paciente na porta sem vaga, ou horário marcado em cima de outro. Não é o mesmo tamanho de estrago.
- 2026-07-15 Nada de prontuário, exames ou financeiro nas conexões: não respondem preço nem horário, que são a maioria do que chega. Mais fio do que o objetivo pede é mais estrago possível sem mais ajuda.

- 2026-07-15 Agente criado: recepcionista-whatsapp. Um papel só, estreito de propósito. Não virou "agente que cuida da clínica", virou "agente que cuida de uma conversa, do oi até a resposta ou o encaminhamento".
- 2026-07-15 Portão de revisão obrigatório com 5 perguntas, sendo a primeira "onde é que isso está escrito?". Motivo: o erro perigoso não é a resposta feia, é a resposta bonita e inventada, que passa justamente por parecer certa.
- 2026-07-15 Isolamento por conversa: uma conversa é uma caixa fechada, nunca misturar dois pacientes nem usar dado de um para responder outro.
- 2026-07-15 Três métricas de saúde definidas: quanto ele resolve sozinho (se pouco, compêndio pobre), quanto ele encaminha à toa (se muito, compêndio mal organizado), e se ele já afirmou algo não escrito (falha grave, uma só já é motivo de parar).

## Open questions
- O substrato é FICTÍCIO. Antes de ligar num WhatsApp real, trocar preço, endereço, telefone, profissionais e políticas pelos dados verdadeiros da clínica.
- Combinar com a recepção a regra do "peguei" no grupo do Telegram. É regra de gente, não de software, e sem ela o grupo falha em silêncio.
- Dados sensíveis: nome de paciente, CPF, resultado de exame nunca devem entrar nos arquivos desta pasta. Checado em 2026-07-15: está limpo, nenhum dado real de paciente nos arquivos.
- O tools.md não diz como o assistente encosta no WhatsApp. Faltam três respostas: em que número ele vive, quem é dono da conta, e o que acontece quando a recepção assume a conversa no meio.
- Nenhuma conversa foi testada ainda. Seis camadas escritas, zero mensagens rodadas.

## Audit log (append)
- 2026-07-15 Estrutura sólida sobre dados falsos. Substrate e Tools rebaixadas para in progress: o compêndio é fictício e o tools.md esqueceu o WhatsApp, que é o canal do próprio objetivo. Identity, Rules, Skills e Agents passam.

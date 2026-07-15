# OS Audit - 2026-07-15
Goal: criar um agente para atender dúvidas das pessoas na minha clínica usando WhatsApp

## Scorecard

| Layer | Score | Why (one specific line) |
|---|---|---|
| Identity | Solid | `CLAUDE.md` tem 26 linhas, nomeia a clínica, o público real (maioria nova perguntando preço e horário) e quatro recusas testáveis, incluindo a que importa: nunca dizer que tem vaga |
| Substrate | **Started** | `compendium.md` está bem organizado e responde as 10 perguntas mais repetidas, mas cada valor dele é FICTÍCIO. Contra o objetivo (atender as pessoas da SUA clínica), ele hoje acerta zero perguntas |
| Rules | Solid | `never.md` nomeia o pior erro (afirmar como oficial o que não sabe) e derivam os outros dele, e `always.md` identifica o reflexo do alerta de Telegram com prioridade |
| Skills | Solid | `responder-duvida-whatsapp/SKILL.md` captura um trabalho que a recepção já faz à mão, com as 3 caixas e 5 checagens de qualidade |
| Tools | **Started** | `tools.md` define bem Google Agenda (leitura) e Telegram (envio ao grupo), mas não lista o WhatsApp, que é o canal do próprio objetivo. A conexão mais importante do OS não está no arquivo de conexões |
| Agents | Solid | `recepcionista-whatsapp/AGENT.md` tem um papel estreito, orquestra a skill que existe, e tem portão de revisão obrigatório de 5 perguntas |

Nenhuma camada é Compounding. Nada aqui melhora sozinho ainda: não existe um caminho que leve o erro de volta para o compêndio.

## O que está genuinamente bom

- **A estrutura aguenta.** Identidade, Regras, Skill e Agente estão amarrados na mesma ideia (só afirmo o que está escrito) e se sustentam mesmo se todo o conteúdo do compêndio for trocado amanhã. Isso é raro e é o motivo de a troca dos dados ser trabalho de digitar, não de refazer.
- **As recusas são testáveis.** "Nunca dizer que tem vaga" e "confirmada só com a agenda oficial" são checáveis por qualquer pessoa lendo uma conversa. Regra que não dá para checar não protege ninguém.
- **O escopo foi defendido.** Sem escrita na agenda, sem prontuário, sem financeiro. Cada "não" desses é um estrago que não vai acontecer.

## Checagem de dado sensível

Você marcou nome de paciente, CPF e exame como coisas que não podem virar arquivo. Passei os arquivos: nenhum dado real de paciente foi escrito. O "João Pereira, (51) 98888-1212" que aparece no substrato é o exemplo fictício do seu próprio documento, e o modelo de alerta em `rules/always.md` usa espaços vazios, não gente. Está limpo.

Fica um alerta para quando isso virar real: exemplo de alerta com paciente de verdade nunca pode ser colado num arquivo desta pasta.

## The three moves that matter most (in order)

1. **Substrate - trocar os dados fictícios pelos reais da sua clínica, começando por `compendium.md`.**
   Preço, endereço, telefone, horário, convênio, profissionais. É a única coisa aqui que impede o OS de funcionar hoje. Você montou um assistente cujo dever é nunca inventar, e entregou a ele um livro inteiro de invenções. Enquanto isso não mudar, cada resposta que ele der vai estar tecnicamente correta e factualmente falsa, que é o pior dos dois mundos. Não é trabalho intelectual, é trabalho de digitar. Todo o resto do OS já está esperando por isso.

2. **Tools - decidir e escrever no `tools.md` como ele encosta no WhatsApp.**
   O seu objetivo tem a palavra WhatsApp dentro dele, e o seu arquivo de conexões não menciona o WhatsApp. A gente ligou os dois fios auxiliares (agenda e alerta) e esqueceu o cano principal. Precisa de três respostas: em qual número ele vive (o da clínica ou um novo), quem fica dono da conta, e o que acontece quando uma pessoa da recepção quiser assumir a conversa no meio. Essa última é a que quebra na prática: se a recepção responder por cima dele sem ele saber, o paciente recebe duas respostas diferentes.

3. **Testar com dez conversas de mentira antes de ligar em qualquer coisa.**
   Você tem seis camadas escritas e zero mensagens rodadas. Escolha dez mensagens reais que chegaram no WhatsApp de vocês nos últimos dias, incluindo as chatas (o pedido de desconto disfarçado, a pessoa com dor às 23h, a mãe perguntando de outra pessoa), e passe uma por uma pelo `AGENT.md`. Em cada resposta, faça a pergunta do portão: onde é que isso está escrito? Toda vez que a resposta não estiver, você achou um buraco no compêndio, e ele custa cinco minutos agora ou um paciente depois.

## The one thing to do next

Abra o `substrate/compendium.md` e corrija **a tabela de preços**, só ela. É a resposta mais pedida no seu WhatsApp e a que causa o maior estrago quando está errada. Trinta minutos com a tabela real da clínica na mão. Depois disso, o resto do compêndio é o mesmo trabalho, só que mais tranquilo.

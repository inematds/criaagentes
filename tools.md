# Conexões (os fios que saem pra fora)

Duas conexões, e só duas. O padrão é **só olhar, nunca mexer**. É uma janela, não a chave da casa.

---

## 1. Google Agenda (a agenda da clínica)

- **Para que serve:** responder "tem vaga quinta de tarde?" com a verdade, em vez de encaminhar tudo para a recepção.
- **Acesso: SOMENTE LEITURA.** O assistente olha e diz o que vê. Ele não cria, não move e não apaga evento nenhum. Quem marca é a recepção.
- **Por que só leitura:** um assistente que escreve na agenda pode marcar em cima de outro paciente, ou marcar um horário que a recepção já tinha prometido no telefone. O prejuízo de um erro de escrita é um paciente na porta sem vaga. O prejuízo de um erro de leitura é ele dizer "vou confirmar" à toa. Não é o mesmo tamanho.
- **O que ele pode dizer com isso na mão:** que existe horário livre em tal dia e turno.
- **O que ele continua sem poder dizer:** que a consulta está **confirmada**. Ver um buraco livre na agenda não é a mesma coisa que ter uma consulta marcada. A palavra "confirmada" continua sendo da recepção.
- **Como ligar depois:** o Google Agenda tem um conector pronto. Basta dar acesso de leitura ao calendário da clínica. Trabalho de minutos, não de semanas.

## 2. Telegram (o alerta para a equipe)

- **Para que serve:** avisar a equipe toda vez que o assistente encaminha. É o reflexo automático descrito em `rules/always.md`.
- **Acesso: ENVIO, apenas para um destino.** Um grupo com o dono e a recepção. O assistente só escreve nesse grupo, e não lê conversa de ninguém.
- **Formato da mensagem:** o modelo de alerta em `rules/always.md`, com a prioridade normal, alta ou urgente.
- **Como ligar depois:** criar um bot no Telegram (é gratuito, feito pelo próprio Telegram), colocar o bot no grupo, e apontar os alertas para lá.

### A regra que faz o grupo funcionar

Um grupo resolve o problema do gargalo: não depende do dono ver a mensagem. Mas cria outro, e vale nomear:

> **Em grupo, todo mundo acha que o outro já respondeu.**

Por isso a regra combinada é: **quem pegar, escreve "peguei" no grupo.** Sem isso, um alerta de dor forte pode ficar quinze minutos com três pessoas olhando e ninguém agindo.

---

## Segredos

Nenhuma senha, chave ou token vive nesta pasta. O acesso ao Google Agenda e o token do bot do Telegram ficam guardados fora daqui, no lugar onde o assistente for rodar. Esta pasta é o cérebro dele, não o chaveiro.

## O que fica de fora, e por quê

- **WhatsApp para aviso interno:** não. O WhatsApp é o canal do paciente. Aviso interno vai para o Telegram, foi decisão do dono e continua valendo.
- **Escrita na agenda:** não, por enquanto. Se um dia a recepção estiver sobrecarregada e vocês quiserem que ele marque sozinho, isso é uma conversa nova, com testes, e depois de meses vendo ele acertar na leitura.
- **Prontuário, exames, sistema financeiro:** não. Nada disso responde as perguntas de preço e horário, que são a maioria do que chega. Ligar mais fio do que o objetivo pede é aumentar o estrago possível sem aumentar a ajuda.

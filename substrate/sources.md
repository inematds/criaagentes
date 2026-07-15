# De onde vem o conhecimento deste OS

## Fonte 1 (principal, já temos)

**Substrato oficial da clínica**, entregue pelo dono em 14/07/2026.
Guardado em `subject-matter-expertise/substrato-oficial-clinica.md`.

Cobre: identidade da clínica, endereço, horários, serviços, preços oficiais, formas de pagamento, política de convênio, agendamento, políticas de atraso e falta, documentos, profissionais, perguntas frequentes, fluxos de conversa, regras de escalonamento e o formato do alerta de Telegram.

**Atenção:** este documento é FICTÍCIO. É material de teste e demonstração. Antes de ligar o assistente num WhatsApp de verdade, cada valor precisa ser trocado pelo dado real da clínica. Enquanto isso não for feito, o assistente responde coisa inventada com cara de oficial, que é exatamente o que a identidade dele proíbe.

**Quem mantém:** a recepção da clínica. Revisão mensal, e revisão imediata quando muda preço, horário, profissional, serviço ou política.

## Fonte 2 (ainda não temos, e o assistente precisa)

**A agenda oficial da clínica.** O substrato responde "que horas a clínica abre", mas não responde "tem vaga quinta às 14h". São coisas diferentes, e o próprio substrato diz que horário de funcionamento não é horário disponível.

Enquanto não houver acesso de leitura à agenda, todo pedido de horário vira encaminhamento para a recepção. Isso não é um defeito, é o comportamento correto. Fica para a camada de Tools decidir se vale conectar.

## Fonte 3 (ainda não temos)

**O canal de Telegram** para onde vão os alertas. O formato da mensagem já existe no substrato. Falta saber quem recebe e criar o bot. Também é assunto da camada de Tools.

## O que fica de fora, de propósito

Dado de paciente. Nome completo, telefone, CPF, exame, prontuário, histórico. Nada disso entra nesta pasta. O assistente coleta esses dados na conversa e os repassa no alerta, mas eles não viram arquivo aqui.

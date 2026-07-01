# DOCUMENTO DE REGRAS DE NEGÓCIO

## Projeto

**Micro-SaaS de Confirmação Automatizada de Agendamentos via WhatsApp**

---

# Objetivo

Este documento define todas as regras de negócio do sistema. As regras aqui descritas representam o comportamento oficial esperado da aplicação e devem ser respeitadas durante todo o desenvolvimento do software.

Cada regra recebe um identificador (RN) para facilitar futuras manutenções, documentação e implementação.

---

# Índice

* RN001 – Empresas
* RN002 – Usuários
* RN003 – Profissionais
* RN004 – Pacientes
* RN005 – Consultas
* RN006 – Alteração de Consultas
* RN007 – Exclusão de Consultas
* RN008 – Lembretes Automáticos
* RN009 – Confirmação do Paciente
* RN010 – Link de Confirmação
* RN011 – Dashboard
* RN012 – Histórico
* RN013 – WhatsApp
* RN014 – Mensagens
* RN015 – Assinatura
* RN016 – Segurança
* RN017 – Validações Gerais

---

# RN001 – Empresas

### RN001.01

Cada empresa cadastrada possui ambiente totalmente isolado.

Uma empresa nunca poderá visualizar informações pertencentes a outra empresa.

---

### RN001.02

Cada unidade física possui sua própria conta no sistema.

Mesmo pertencendo ao mesmo grupo empresarial, cada clínica utilizará um login independente.

---

### RN001.03

O CNPJ não poderá ser alterado após a criação da conta.

Caso seja necessário utilizar outro CNPJ, uma nova conta deverá ser criada.

---

### RN001.04

O WhatsApp conectado poderá ser alterado a qualquer momento.

---

### RN001.05

O e-mail principal da conta não poderá ser alterado.

---

# RN002 – Usuários

### RN002.01

A empresa poderá possuir até três administradores.

Todos possuem exatamente as mesmas permissões administrativas.

---

### RN002.02

Qualquer administrador poderá:

* redefinir senha;
* alterar configurações;
* excluir outro administrador;
* cadastrar administradores.

---

### RN002.03

Não existe limite de secretárias cadastradas.

---

# RN003 – Profissionais

### RN003.01

O cadastro de profissionais é opcional.

---

### RN003.02

Caso a empresa utilize profissionais, eles deverão ser previamente cadastrados.

---

### RN003.03

Durante o cadastro da consulta o profissional será selecionado em uma lista.

Não será necessário digitá-lo manualmente.

---

### RN003.04

A empresa poderá optar por ocultar o nome do profissional do paciente.

---

# RN004 – Pacientes

### RN004.01

Toda consulta deve possuir:

* nome do paciente;
* telefone;
* data;
* horário.

---

### RN004.02

O telefone é obrigatório.

Sem telefone não é possível enviar lembretes.

---

### RN004.03

Ao informar um telefone já existente, o sistema localizará automaticamente o paciente anteriormente cadastrado.

---

### RN004.04

O sistema preencherá automaticamente os dados encontrados.

---

### RN004.05

Pacientes com consultas futuras não poderão ser excluídos.

O sistema exibirá aviso informando que existem consultas pendentes.

---

# RN005 – Consultas

### RN005.01

Somente a empresa poderá cadastrar consultas.

---

### RN005.02

Consultas somente poderão ser cadastradas com antecedência mínima de cinco horas.

---

### RN005.03

Não será permitido cadastrar consultas no passado.

---

### RN005.04

Consultas poderão ser cadastradas para qualquer data futura.

---

### RN005.05

Cada consulta possuirá um único status principal.

Os status possíveis são:

* Agendada
* Mensagem Enviada
* Confirmada
* Cancelada
* Solicitação de Alteração

---

# RN006 – Alteração de Consultas

### RN006.01

Uma consulta poderá ser alterada enquanto não estiver concluída.

---

### RN006.02

Caso a data ou horário sejam alterados, todos os lembretes antigos deverão ser cancelados automaticamente.

---

### RN006.03

Após cancelar os lembretes anteriores, novos lembretes serão programados automaticamente.

---

### RN006.04

Caso dois usuários tentem editar simultaneamente a mesma consulta, o sistema deverá informar que ela foi modificada por outro usuário e solicitar o recarregamento das informações.

---

# RN007 – Exclusão de Consultas

### RN007.01

A empresa poderá excluir consultas futuras.

---

### RN007.02

Toda exclusão deverá ficar registrada no histórico.

---

# RN008 – Lembretes Automáticos

### RN008.01

O primeiro lembrete poderá ser configurado entre 48 horas e o horário da consulta.

---

### RN008.02

O sistema recomendará que o primeiro lembrete seja configurado entre 48 e 24 horas antes da consulta.

---

### RN008.03

O segundo lembrete é opcional.

---

### RN008.04

Caso utilizado, o segundo lembrete poderá ser configurado entre 12 horas e o horário da consulta.

---

### RN008.05

Os lembretes serão enviados automaticamente.

Nenhuma ação manual será necessária após o cadastro da consulta.

---

# RN009 – Confirmação do Paciente

### RN009.01

O paciente confirmará sua presença através de um link enviado pelo WhatsApp.

---

### RN009.02

O paciente poderá escolher apenas uma opção.

---

### RN009.03

As opções disponíveis serão:

* Confirmar consulta
* Cancelar consulta
* Solicitar alteração

---

### RN009.04

Após selecionar uma opção, ela será considerada definitiva.

---

### RN009.05

Caso o paciente acesse novamente o link, visualizará apenas o status já registrado.

---

# RN010 – Link de Confirmação

### RN010.01

Cada consulta possuirá um link exclusivo.

---

### RN010.02

O link expirará imediatamente após a primeira resposta do paciente.

---

### RN010.03

O link não poderá ser reutilizado.

---

# RN011 – Dashboard

### RN011.01

O dashboard exibirá:

* Consultas Agendadas
* Mensagens Enviadas
* Confirmadas
* Canceladas
* Solicitações de Alteração

---

### RN011.02

Os dados serão atualizados em tempo real.

---

### RN011.03

Será possível filtrar o histórico por período.

---

### RN011.04

O sistema exibirá o mês atual e permitirá consultas de períodos anteriores.

---

# RN012 – Histórico

### RN012.01

Toda alteração relevante será registrada.

---

### RN012.02

Serão registrados:

* criação;
* edição;
* exclusão;
* confirmações;
* cancelamentos;
* alterações.

---

### RN012.03

Os registros permanecerão disponíveis por 30 dias.

---

# RN013 – WhatsApp

### RN013.01

Cada empresa conectará seu próprio WhatsApp através de QR Code.

---

### RN013.02

Caso o WhatsApp seja desconectado, o sistema deverá:

* exibir alerta;
* informar o problema;
* impedir novos envios até a reconexão.

---

### RN013.03

Mensagens com falha permanecerão registradas e poderão ser reenviadas manualmente.

---

# RN014 – Mensagens

### RN014.01

A empresa poderá editar completamente os textos enviados.

---

### RN014.02

O sistema fornecerá um modelo padrão inicial.

---

### RN014.03

Será permitido utilizar emojis.

---

### RN014.04

As mensagens utilizarão variáveis automáticas, como:

* nome do paciente;
* data;
* horário;
* profissional (quando utilizado);
* link de confirmação.

---

RN015 – Assinatura

RN015.01
O sistema oferecerá um período de teste gratuito de 14 dias para todas as novas empresas cadastradas.

RN015.02
Durante o período de teste, todas as funcionalidades do SaaS permanecerão liberadas, sem limitações de uso.

RN015.03
Ao término dos 14 dias, caso nenhum plano seja contratado, o acesso ao sistema será bloqueado automaticamente até a confirmação do pagamento.

RN015.04
O sistema possuirá um único plano, com as seguintes modalidades de contratação:

• Mensal — R$ 120,00
• Trimestral — R$ 330,00 (aproximadamente 8% de desconto)
• Semestral — R$ 600,00 (aproximadamente 17% de desconto)
• Anual — R$ 1.140,00 (aproximadamente 25% de desconto)

RN015.05
Independentemente da modalidade contratada, todas as funcionalidades do sistema permanecerão ilimitadas para:

• Consultas;
• Profissionais;
• Mensagens enviadas.

RN015.06
Todas as cobranças, renovações e confirmações de pagamento serão realizadas através da plataforma Asaas.

RN015.07
Ao cancelar a assinatura, a empresa perderá o acesso ao sistema, porém seus dados permanecerão armazenados por até 30 dias.

RN015.08
Durante esse período de 30 dias, a empresa poderá reativar sua assinatura e recuperar integralmente todos os seus dados.

RN015.09
Após o período de 30 dias, os dados poderão ser removidos definitivamente do sistema, conforme a política de retenção de dados do SaaS.
---

# RN016 – Segurança

### RN016.01

Todos os acessos deverão utilizar HTTPS.

---

### RN016.02

Cada empresa terá acesso apenas aos seus próprios dados.

---

### RN016.03

As informações serão protegidas por autenticação e controle de permissões.

---

### RN016.04

Toda alteração importante deverá gerar registro de auditoria.

---

# RN017 – Validações Gerais

### RN017.01

Campos obrigatórios deverão ser validados antes do salvamento.

---

### RN017.02

Sempre que ocorrer um erro, o sistema deverá informar claramente:

* motivo do erro;
* como corrigir;
* ação necessária.

---

### RN017.03

Caso uma validação impeça uma operação, nenhuma informação deverá ser salva parcialmente.

---

### RN017.04

Todas as regras descritas neste documento possuem prioridade sobre qualquer comportamento não especificado durante o desenvolvimento.

---

# Conclusão

Este documento estabelece o conjunto oficial de regras de negócio do Micro-SaaS de Confirmação Automatizada de Agendamentos.

Toda implementação do backend, frontend, banco de dados, APIs, automações e integrações deverá seguir integralmente estas regras, garantindo consistência, previsibilidade e padronização do sistema ao longo de sua evolução.

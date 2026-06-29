# DOCUMENTO DE FLUXO COMPLETO DO SISTEMA

## Projeto

**Micro-SaaS de Confirmação Automatizada de Agendamentos via WhatsApp**

---

# Objetivo

Este documento define todo o fluxo operacional do sistema, descrevendo como cada funcionalidade funciona desde o cadastro da empresa até a confirmação da consulta pelo paciente. O objetivo é servir como referência oficial para o desenvolvimento do backend, frontend e futuras implementações do SaaS.

---

# FS-001 — Cadastro da Empresa

## Objetivo

Permitir que empresas e profissionais autônomos criem uma conta no sistema.

## Fluxo

Ao acessar a página inicial do SaaS, o usuário poderá escolher entre as opções:

* Entrar
* Criar Conta
* Continuar com Google

Caso escolha criar uma conta, o sistema solicitará:

* Nome da empresa ou profissional
* CPF ou CNPJ
* Telefone
* E-mail
* Senha

Após validar todas as informações, o sistema criará automaticamente:

* a empresa;
* o administrador principal;
* as configurações iniciais do sistema;
* o período de teste (caso esteja habilitado).

Ao finalizar, o usuário será direcionado para o primeiro acesso.

---

# FS-002 — Primeiro Acesso

## Objetivo

Preparar a empresa para começar a utilizar o sistema.

## Fluxo

No primeiro acesso o sistema solicitará que a empresa realize a configuração inicial.

A configuração consiste em:

* conectar o WhatsApp;
* cadastrar os profissionais (opcional);
* configurar o primeiro lembrete;
* configurar o segundo lembrete (opcional);
* personalizar as mensagens automáticas.

Após concluir essa etapa, a empresa será direcionada para o Dashboard principal.

---

# FS-003 — Login

## Objetivo

Permitir acesso seguro ao sistema.

## Fluxo

O usuário poderá realizar login utilizando:

* E-mail e senha;
* Continuar com Google.

Caso utilize o Google, o sistema verificará automaticamente se aquele e-mail já possui cadastro.

Se existir uma conta vinculada:

o login será realizado automaticamente.

Caso não exista:

o sistema oferecerá a criação de uma nova conta.

A sessão permanecerá ativa enquanto o usuário utilizar o sistema com frequência.

Caso permaneça aproximadamente trinta dias sem acessar, será necessário realizar um novo login.

---

# FS-004 — Dashboard

## Objetivo

Apresentar um resumo geral da operação da empresa.

O Dashboard exibirá em tempo real:

* consultas agendadas;
* consultas confirmadas;
* consultas canceladas;
* solicitações de alteração;
* alertas do sistema.

Sempre que existir algum problema operacional, será exibido um indicador visual.

Ao clicar nesse indicador, o sistema apresentará uma explicação detalhada do problema juntamente com as orientações necessárias para sua correção.

---

# FS-005 — Cadastro de Profissionais

## Objetivo

Permitir que a empresa cadastre seus profissionais.

Cada profissional poderá possuir:

* nome;
* especialidade (opcional).

O cadastro facilitará o preenchimento das consultas, permitindo apenas selecionar o profissional durante o agendamento.

O uso dessa funcionalidade será opcional.

---

# FS-006 — Cadastro de Consulta

## Objetivo

Cadastrar rapidamente uma consulta.

Campos obrigatórios:

* Nome do paciente;
* Telefone;
* Data;
* Horário.

Campo opcional:

* Profissional.

Ao informar o telefone do paciente, o sistema verificará automaticamente se ele já existe no banco de dados daquela empresa.

Caso exista:

os dados serão preenchidos automaticamente.

Após salvar a consulta, o sistema criará automaticamente todos os lembretes programados.

---

# FS-007 — Alteração de Consulta

## Objetivo

Permitir alterações em consultas futuras.

Sempre que uma consulta for alterada:

* os lembretes antigos serão cancelados;
* novos lembretes serão automaticamente agendados.

Todas as alterações ficarão registradas no histórico do sistema.

---

# FS-008 — Exclusão de Consulta

## Objetivo

Permitir a exclusão de consultas futuras.

Ao excluir uma consulta:

* todos os lembretes relacionados serão cancelados;
* o histórico registrará a exclusão.

Caso existam consultas futuras vinculadas ao paciente, o sistema exibirá um aviso antes da exclusão.

---

# FS-009 — Agendamento Automático dos Lembretes

## Objetivo

Automatizar completamente o envio dos lembretes.

Sempre que uma consulta for cadastrada, o sistema verificará as configurações definidas pela empresa.

Exemplo:

Primeiro lembrete:

48 horas antes.

Segundo lembrete:

2 horas antes.

Automaticamente o Celery criará todas as tarefas necessárias.

Nenhum processo manual será necessário.

---

# FS-010 — Envio Automático via WhatsApp

## Objetivo

Enviar mensagens automaticamente aos pacientes.

Quando chegar o horário programado, o Celery executará a tarefa.

O backend enviará a solicitação para a Evolution API.

A Evolution API utilizará o WhatsApp conectado da empresa para realizar o envio.

A mensagem poderá conter automaticamente:

* nome do paciente;
* nome da empresa;
* data;
* horário;
* profissional (quando utilizado);
* link exclusivo de confirmação.

Essas informações serão inseridas automaticamente através de variáveis dinâmicas.

Todo envio ficará registrado no histórico.

---

# FS-011 — Página de Confirmação

## Objetivo

Permitir que o paciente confirme sua consulta.

Ao clicar no link recebido pelo WhatsApp, o sistema validará automaticamente um token exclusivo daquela consulta.

Após validar o token, será apresentada uma página contendo:

* nome da empresa;
* data;
* horário;
* profissional (quando utilizado).

O paciente poderá escolher apenas uma opção:

* Confirmar consulta;
* Cancelar consulta;
* Solicitar alteração.

Após selecionar qualquer opção:

* o status será atualizado imediatamente;
* o link será bloqueado para novas alterações.

Caso seja acessado novamente, apenas o status anteriormente escolhido será exibido.

---

# FS-012 — Segundo Lembrete

## Objetivo

Enviar um lembrete final antes da consulta.

Caso essa funcionalidade esteja ativada, o sistema enviará automaticamente um segundo lembrete.

Esse envio ocorrerá independentemente do paciente já ter respondido anteriormente.

O objetivo será apenas recordar o horário da consulta.

---

# FS-013 — Dashboard em Tempo Real

## Objetivo

Atualizar automaticamente os indicadores do sistema.

Sempre que ocorrer:

* envio de mensagem;
* confirmação;
* cancelamento;
* solicitação de alteração.

Os indicadores serão atualizados automaticamente.

O Dashboard exibirá inicialmente os dados do mês atual.

Também permitirá consultas por qualquer período através dos filtros disponíveis.

---

# FS-014 — Histórico

## Objetivo

Registrar todas as ações relevantes realizadas no sistema.

Serão registrados:

* criação de consultas;
* alterações;
* exclusões;
* confirmações;
* cancelamentos;
* alterações de configurações;
* conexões do WhatsApp;
* alterações administrativas.

Os registros permanecerão disponíveis pelos últimos trinta dias.

---

# FS-015 — Conexão do WhatsApp

## Objetivo

Permitir a integração do WhatsApp da empresa com o SaaS.

Fluxo:

A empresa acessa as configurações.

Seleciona a opção conectar WhatsApp.

O sistema gera um QR Code.

O QR Code é escaneado pelo WhatsApp da empresa.

Após a autenticação, a conexão é estabelecida.

Caso o WhatsApp seja desconectado posteriormente:

o sistema exibirá um alerta visual no Dashboard e bloqueará automaticamente novos envios até que a conexão seja restabelecida.

---

# FS-016 — Assinatura

## Objetivo

Gerenciar a assinatura da empresa.

A empresa poderá:

* visualizar seu plano;
* renovar assinatura;
* alterar a forma de pagamento;
* cancelar assinatura.

Quando uma assinatura for cancelada:

os dados permanecerão armazenados durante trinta dias.

Durante esse período será possível reativar a conta sem perda de informações.

Após esse prazo os dados poderão ser removidos definitivamente.

---

# FS-017 — Configurações

## Objetivo

Permitir que cada empresa personalize o funcionamento do sistema.

Será possível:

* alterar o horário do primeiro lembrete;
* alterar o horário do segundo lembrete;
* ativar ou desativar o segundo lembrete;
* editar os textos das mensagens;
* restaurar a mensagem padrão;
* alterar o nome da empresa;
* alterar telefone;
* alterar o WhatsApp conectado;
* alterar senha;
* gerenciar administradores;
* alterar preferências gerais do sistema.

Todas as alterações serão registradas automaticamente no histórico.

---

# FS-018 — Recuperação de Senha

## Objetivo

Permitir a recuperação segura da conta.

Fluxo:

O usuário seleciona "Esqueci minha senha".

Informa o e-mail cadastrado.

O sistema envia um link exclusivo para recuperação.

O usuário define uma nova senha.

Após a alteração, todos os links anteriores de recuperação são invalidados automaticamente.

---

# Resumo do Fluxo Geral do Sistema

A empresa cria sua conta.

Realiza o primeiro acesso.

Conecta seu WhatsApp.

Configura o sistema.

Cadastra seus profissionais.

Cadastra uma consulta.

O sistema agenda automaticamente os lembretes.

No horário programado, o Celery executa a tarefa.

A Evolution API envia a mensagem pelo WhatsApp da empresa.

O paciente acessa o link exclusivo.

Escolhe confirmar, cancelar ou solicitar alteração.

O Dashboard é atualizado automaticamente.

Todo o histórico permanece registrado para consulta pela empresa.

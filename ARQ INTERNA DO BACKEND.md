# DOCUMENTO DE ARQUITETURA INTERNA DO BACKEND

## Projeto

**Micro-SaaS de Confirmação Automatizada de Agendamentos via WhatsApp**

---

# Objetivo

Este documento define a arquitetura interna do backend do SaaS, estabelecendo como o sistema será organizado internamente, como os módulos se comunicam, como as regras de negócio serão executadas e como ocorrerá todo o processamento dos dados.

O objetivo é manter um backend organizado, escalável, seguro e de fácil manutenção.

---

# Arquitetura Escolhida

## Modelo Arquitetural

**Monólito Modular utilizando Django com Service Layer (Camada de Serviços).**

O sistema será desenvolvido em um único projeto Django, porém dividido em módulos independentes.

As regras de negócio não ficarão nas Views nem nos Models.

Toda regra de negócio será implementada em uma camada própria chamada **Services**, responsável por centralizar toda a lógica do sistema.

---

# Estrutura Geral do Backend

```text
Cliente

↓

Frontend

↓

Django URLs

↓

Views

↓

Services

↓ 

Models

↓

PostgreSQL

↓

Resposta ao Frontend
```

Cada camada possui apenas uma responsabilidade específica.

---

# BI-001 — Entrada das Requisições

## Objetivo

Receber todas as solicitações realizadas pelo Frontend.

## Fluxo

Toda requisição seguirá obrigatoriamente esta sequência:

```text
Frontend

↓

URL do Django

↓

View

↓

Service

↓

Model

↓

PostgreSQL

↓

Resposta
```

As Views terão apenas a responsabilidade de receber e devolver respostas.

Nenhuma regra de negócio será implementada diretamente nas Views.

---

# BI-002 — Camada de Serviços (Service Layer)

## Objetivo

Centralizar toda a lógica do sistema.

Toda decisão do sistema será executada nesta camada.

Exemplos:

* cadastrar consulta;
* alterar consulta;
* excluir consulta;
* conectar WhatsApp;
* enviar lembretes;
* alterar configurações;
* validar permissões;
* gerar históricos.

As Services poderão comunicar-se com outras Services quando necessário.

---

# BI-003 — Validação dos Dados

## Objetivo

Garantir que nenhuma informação inválida seja salva.

Antes de qualquer operação o backend validará automaticamente:

* usuário autenticado;
* empresa existente;
* CPF ou CNPJ válido;
* telefone preenchido;
* data válida;
* horário válido;
* consulta futura;
* permissões do usuário.

Caso qualquer validação falhe, nenhuma alteração será realizada.

---

# BI-004 — Execução das Regras de Negócio

## Objetivo

Aplicar todas as regras definidas no Documento de Regras de Negócio.

Exemplos:

* impedir consultas no passado;
* impedir confirmação duplicada;
* impedir acesso entre empresas;
* impedir alteração de dados proibidos;
* verificar configurações da empresa;
* verificar horários dos lembretes.

Nenhuma regra ficará espalhada pelo sistema.

Todas permanecerão centralizadas nas Services.

---

# BI-005 — Persistência dos Dados

## Objetivo

Salvar as informações permanentemente.

Após todas as validações e regras de negócio, os dados serão gravados no PostgreSQL.

Principais entidades manipuladas:

* Empresas;
* Usuários;
* Profissionais;
* Pacientes;
* Consultas;
* Notificações;
* Histórico.

Toda gravação ocorrerá através dos Models do Django.

---

# BI-006 — Agendamento das Tarefas

## Objetivo

Automatizar completamente os lembretes.

Sempre que uma consulta for cadastrada ou alterada:

O backend criará automaticamente as tarefas responsáveis pelos lembretes.

Fluxo:

```text
Consulta salva

↓

Service

↓

Celery

↓

Fila Redis
```

Caso a consulta seja alterada:

* os lembretes antigos serão cancelados;
* novos lembretes serão criados automaticamente.

---

# BI-007 — Motor de Automação

## Objetivo

Executar tarefas programadas.

O Celery será responsável por executar automaticamente:

* primeiro lembrete;
* segundo lembrete;
* tarefas futuras.

Antes de executar qualquer envio, o sistema verificará:

* consulta ainda existe;
* consulta continua ativa;
* consulta não foi cancelada;
* WhatsApp conectado;
* horário correto.

Somente após todas as verificações o envio será autorizado.

---

# BI-008 — Integração com WhatsApp

## Objetivo

Enviar mensagens utilizando a Evolution API.

Fluxo:

```text
Celery

↓

Service de Notificações

↓

Evolution API

↓

WhatsApp da Empresa

↓

Paciente
```

A Evolution API será responsável apenas pela comunicação com o WhatsApp.

Toda lógica continuará sendo responsabilidade do backend.

---

# BI-009 — Processamento da Confirmação

## Objetivo

Processar as respostas do paciente.

Quando o paciente acessar o link recebido:

O backend executará automaticamente:

* validar token;
* localizar consulta;
* verificar validade;
* atualizar status;
* registrar histórico;
* atualizar Dashboard.

Após uma resposta válida:

o token será bloqueado para novas alterações.

---

# BI-010 — Dashboard

## Objetivo

Fornecer indicadores atualizados em tempo real.

Sempre que ocorrer:

* confirmação;
* cancelamento;
* solicitação de alteração;
* criação de consulta;
* exclusão;
* envio de lembrete.

Os indicadores serão atualizados automaticamente.

O Dashboard consultará diretamente o PostgreSQL.

---

# BI-011 — Histórico

## Objetivo

Registrar todas as alterações importantes.

Serão registradas automaticamente:

* criação;
* edição;
* exclusão;
* login;
* alteração de senha;
* alteração de configurações;
* alteração de administradores;
* conexão do WhatsApp;
* confirmações;
* cancelamentos.

Os registros permanecerão armazenados durante trinta dias.

---

# BI-012 — Segurança

## Objetivo

Garantir proteção dos dados.

O backend implementará:

* autenticação;
* autorização;
* isolamento entre empresas;
* criptografia de senhas;
* comunicação HTTPS;
* validação de tokens;
* proteção contra acesso não autorizado.

Nenhum usuário poderá acessar informações pertencentes a outra empresa.

---

# BI-013 — Tratamento de Erros

## Objetivo

Garantir estabilidade do sistema.

Sempre que ocorrer qualquer erro:

* erro de banco;
* erro de conexão;
* erro da Evolution API;
* erro de autenticação;
* erro de validação;
* erro interno.

O backend registrará automaticamente o evento.

Quando possível, apresentará ao usuário uma mensagem clara indicando o problema e a forma de corrigi-lo.

---

# BI-014 — Organização dos Módulos

O projeto será dividido em módulos independentes.

Estrutura prevista:

```text
backend/

├── accounts/
├── companies/
├── professionals/
├── patients/
├── appointments/
├── notifications/
├── whatsapp/
├── dashboard/
├── history/
├── authentication/
├── services/
├── core/
```

Cada módulo possuirá sua própria responsabilidade.

Nenhum módulo deverá concentrar funcionalidades pertencentes a outro.

---

# Resumo da Arquitetura

**Framework:** Django

**Linguagem:** Python

**Arquitetura:** Monólito Modular

**Padrão interno:** Service Layer

**Banco de Dados:** PostgreSQL

**Fila de tarefas:** Redis

**Processamento assíncrono:** Celery

**Integração WhatsApp:** Evolution API

**Autenticação:** Django Authentication

**Comunicação:** HTTPS

**Histórico:** Centralizado

**Regras de Negócio:** Camada Services

**Objetivo Final:** manter um backend altamente organizado, escalável, seguro, desacoplado e preparado para evolução contínua sem comprometer a estrutura do sistema.

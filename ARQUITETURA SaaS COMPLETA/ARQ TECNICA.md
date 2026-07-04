


Arquitetura Técnica

# DOCUMENTO DE ARQUITETURA DO SAAS

## Projeto:

**Micro-SaaS de Confirmação Automatizada de Agendamentos via WhatsApp**

## Objetivo:

Criar uma plataforma SaaS B2B que reduz faltas em consultas e serviços agendados através de lembretes automáticos via WhatsApp, confirmação através de link e acompanhamento em painel administrativo.

O sistema não substitui o sistema de agenda da empresa. Ele funciona como uma camada de automação responsável pela confirmação e comunicação com clientes.

---

# 1. ARQUITETURA DE PRODUTO E FUNCIONAL

## Objetivo

Definir o que o sistema resolve, como funciona e quais são suas principais funcionalidades.

---

## Modelo do produto

Tipo:

**SaaS B2B Multi-Tenant**

Uma única plataforma utilizada por várias empresas.

Exemplos:

* clínicas odontológicas;
* clínicas médicas;
* estética;
* serviços com agendamento.

---

## Fluxo principal:

Empresa:

1. Cria conta.
2. Conecta seu WhatsApp.
3. Cadastra profissionais.
4. Cadastra consultas manualmente.
5. Sistema acompanha os horários.
6. Envia lembretes automáticos.
7. Paciente confirma através de link.
8. Dashboard atualiza os resultados.

---

## Funcionalidades principais:

### Gestão de profissionais

Cadastro de:

* médicos;
* dentistas;
* funcionários.

---

### Cadastro rápido de consultas

Informações:

* nome do paciente;
* telefone;
* profissional;
* data;
* horário.

---

### Automação de mensagens

Configuração:

* lembrete principal (exemplo: 24 horas antes);
* segundo lembrete opcional (exemplo: 2 horas antes).

---

### Confirmação do paciente

Paciente recebe link:

Visualiza:

* clínica;
* profissional;
* data;
* horário.

Pode:

* confirmar;
* cancelar;
* solicitar alteração.

---

### Dashboard

Mostra:

* consultas agendadas;
* confirmadas;
* canceladas;
* solicitações de alteração.

---

# 2. ARQUITETURA DE APLICAÇÃO E BACKEND

## Objetivo

Definir como o software será organizado internamente.

---

## Arquitetura escolhida:

**Monólito Modular com Django**

---

O sistema será um único projeto Django dividido em módulos.

Estrutura:

```
Sistema SaaS

├── Usuários
├── Empresas
├── Profissionais
├── Consultas
├── Notificações
├── WhatsApp
└── Dashboard
```

---

## Tecnologia principal:

Backend:

* Python
* Django

Frontend:

* Django Templates
* Bootstrap
* JavaScript

---

## Responsabilidades:

Django controla:

* usuários;
* empresas;
* permissões;
* consultas;
* regras do sistema;
* comunicação com APIs.

---

# 3. ARQUITETURA DE DADOS E MULTI-TENANCY

## Objetivo

Organizar e proteger os dados de várias empresas dentro do mesmo sistema.

---

## Banco de dados:

PostgreSQL

---

## Modelo escolhido:

**Banco único Multi-Tenant**

---

Cada registro possui vínculo com a empresa.

Exemplo:

Consulta:

```
id: 100

empresa_id: 5

Paciente:
João Silva

Data:
20/07

Horário:
14:00
```

---

A empresa só acessa seus próprios dados.

---

## Principais entidades:

### Empresa

Guarda:

* nome;
* configurações;
* plano.

---

### Usuário

Guarda:

* login;
* senha;
* permissões.

---

### Profissional

Guarda:

* nome;
* especialidade.

---

### Consulta

Guarda:

* paciente;
* telefone;
* data;
* horário;
* status.

---

### Notificação

Guarda:

* mensagem enviada;
* horário;
* status.

---

# 4. ARQUITETURA DE AUTOMAÇÃO E INTEGRAÇÕES

## Objetivo

Fazer o sistema trabalhar automaticamente sem intervenção humana.

---

## Motor de automação:

Tecnologias:

* Celery;
* Redis.

---

Funcionamento:

O sistema verifica consultas futuras.

Exemplo:

Consulta:

20/07 às 14h

Configuração:

Enviar 24 horas antes.

---

O sistema cria uma tarefa:

Enviar mensagem:

19/07 às 14h.

---

## Integração WhatsApp:

Tecnologia:

Evolution API.

---

Fluxo:

```
Django

↓

Evolution API

↓

WhatsApp da empresa

↓

Paciente
```

---

Responsabilidades:

* conectar WhatsApp;
* enviar mensagens;
* receber confirmações.

---

Conexão:

Empresa entra no SaaS.

Clica:

"Conectar WhatsApp".

Escaneia QR Code.

WhatsApp fica conectado.

---

# 5. ARQUITETURA DE INFRAESTRUTURA, SEGURANÇA E ESCALABILIDADE

## Objetivo

Definir onde a plataforma será hospedada, como os serviços serão organizados, quais mecanismos garantirão a segurança dos dados e como a infraestrutura evoluirá conforme o crescimento da base de clientes.

---

## Infraestrutura Inicial (MVP)

A plataforma será hospedada inicialmente em uma única VPS fornecida pela Hetzner Cloud.

Esta VPS será responsável por executar todos os componentes principais do sistema:

* Django
* PostgreSQL
* Redis
* Celery
* Evolution API

A centralização da infraestrutura reduz custos, simplifica a administração do ambiente e acelera o desenvolvimento do MVP.

---

## Escalabilidade

A infraestrutura foi projetada para crescer de forma gradual, sem necessidade de alterar a arquitetura da aplicação.

---

## Segurança

A plataforma adotará mecanismos de segurança em todas as camadas da aplicação.

Principais implementações:

* autenticação de usuários;
* controle de permissões por empresa;
* isolamento de dados entre clientes (Multi-Tenant);
* comunicação criptografada utilizando HTTPS (SSL);
* backups automáticos do banco de dados;
* proteção das conexões com o WhatsApp utilizando proxies dedicados para cada empresa.

---

## Resumo da Arquitetura

| Área                | Decisão                                                                               |
| ------------------- | ------------------------------------------------------------------------------------- |
| Hospedagem          | Hetzner Cloud                                                                         |
| Arquitetura Inicial | VPS única para o MVP                                                                  |
| Escalabilidade      | Separação gradual dos serviços conforme o crescimento                                 |
| Segurança           | HTTPS, autenticação, isolamento Multi-Tenant, backups automáticos e proxies dedicados |

# DOCUMENTO DE AUDITORIA, PERFIL DO SUPER ADMIN E CENTRAL DE NOTIFICAÇÕES

## Projeto

**Agendap — Micro-SaaS de Confirmação Automatizada de Agendamentos via WhatsApp**

---

# Objetivo

Este documento define os recursos responsáveis pela rastreabilidade das ações administrativas, gerenciamento da conta do Super Admin e funcionamento da Central de Notificações do Dashboard Administrativo.

Seu objetivo é garantir segurança, transparência, rastreabilidade e acompanhamento das principais ocorrências da plataforma.

Este documento integra a especificação oficial do Dashboard Administrativo do Agendap.

---

# DAP-001 — Auditoria da Plataforma

## Objetivo

Registrar todas as ações administrativas realizadas dentro do Dashboard.

Toda ação relevante executada por qualquer administrador deverá ser armazenada automaticamente.

Nenhuma ação administrativa poderá ocorrer sem registro na Auditoria.

---

# DAP-002 — Eventos Auditáveis

Serão registrados automaticamente eventos como:

* login;
* logout;
* alteração de senha;
* alteração de e-mail;
* criação de administradores;
* remoção de administradores;
* alteração de permissões;
* criação de empresas;
* suspensão de empresas;
* reativação de empresas;
* exclusão de empresas;
* alteração de planos;
* redefinição do período de teste;
* alterações nas configurações globais;
* alterações de planos comerciais;
* utilização do recurso "Entrar como Empresa";
* alterações relacionadas ao Dashboard Administrativo.

---

# DAP-003 — Informações Registradas

Cada evento armazenará obrigatoriamente:

* data;
* horário;
* administrador responsável;
* tipo da ação;
* empresa afetada (quando aplicável);
* endereço IP;
* resultado da operação.

---

# DAP-004 — Consulta da Auditoria

O Dashboard permitirá pesquisar registros utilizando filtros.

Filtros disponíveis:

* período;
* administrador;
* CPF;
* CNPJ;
* e-mail;
* tipo de ação.

O objetivo será facilitar investigações e suporte.

---

# DAP-005 — Integridade da Auditoria

Os registros da Auditoria serão permanentes durante o período de retenção definido pela plataforma.

Nenhum administrador poderá editar registros.

Nenhum administrador poderá excluir registros manualmente.

A remoção ocorrerá exclusivamente conforme a política oficial de retenção da plataforma.

---

# DAP-006 — Ações Suspeitas

O sistema identificará automaticamente eventos considerados incomuns.

Exemplos:

* excesso de tentativas de login;
* múltiplas alterações administrativas em curto período;
* diversos convites administrativos gerados;
* sucessivas suspensões de empresas.

Esses eventos serão apresentados apenas como alertas administrativos.

---

# DAP-007 — Perfil do Super Admin

## Objetivo

Permitir gerenciamento completo da conta do proprietário da plataforma.

Será possível alterar:

* nome;
* foto de perfil (opcional);
* e-mail;
* senha.

Todas as alterações serão registradas automaticamente na Auditoria.

---

# DAP-008 — Segurança da Conta

O Super Admin poderá configurar:

* autenticação em dois fatores (2FA);
* alteração de senha;
* gerenciamento das sessões ativas.

O sistema deverá invalidar automaticamente sessões comprometidas ou encerradas manualmente.

---

# DAP-009 — Sessões Ativas

O Dashboard exibirá todas as sessões abertas da conta administrativa.

Cada sessão apresentará:

* navegador;
* sistema operacional;
* endereço IP;
* data;
* horário;
* localização aproximada (quando disponível).

Será possível encerrar individualmente qualquer sessão ativa, exceto a sessão atualmente utilizada.

---

# DAP-010 — Recuperação da Conta

Caso necessário, o Super Admin poderá recuperar o acesso através do fluxo oficial de recuperação.

Fluxo:

Solicitação de recuperação.

↓

Envio de e-mail.

↓

Token exclusivo.

↓

Definição da nova senha.

↓

Invalidação automática do token utilizado.

---

# DAP-011 — Central de Notificações

## Objetivo

Centralizar todos os eventos relevantes da plataforma.

O Dashboard exibirá um ícone de notificações na barra superior.

Sempre que existirem notificações pendentes, será apresentada uma indicação visual em vermelho juntamente com a quantidade de notificações não lidas.

---

# DAP-012 — Organização das Notificações

A Central de Notificações será organizada por categorias.

Categorias disponíveis:

* Todas;
* Financeiro;
* Empresas;
* Segurança;
* Sistema;
* Infraestrutura;
* Administradores.

O administrador poderá alternar entre as categorias utilizando abas específicas.

---

# DAP-013 — Notificações Financeiras

Exemplos:

* nova assinatura;
* pagamento confirmado;
* pagamento recusado;
* empresa inadimplente;
* empresa reativada.

Essas notificações serão visíveis apenas para usuários autorizados.

---

# DAP-014 — Notificações das Empresas

Exemplos:

* nova empresa cadastrada;
* empresa suspensa;
* empresa excluída;
* empresa convertida para plano pago;
* término do período de teste.

---

# DAP-015 — Notificações de Segurança

Exemplos:

* tentativas excessivas de login;
* alteração de senha;
* alteração de permissões;
* login em novo dispositivo;
* criação de administrador.

---

# DAP-016 — Notificações do Sistema

Exemplos:

* atualização da plataforma;
* erro crítico;
* falhas internas;
* recuperação automática de serviços.

---

# DAP-017 — Notificações de Infraestrutura

Exemplos:

* PostgreSQL indisponível;
* Redis indisponível;
* Celery interrompido;
* Evolution API desconectada;
* falha de backup.

---

# DAP-018 — Notificações dos Administradores

Exemplos:

* convite aceito;
* convite expirado;
* administrador removido;
* permissões alteradas.

---

# DAP-019 — Gerenciamento das Notificações

Cada notificação poderá ser:

* marcada como lida;
* marcada como não lida.

O histórico permanecerá disponível conforme a política de retenção da plataforma.

Nenhuma notificação poderá ser editada manualmente.

---

# DAP-020 — Princípios Gerais

Todos os recursos descritos neste documento deverão seguir obrigatoriamente os seguintes princípios:

* rastreabilidade completa;
* segurança máxima;
* transparência operacional;
* integridade dos registros;
* consistência com a arquitetura oficial do Agendap;
* validação obrigatória pelo Backend;
* registro automático das ações administrativas.

---

# Resumo da Arquitetura

O módulo de Auditoria, Perfil do Super Admin e Central de Notificações constitui a camada responsável pela governança operacional do Dashboard Administrativo.

Através dele, será possível rastrear todas as ações relevantes da plataforma, administrar com segurança a conta do Super Admin e acompanhar em tempo real os principais eventos administrativos, financeiros, técnicos e operacionais do Agendap.

Todos os registros serão protegidos contra alterações manuais, garantindo integridade, segurança e rastreabilidade durante toda a operação da plataforma.

Este documento, juntamente com os demais documentos do Dashboard Administrativo, constitui a especificação oficial do painel administrativo da plataforma Agendap.

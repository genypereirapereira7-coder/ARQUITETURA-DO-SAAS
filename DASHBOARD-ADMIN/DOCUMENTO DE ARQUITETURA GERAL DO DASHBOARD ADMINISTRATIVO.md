# DOCUMENTO DE ARQUITETURA GERAL DO DASHBOARD ADMINISTRATIVO

## Projeto

**Agendap — Micro-SaaS de Confirmação Automatizada de Agendamentos via WhatsApp**

---

# Objetivo

Este documento define toda a arquitetura geral do Dashboard Administrativo da plataforma Agendap.

O Dashboard Administrativo será o ambiente exclusivo de administração da plataforma, destinado ao gerenciamento operacional, comercial e técnico do SaaS.

Este painel não faz parte do sistema utilizado pelos clientes da Agendap.

Seu objetivo é permitir que os administradores da plataforma realizem a gestão completa do negócio com segurança, rastreabilidade e controle total sobre todas as empresas cadastradas.

Este documento faz parte da arquitetura oficial do projeto e deverá ser utilizado como especificação obrigatória durante todo o desenvolvimento do Dashboard Administrativo.

---

# DA-001 — Objetivo do Dashboard Administrativo

O Dashboard Administrativo será responsável por centralizar todas as operações internas da Agendap.

Seu objetivo é permitir que os administradores autorizados acompanhem a operação da plataforma, gerenciem empresas, administradores, planos, configurações, monitoramento e auditoria, mantendo controle completo sobre o SaaS.

O Dashboard Administrativo nunca será disponibilizado aos clientes da plataforma.

Seu acesso será exclusivo da equipe interna da Agendap.

---

# DA-002 — Arquitetura Geral

O Dashboard Administrativo será uma aplicação integrada ao backend principal do Agendap.

Não haverá um sistema separado.

Toda a comunicação ocorrerá utilizando a mesma arquitetura do backend oficial da plataforma, respeitando todas as regras de segurança, autenticação e autorização definidas na arquitetura do sistema.

O Dashboard possuirá autenticação própria, independente da autenticação utilizada pelas empresas clientes.

---

# DA-003 — Estrutura Geral do Dashboard

O Dashboard será organizado em módulos independentes.

Cada módulo possuirá responsabilidade específica.

Estrutura prevista:

* Dashboard Principal
* Empresas
* Administradores
* Configurações
* Monitoramento
* Auditoria
* Notificações
* Perfil do Super Admin

Cada módulo será isolado internamente, facilitando manutenção e evolução futura.

---

# DA-004 — Níveis de Administração

O Dashboard possuirá dois níveis administrativos.

## Super Admin

Representa o proprietário da plataforma.

Possui acesso irrestrito a todos os módulos do Dashboard.

Pode criar administradores.

Pode alterar permissões.

Pode acessar empresas.

Pode alterar planos.

Pode alterar configurações globais.

Pode administrar toda a plataforma.

O Super Admin é considerado a autoridade máxima do sistema.

---

## Administrador

Representa um funcionário autorizado pelo Super Admin.

Seu acesso será limitado pelas permissões atribuídas durante sua criação.

Nenhuma permissão será concedida automaticamente.

Todo acesso será controlado pelo Super Admin.

---

# DA-005 — Sistema de Permissões

Cada Administrador possuirá um conjunto individual de permissões.

As permissões serão definidas exclusivamente pelo Super Admin.

Exemplos de permissões:

* visualizar empresas;
* editar empresas;
* suspender empresas;
* alterar planos;
* acessar empresas;
* visualizar auditoria;
* visualizar monitoramento;
* alterar configurações;
* criar administradores;
* remover administradores.

O sistema deverá verificar todas as permissões antes da execução de qualquer operação.

Nenhuma permissão será validada apenas pelo Frontend.

Toda autorização ocorrerá obrigatoriamente no Backend.

---

# DA-006 — Sistema de Convites

Novos Administradores não poderão criar contas livremente.

O processo seguirá obrigatoriamente o seguinte fluxo:

O Super Admin cria um convite.

Seleciona todas as permissões.

O sistema gera automaticamente um código único.

Esse código possuirá validade de 24 horas.

Após esse período será automaticamente invalidado.

O Super Admin enviará ao funcionário:

* link do Dashboard Administrativo;
* código de acesso.

Nenhuma outra forma de cadastro será permitida.

---

# DA-007 — Primeiro Acesso do Administrador

Ao acessar o Dashboard Administrativo pela primeira vez, o Administrador realizará:

* login utilizando e-mail e senha;
* validação do código de convite;
* criação definitiva da conta administrativa.

Após validação bem-sucedida, o código será automaticamente inutilizado.

Nenhum código poderá ser reutilizado.

---

# DA-008 — Login Administrativo

O Dashboard Administrativo possuirá autenticação exclusiva.

O login será realizado utilizando:

* e-mail;
* senha.

O sistema poderá utilizar autenticação em dois fatores (2FA), conforme configuração da conta do administrador.

A autenticação administrativa será totalmente independente da autenticação utilizada pelas empresas clientes.

---

# DA-009 — Segurança do Dashboard

O Dashboard Administrativo será protegido por múltiplas camadas de segurança.

Entre elas:

* autenticação obrigatória;
* autorização baseada em permissões;
* sessões seguras;
* proteção contra força bruta;
* proteção CSRF;
* HTTPS obrigatório;
* cookies seguros;
* isolamento completo entre administradores e empresas.

Nenhuma operação administrativa poderá ser executada sem autenticação válida.

---

# DA-010 — Acesso às Empresas

O Super Admin poderá acessar temporariamente qualquer empresa cadastrada.

Esse acesso terá como objetivo:

* suporte técnico;
* investigação de problemas;
* validação operacional.

Esse recurso será chamado "Entrar como Empresa".

Todo acesso será obrigatoriamente registrado na Auditoria.

O Administrador somente poderá utilizar essa funcionalidade caso receba permissão explícita do Super Admin.

---

# DA-011 — Pesquisa de Empresas

O Dashboard permitirá localizar empresas utilizando exclusivamente:

* CPF;
* CNPJ;
* e-mail.

Não será permitida pesquisa por nome da empresa.

Não será permitida pesquisa por pacientes.

Não será permitida pesquisa por profissionais.

Todo acesso será realizado diretamente sobre a empresa cliente.

---

# DA-012 — Princípios do Dashboard Administrativo

Toda evolução do Dashboard seguirá obrigatoriamente os seguintes princípios:

* simplicidade operacional;
* segurança máxima;
* rastreabilidade completa;
* separação de responsabilidades;
* controle centralizado pelo Super Admin;
* autorização obrigatória no Backend;
* facilidade de manutenção;
* escalabilidade futura;
* consistência com toda a arquitetura oficial da plataforma.

---

# Resumo da Arquitetura

O Dashboard Administrativo constitui o ambiente exclusivo de administração da plataforma Agendap.

Seu funcionamento será baseado em autenticação própria, múltiplos níveis administrativos, controle granular de permissões, sistema seguro de convites, auditoria completa e acesso controlado às empresas cadastradas.

Toda funcionalidade administrativa deverá respeitar integralmente as regras estabelecidas neste documento e nos demais documentos oficiais da arquitetura do projeto.

Este documento, juntamente com os demais documentos do Dashboard Administrativo, constitui a especificação oficial do painel administrativo da plataforma Agendap.


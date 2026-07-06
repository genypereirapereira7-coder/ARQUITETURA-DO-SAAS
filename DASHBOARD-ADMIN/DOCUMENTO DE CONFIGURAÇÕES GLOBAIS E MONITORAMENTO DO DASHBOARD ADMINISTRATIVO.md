# DOCUMENTO DE CONFIGURAÇÕES GLOBAIS E MONITORAMENTO DO DASHBOARD ADMINISTRATIVO

## Projeto

**Agendap — Micro-SaaS de Confirmação Automatizada de Agendamentos via WhatsApp**

---

# Objetivo

Este documento define todas as configurações globais e os recursos de monitoramento da plataforma Agendap.

Seu objetivo é permitir que o Super Admin administre o funcionamento geral da plataforma através do Dashboard Administrativo, sem necessidade de alterações diretas no código sempre que possível.

Também define todos os recursos responsáveis por acompanhar a saúde operacional do sistema.

Este documento faz parte da especificação oficial do Dashboard Administrativo.

---

# DGM-001 — Configurações Gerais da Plataforma

## Objetivo

Permitir que o Super Admin configure informações institucionais da plataforma.

Será possível alterar:

* Nome da plataforma;
* Logo oficial;
* Favicon;
* Idioma padrão;
* Fuso horário;
* Mensagem de manutenção;
* Ativar ou desativar o modo de manutenção.

Todas as alterações deverão ser registradas automaticamente na Auditoria.

---

# DGM-002 — Configurações Comerciais

## Objetivo

Permitir administração das regras comerciais da plataforma.

Será possível configurar:

* quantidade de dias do período de teste;
* ativar ou desativar período de teste;
* política de cancelamento;
* política de reembolso;
* valor mínimo permitido para planos;
* valor máximo permitido para planos.

Todas as alterações deverão ser registradas na Auditoria.

---

# DGM-003 — Gerenciamento dos Planos

## Objetivo

Permitir administração completa dos planos comerciais.

Cada plano poderá possuir:

* nome;
* valor;
* percentual de desconto;
* ordem de exibição;
* cor utilizada na interface;
* badge (Ex.: Mais Vendido);
* benefícios;
* status (Ativo/Inativo).

As alterações realizadas refletirão automaticamente na plataforma.

---

# DGM-004 — Vídeo de Configuração Inicial

## Objetivo

Permitir que o Super Admin altere o vídeo enviado aos novos clientes.

O Dashboard disponibilizará apenas um campo:

Link do vídeo oficial hospedado no YouTube.

Fluxo:

Novo cliente cria conta.

↓

Recebe o e-mail de boas-vindas.

↓

O e-mail contém o link oficial do vídeo de configuração.

↓

O cliente aprende a utilizar a plataforma.

Nenhum outro vídeo será administrado pelo Dashboard.

---

# DGM-005 — Configurações de Segurança

## Objetivo

Centralizar as principais configurações de segurança da plataforma.

Será possível configurar:

* obrigatoriedade de autenticação em dois fatores (2FA);
* tempo máximo de sessão;
* tempo máximo de inatividade;
* quantidade máxima de tentativas de login;
* política mínima de senha;
* regras de complexidade de senha.

Toda alteração deverá ser registrada na Auditoria.

---

# DGM-006 — Informações da Versão

## Objetivo

Permitir consulta da versão atualmente instalada.

O Dashboard exibirá:

* versão atual da plataforma;
* data da última atualização;
* histórico de versões instaladas.

O Dashboard não realizará atualizações da aplicação.

Todo processo de atualização continuará sendo realizado através do processo oficial de deploy.

---

# DGM-007 — Monitoramento Geral

## Objetivo

Permitir que os administradores acompanhem a saúde operacional da plataforma.

Todas as informações deverão ser exibidas em tempo real.

Nenhuma informação desta tela será editável.

---

# DGM-008 — Monitoramento do Servidor

O Dashboard exibirá:

* status do servidor;
* utilização da CPU;
* utilização da memória RAM;
* utilização do disco;
* tempo de funcionamento (Uptime).

Essas informações terão caráter exclusivamente informativo.

---

# DGM-009 — Monitoramento do Banco de Dados

O Dashboard exibirá informações do PostgreSQL.

Serão apresentadas:

* status do banco;
* tempo médio de resposta;
* quantidade de conexões;
* último backup realizado.

---

# DGM-010 — Monitoramento do Redis

O Dashboard exibirá:

* status;
* memória utilizada;
* quantidade de chaves;
* tempo de resposta.

---

# DGM-011 — Monitoramento do Celery

O Dashboard exibirá:

* status dos Workers;
* quantidade de Workers ativos;
* Workers indisponíveis;
* tarefas em execução;
* tarefas concluídas;
* tarefas com erro;
* tempo médio de execução.

Essas informações permitirão identificar problemas relacionados às automações da plataforma.

---

# DGM-012 — Monitoramento da Evolution API

O Dashboard exibirá:

* status da Evolution API;
* tempo médio de resposta;
* versão instalada;
* quantidade de instâncias;
* instâncias conectadas;
* instâncias desconectadas;
* mensagens enviadas;
* mensagens com erro.

---

# DGM-013 — Monitoramento dos Backups

O Dashboard exibirá:

* último backup realizado;
* próximo backup programado;
* status do backup.

O Dashboard não permitirá restaurar nem baixar backups.

Esses procedimentos continuarão sendo realizados diretamente na infraestrutura do servidor.

---

# DGM-014 — Testes dos Serviços

O Dashboard permitirá executar testes rápidos dos principais serviços da plataforma.

Será possível testar:

* Servidor;
* PostgreSQL;
* Redis;
* Celery;
* Evolution API;
* Sistema de Backup.

Após cada teste, o sistema informará:

* Sucesso;
* Falha.

Esses testes não executarão operações críticas.

Seu objetivo será apenas validar disponibilidade dos serviços.

---

# DGM-015 — Histórico de Incidentes

## Objetivo

Apresentar os principais eventos relacionados à estabilidade da plataforma.

Exemplos:

* indisponibilidade do PostgreSQL;
* falha da Evolution API;
* interrupção do Celery;
* falha de Backup;
* recuperação automática dos serviços.

O histórico permitirá rápida identificação de problemas recentes.

---

# DGM-016 — Princípios das Configurações Globais

Toda configuração disponível no Dashboard deverá seguir obrigatoriamente os seguintes princípios:

* simplicidade operacional;
* segurança;
* rastreabilidade;
* facilidade de manutenção;
* alterações registradas na Auditoria;
* validação obrigatória pelo Backend;
* consistência com a arquitetura oficial da plataforma.

---

# DGM-017 — Princípios do Monitoramento

O sistema de monitoramento seguirá obrigatoriamente os seguintes princípios:

* somente leitura;
* atualização automática;
* informações em tempo real;
* nenhuma alteração direta na infraestrutura através do Dashboard;
* identificação rápida de falhas;
* apoio ao diagnóstico operacional.

---

# Resumo da Arquitetura

O módulo de Configurações Globais e Monitoramento constitui o centro administrativo responsável pela configuração da plataforma e pelo acompanhamento contínuo da saúde operacional do Agendap.

Através dele, o Super Admin poderá administrar parâmetros globais do SaaS, acompanhar os principais serviços da infraestrutura, validar a disponibilidade dos componentes críticos e identificar rapidamente qualquer instabilidade operacional.

Nenhuma funcionalidade deste módulo permitirá alterações diretas na infraestrutura da plataforma, preservando a segurança e a estabilidade do ambiente de produção.

Este documento, juntamente com os demais documentos do Dashboard Administrativo, constitui parte da especificação oficial do painel administrativo da plataforma Agendap.

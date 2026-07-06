# DOCUMENTO DE GESTÃO OPERACIONAL DO DASHBOARD ADMINISTRATIVO

## Projeto

**Agendap — Micro-SaaS de Confirmação Automatizada de Agendamentos via WhatsApp**

---

# Objetivo

Este documento define toda a estrutura operacional do Dashboard Administrativo da plataforma Agendap.

Seu objetivo é estabelecer como o Super Admin e os Administradores autorizados irão gerenciar as empresas, acompanhar indicadores, executar ações administrativas e operar o SaaS no dia a dia.

Este documento complementa a Arquitetura Geral do Dashboard Administrativo e faz parte da especificação oficial da plataforma.

---

# DO-001 — Dashboard Principal

## Objetivo

O Dashboard Principal será a tela inicial apresentada imediatamente após o login do administrador.

Seu objetivo será fornecer uma visão geral da situação operacional e comercial da plataforma.

Todas as informações deverão ser atualizadas automaticamente.

---

# DO-002 — Cards Principais

O Dashboard exibirá os principais indicadores da plataforma.

Entre eles:

* Empresas Ativas;
* Empresas em Período de Teste;
* Empresas Inadimplentes;
* Empresas Suspensas;
* Empresas Canceladas;
* Assinaturas Ativas;
* Novas Empresas no mês;
* Total de Administradores.

Todos os indicadores deverão representar dados em tempo real.

---

# DO-003 — Indicadores Financeiros

O Dashboard exibirá indicadores financeiros exclusivamente para o Super Admin.

Serão apresentados:

* Receita Mensal;
* Receita Anual;
* Receita Recorrente (MRR);
* Receita Total;
* Empresas Pagantes.

Administradores comuns nunca poderão visualizar informações financeiras.

Toda validação ocorrerá obrigatoriamente no Backend.

---

# DO-004 — Gráficos

O Dashboard apresentará gráficos para facilitar a análise do crescimento da plataforma.

Entre eles:

* Evolução das empresas cadastradas;
* Evolução das assinaturas;
* Crescimento da receita;
* Empresas em teste versus empresas pagantes.

Todos os gráficos deverão permitir filtros por período.

---

# DO-005 — Alertas

O Dashboard exibirá automaticamente alertas importantes.

Exemplos:

* empresas inadimplentes;
* empresas próximas ao fim do período de teste;
* pagamentos recusados;
* falhas críticas do sistema;
* serviços indisponíveis.

Os alertas deverão permanecer visíveis até serem resolvidos.

---

# DO-006 — Ações Rápidas

O Dashboard disponibilizará atalhos para operações frequentemente utilizadas.

Entre elas:

* pesquisar empresa;
* criar administrador;
* acessar monitoramento;
* acessar auditoria;
* acessar configurações.

O objetivo é reduzir o número de cliques necessários para operações administrativas.

---

# DO-007 — Gerenciamento de Empresas

O Dashboard permitirá administração completa das empresas cadastradas.

Cada empresa apresentará:

* Nome;
* CPF ou CNPJ;
* E-mail;
* Plano contratado;
* Status;
* Data de cadastro;
* Situação financeira.

---

# DO-008 — Pesquisa de Empresas

A pesquisa será realizada exclusivamente por:

* CPF;
* CNPJ;
* E-mail.

Não será permitido pesquisar:

* pacientes;
* profissionais;
* consultas;
* nome da empresa.

Após localizar a empresa, o administrador poderá visualizar todas as informações administrativas relacionadas a ela.

---

# DO-009 — Ações Disponíveis sobre Empresas

Dependendo das permissões atribuídas, será possível:

* visualizar empresa;
* editar informações;
* suspender empresa;
* reativar empresa;
* excluir empresa;
* alterar plano;
* redefinir período de teste (quando autorizado);
* acessar a empresa utilizando o recurso "Entrar como Empresa".

Todas as operações deverão ser registradas na Auditoria.

---

# DO-010 — Entrar como Empresa

O recurso "Entrar como Empresa" permitirá que administradores autorizados acessem temporariamente o ambiente administrativo de uma empresa.

Objetivos:

* suporte técnico;
* investigação de problemas;
* validação operacional.

Esse recurso nunca permitirá acesso ao ambiente de pacientes.

Todo acesso será registrado automaticamente na Auditoria.

Somente o Super Admin poderá utilizar esta funcionalidade por padrão.

Administradores comuns dependerão de permissão específica concedida pelo Super Admin.

---

# DO-011 — Gerenciamento de Administradores

O Dashboard permitirá administrar todos os usuários administrativos da plataforma.

Será possível:

* visualizar administradores;
* criar administradores;
* editar permissões;
* bloquear acesso;
* remover administradores;
* visualizar último acesso;
* visualizar status da conta.

---

# DO-012 — Convites Administrativos

Novos administradores serão criados através do sistema oficial de convites.

Fluxo:

O Super Admin cria o convite.

Seleciona as permissões.

O sistema gera automaticamente um código único.

Esse código possuirá validade de 24 horas.

O Super Admin enviará:

* link do Dashboard Administrativo;
* código de acesso.

Após utilização, o código será automaticamente invalidado.

Nenhum código poderá ser reutilizado.

---

# DO-013 — Permissões Administrativas

Cada administrador possuirá permissões independentes.

O Super Admin poderá habilitar ou remover individualmente cada permissão.

Exemplos:

* visualizar empresas;
* editar empresas;
* suspender empresas;
* excluir empresas;
* alterar planos;
* criar administradores;
* remover administradores;
* acessar auditoria;
* acessar monitoramento;
* acessar configurações;
* utilizar "Entrar como Empresa".

Nenhuma permissão será concedida automaticamente.

---

# DO-014 — Controle de Acesso

O sistema verificará todas as permissões antes da execução de qualquer ação.

Caso o administrador não possua autorização suficiente, a operação será imediatamente bloqueada.

Toda validação ocorrerá obrigatoriamente no Backend.

---

# DO-015 — Princípios Operacionais

Toda gestão operacional do Dashboard deverá seguir os seguintes princípios:

* simplicidade;
* rapidez;
* rastreabilidade;
* segurança;
* validação obrigatória no Backend;
* registro completo das operações;
* facilidade de manutenção;
* escalabilidade.

---

# Resumo da Arquitetura

O Dashboard Operacional constitui o principal ambiente de administração da plataforma Agendap.

Através dele será possível acompanhar indicadores, gerenciar empresas, administrar usuários internos, controlar permissões, alterar planos, prestar suporte técnico e executar todas as operações administrativas necessárias para o funcionamento do SaaS.

Todas as ações administrativas deverão respeitar integralmente as regras estabelecidas neste documento e permanecer registradas na Auditoria da plataforma.

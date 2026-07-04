DOCUMENTO DE ARQUITETURA DE SEGURANÇA
Projeto

Micro-SaaS de Confirmação Automatizada de Agendamentos via WhatsApp

Objetivo

Definir toda a arquitetura de segurança do SaaS, estabelecendo as camadas de proteção responsáveis por garantir a confidencialidade, integridade, disponibilidade e isolamento dos dados das empresas, protegendo a plataforma contra acessos não autorizados, ataques, vazamentos de informações e falhas operacionais.

A segurança deverá ser aplicada em todas as camadas do sistema, desde a infraestrutura até a comunicação entre serviços externos.

1. ARQUITETURA DE SEGURANÇA

A segurança do sistema será baseada em múltiplas camadas independentes.

Caso uma camada falhe, as demais continuarão protegendo o sistema.

Camadas:

Segurança da Infraestrutura.
Segurança da Aplicação.
Segurança das APIs.
Segurança Multi-Tenant.
Segurança do Banco de Dados.
Segurança das Sessões.
Controle de Acesso.
Segurança da Integração WhatsApp.
Segurança Financeira.
Auditoria.
Proteção contra Ataques.
Proteção de Uploads.
Segurança dos Webhooks.
Conformidade com LGPD.
2. SEGURANÇA DA INFRAESTRUTURA

Toda a infraestrutura deverá operar utilizando comunicação criptografada.

Ferramentas:

HTTPS (Let's Encrypt).
Firewall UFW.
Fail2Ban.
SSH utilizando chaves criptográficas.
Atualizações periódicas de segurança do sistema operacional.

Não será permitido acesso administrativo utilizando login e senha simples no servidor.

Todo acesso administrativo deverá ocorrer exclusivamente através de autenticação por chave SSH.

3. SEGURANÇA DA APLICAÇÃO

O Backend será desenvolvido utilizando Django.

Serão utilizadas todas as proteções nativas oferecidas pelo framework.

Proteções obrigatórias:

Proteção CSRF.
Proteção contra SQL Injection utilizando ORM.
Proteção contra Cross Site Scripting (XSS).
Validação automática de formulários.
Validação automática dos Serializers.
Sanitização das entradas.
Escape automático de conteúdo HTML.

Nenhuma informação enviada pelo usuário será considerada confiável.

Toda informação deverá ser validada novamente no Backend.

4. SEGURANÇA DAS APIs

Todas as APIs seguirão um padrão único.

Características:

Comunicação exclusivamente via HTTPS.
Dados transmitidos utilizando JSON.
Versionamento das APIs.
Autenticação obrigatória.
Controle de permissões.
Validação completa das requisições.
Registro de logs.

Todas as APIs privadas exigirão autenticação válida.

Nenhuma API administrativa poderá ser acessada publicamente.

5. AUTENTICAÇÃO

Métodos permitidos:

Login utilizando e-mail e senha.
Login utilizando conta Google (OAuth).

Após autenticação bem-sucedida, será emitido um token de acesso.

Esse token será utilizado automaticamente durante a navegação da plataforma.

6. SESSÕES

Após o login, a sessão permanecerá ativa enquanto houver utilização frequente da plataforma.

Caso o usuário permaneça aproximadamente 30 dias sem acessar o sistema, será necessário realizar um novo login.

As sessões utilizarão:

Cookies HttpOnly.
Cookies Secure.
SameSite.
Comunicação exclusivamente via HTTPS.
7. CONTROLE DE ACESSO (RBAC)

O sistema utilizará Controle de Acesso Baseado em Funções (Role-Based Access Control).

Perfis:

Administrador

Permissões:

Controle total da empresa.
Gerenciamento de usuários.
Configurações.
Consultas.
Profissionais.
WhatsApp.
Assinatura.

Secretária

Permissões:

Cadastro de consultas.
Alteração de consultas.
Cadastro de pacientes.
Cadastro de profissionais.
Consulta ao Dashboard.

Paciente

Permissões:

Confirmar consulta.
Cancelar consulta.
Solicitar reagendamento.
Consultar status da consulta através do link recebido.

Todas as permissões serão verificadas no Backend.

8. SEGURANÇA MULTI-TENANT

Cada empresa possuirá isolamento completo de seus dados.

O Front-end nunca enviará o identificador da empresa.

O Backend identificará automaticamente a empresa autenticada.

Nenhuma empresa poderá visualizar informações pertencentes a outra empresa.

Esse isolamento será obrigatório em todas as consultas realizadas ao banco de dados.

9. SEGURANÇA DO BANCO DE DADOS

O banco de dados utilizará PostgreSQL.

Práticas obrigatórias:

ORM do Django.
Validação dos dados.
Controle de permissões.
Backup periódico.
Integridade referencial.
Criptografia das senhas utilizando algoritmos seguros do Django (Argon2 ou PBKDF2).

Nenhuma senha será armazenada em texto simples.

10. SEGURANÇA DA INTEGRAÇÃO WHATSAPP

A comunicação com o WhatsApp ocorrerá exclusivamente através da Evolution API.

Fluxo:

Front-end

↓

Backend

↓

Evolution API

↓

WhatsApp

O Front-end nunca acessará diretamente a Evolution API.

Cada empresa utilizará sua própria instância do WhatsApp.

Cada empresa utilizará um Proxy dedicado através do Proxy-Cheap.

Isso reduz o risco de impacto entre clientes e melhora o isolamento operacional.

O sistema monitorará continuamente o estado da conexão do WhatsApp.

Caso ocorra desconexão:

alerta visual no Dashboard;
registro em log;
suspensão temporária dos envios até a reconexão.
11. SEGURANÇA FINANCEIRA

Todo o processamento financeiro será realizado pelo Asaas.

O SaaS nunca armazenará:

números de cartão;
CVV;
dados bancários sensíveis.

O sistema armazenará apenas informações necessárias para gerenciamento da assinatura.

Toda atualização financeira será recebida através de Webhooks autenticados.

12. SEGURANÇA DOS WEBHOOKS

Todos os Webhooks recebidos deverão validar obrigatoriamente:

autenticidade da origem;
assinatura digital (quando fornecida);
formato da requisição;
integridade dos dados recebidos.

Nenhum Webhook será processado sem validação prévia.

13. PROTEÇÃO CONTRA ATAQUES

O sistema implementará:

Rate Limiting.
Bloqueio temporário após múltiplas tentativas de login.
Proteção contra força bruta.
Proteção contra enumeração de usuários.
Limitação do tamanho das requisições.
Validação de uploads.
Validação de conteúdo recebido pelas APIs.
14. SEGURANÇA DOS UPLOADS

Os uploads serão restritos aos recursos autorizados, como o logotipo da empresa.

Arquivos permitidos:

PNG.
JPG.
WEBP.

Todos os arquivos deverão ser validados quanto ao tipo e ao tamanho antes do armazenamento.

Arquivos inválidos serão rejeitados automaticamente.

15. AUDITORIA E LOGS

Todas as ações críticas deverão gerar registros de auditoria.

Eventos registrados:

Login.
Logout.
Alteração de senha.
Alteração de configurações.
Alteração do WhatsApp.
Alteração de consultas.
Cancelamentos.
Solicitações de reagendamento.
Alteração de usuários.
Alteração de administradores.
Alteração da assinatura.

Os registros permanecerão armazenados pelos últimos 30 dias.

16. BACKUP E RECUPERAÇÃO

O sistema realizará backups periódicos do banco de dados.

Objetivos:

recuperação em caso de falha;
recuperação em caso de erro operacional;
proteção contra perda de informações.

Os procedimentos de restauração deverão ser testados periodicamente.

17. CONFORMIDADE COM A LGPD

O sistema seguirá os princípios da Lei Geral de Proteção de Dados (LGPD).

Práticas adotadas:

coleta apenas dos dados necessários;
acesso restrito por empresa;
comunicação criptografada;
exclusão definitiva dos dados após o período de retenção;
histórico das operações administrativas;
isolamento completo das informações entre empresas.
18. MONITORAMENTO

O sistema deverá monitorar continuamente:

disponibilidade do servidor;
disponibilidade da Evolution API;
disponibilidade do PostgreSQL;
disponibilidade do Redis;
disponibilidade do sistema de filas;
status da conexão do WhatsApp.

Falhas críticas deverão gerar alertas internos para rápida identificação e correção.

Resumo da Arquitetura de Segurança
Área	Decisão
Comunicação	HTTPS obrigatório
Infraestrutura	UFW, Fail2Ban, SSH por chave
Aplicação	Django Security, CSRF, ORM, XSS, Sanitização
APIs	REST, JSON, Token, Versionamento
Sessão	Persistente com renovação após aproximadamente 30 dias de inatividade
Controle de Acesso	RBAC
Banco de Dados	PostgreSQL com senhas criptografadas
Multi-Tenant	Isolamento automático por empresa
WhatsApp	Evolution API + Proxy dedicado por empresa
Financeiro	Asaas
Webhooks	Validação obrigatória da origem
Uploads	PNG, JPG e WEBP validados
Proteção	Rate Limiting, Anti-Brute Force, Anti-Enumeração
Auditoria	Logs das ações críticas por 30 dias
Backup	Backups periódicos e plano de recuperação
LGPD	Coleta mínima, criptografia e isolamento dos dados
Monitoramento	Servidor, Banco, Redis, Evolution API e WhatsApp

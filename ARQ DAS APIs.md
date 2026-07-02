

# DOCUMENTO DE ARQUITETURA DAS APIs

## Projeto

**Micro-SaaS de Confirmação Automatizada de Agendamentos via WhatsApp**

---

# Objetivo

Definir a arquitetura das APIs responsáveis pela comunicação entre o Front-end, o Back-end, o Banco de Dados e as integrações externas.

Todas as funcionalidades do sistema deverão ser acessadas exclusivamente através das APIs.

Nenhum componente do Front-end poderá acessar diretamente o banco de dados ou serviços externos.

As APIs seguirão um padrão único de organização, segurança, autenticação, versionamento e resposta.

---

# 1. PADRÃO DA API

## Arquitetura

REST API

A comunicação entre Front-end e Back-end será realizada utilizando o padrão REST.

Todas as requisições utilizarão HTTPS.

Todos os dados serão transmitidos no formato JSON.

Exemplo de fluxo:

Front-end

↓

API REST

↓

Backend Django

↓

Banco de Dados

↓

Resposta JSON

---

# 2. TECNOLOGIAS

Backend

* Python
* Django
* Django REST Framework (DRF)

Comunicação

* HTTPS
* JSON

Documentação

* OpenAPI
* Swagger

---

# 3. VERSIONAMENTO

Todas as APIs serão versionadas desde a primeira versão do sistema.

Padrão:

/api/v1/

No futuro poderão existir:

/api/v2/

/api/v3/

Sem quebrar compatibilidade com versões anteriores.

---

# 4. AUTENTICAÇÃO

Toda requisição protegida exigirá autenticação.

Métodos suportados:

* Login com e-mail e senha
* Login utilizando conta Google (OAuth)

Após autenticação, o sistema emitirá um token de acesso.

Esse token será utilizado automaticamente nas próximas requisições.

---

# 5. SESSÃO

Após o login, a sessão permanecerá ativa enquanto houver utilização frequente do sistema.

Caso o usuário permaneça aproximadamente 30 dias sem acessar, será necessário realizar um novo login.

Essa renovação ocorrerá automaticamente conforme o uso contínuo da plataforma.

---

# 6. SEGURANÇA DAS APIs

Todas as APIs deverão implementar obrigatoriamente:

* HTTPS obrigatório.
* Autenticação por token.
* Controle de acesso baseado em funções (RBAC).
* Isolamento Multi-Tenant.
* Validação de todos os dados recebidos.
* Sanitização de entradas.
* Proteção contra SQL Injection.
* Proteção contra Cross Site Scripting (XSS).
* Rate Limiting contra abuso de requisições.
* Registro de logs das operações importantes.

---

# 7. ISOLAMENTO MULTI-TENANT

Todas as consultas realizadas pelas APIs deverão ser automaticamente filtradas pela empresa autenticada.

O Front-end nunca enviará manualmente o identificador da empresa.

O Backend identificará automaticamente a empresa através do usuário autenticado.

Isso garante isolamento completo entre empresas diferentes.

---

# 8. PADRÃO DAS RESPOSTAS

Todas as APIs deverão seguir um padrão único de resposta.

Sucesso:

200 OK

Criação:

201 Created

Requisição inválida:

400 Bad Request

Não autenticado:

401 Unauthorized

Sem permissão:

403 Forbidden

Não encontrado:

404 Not Found

Erro interno:

500 Internal Server Error

As mensagens deverão ser claras e padronizadas.

---

# 9. ORGANIZAÇÃO DAS APIs

As APIs serão divididas por módulos do sistema.

API001 — Autenticação

Responsável por:

* Login.
* Login Google.
* Logout.
* Recuperação de senha.
* Renovação da sessão.

---

API002 — Empresas

Responsável por:

* Buscar empresa.
* Atualizar nome.
* Atualizar telefone.
* Atualizar logotipo.
* Buscar plano.
* Atualizar informações gerais.

---

API003 — Usuários

Responsável por:

* Criar administrador.
* Criar secretária.
* Editar usuário.
* Alterar senha.
* Ativar usuário.
* Desativar usuário.
* Excluir usuário.
* Listar usuários.

---

API004 — Profissionais

Responsável por:

* Criar profissional.
* Editar profissional.
* Excluir profissional.
* Buscar profissional.
* Listar profissionais.

---

API005 — Pacientes

Responsável por:

* Criar paciente.
* Atualizar paciente.
* Buscar paciente.
* Buscar histórico.
* Buscar paciente por telefone.
* Listar pacientes.

O sistema deverá identificar automaticamente pacientes já cadastrados através do telefone.

---

API006 — Consultas

Responsável por:

* Criar consulta.
* Alterar consulta.
* Cancelar consulta.
* Buscar consulta.
* Buscar consultas do dia.
* Buscar consultas futuras.
* Buscar por período.
* Buscar por status.

Ao alterar uma consulta já agendada, os lembretes antigos deverão ser cancelados automaticamente e novos lembretes deverão ser programados.

---

API007 — Dashboard

Responsável por fornecer indicadores do sistema.

Informações:

* Consultas do dia.
* Próximas consultas.
* Consultas confirmadas.
* Consultas canceladas.
* Solicitações de reagendamento.
* Consultas pendentes.
* Alertas.
* Estatísticas gerais.

---

API008 — Configurações

Responsável pelas preferências da empresa.

Permitir:

* Alterar horário do primeiro lembrete.
* Alterar horário do segundo lembrete.
* Ativar ou desativar segundo lembrete.
* Editar mensagens.
* Restaurar mensagem padrão.
* Alterar nome da empresa.
* Alterar telefone.
* Alterar logotipo.
* Alterar WhatsApp.
* Gerenciar administradores.
* Gerenciar secretárias.
* Alterar preferências gerais.

---

API009 — WhatsApp

Responsável pela integração com a Evolution API.

Permitir:

* Conectar WhatsApp.
* Desconectar WhatsApp.
* Buscar QR Code.
* Atualizar status da conexão.
* Consultar estado da conexão.
* Reconectar automaticamente quando possível.

Toda comunicação com a Evolution API ocorrerá exclusivamente através do Backend.

O Front-end nunca realizará comunicação direta com a Evolution API.

---

API010 — Histórico

Responsável pelos registros do sistema.

Permitir:

* Buscar histórico.
* Buscar histórico por usuário.
* Buscar histórico por período.
* Buscar histórico por ação.

Os registros permanecerão disponíveis pelos últimos 30 dias.

---

API011 — Assinatura

Responsável pela integração financeira.

Integração:

Asaas

Permitir:

* Consultar assinatura.
* Consultar plano.
* Consultar pagamentos.
* Consultar cobranças.
* Renovar assinatura.
* Cancelar assinatura.
* Consultar período de teste.
* Consultar vencimento.

Todo o processamento financeiro ocorrerá através do Asaas.

---

API012 — Página Pública do Paciente

Responsável pelo link enviado ao paciente.

Permitir:

* Validar token.
* Buscar consulta.
* Confirmar consulta.
* Cancelar consulta.
* Solicitar reagendamento.
* Consultar status atual.

Após o paciente realizar uma ação, o link ficará bloqueado para novas alterações.

Caso seja acessado novamente, apenas exibirá o status atual da consulta.

---

API013 — Webhooks

Responsável por receber eventos de sistemas externos.

Eventos previstos:

Evolution API

* WhatsApp conectado.
* WhatsApp desconectado.
* QR Code atualizado.
* Mensagem enviada.
* Mensagem entregue.
* Falha no envio.

Asaas

* Pagamento aprovado.
* Pagamento recusado.
* Cobrança gerada.
* Assinatura renovada.
* Assinatura cancelada.
* Período de teste encerrado.

Todos os Webhooks deverão validar a autenticidade da origem antes de processar qualquer evento.

---

# 10. VALIDAÇÕES

Todas as APIs deverão validar obrigatoriamente:

* Campos obrigatórios.
* CPF.
* CNPJ.
* Telefone.
* Datas.
* Horários.
* Permissões do usuário.
* Limites definidos pelas regras de negócio.
* Integridade dos dados recebidos.

Nenhuma informação deverá ser gravada sem validação.

---

# 11. UPLOAD DE ARQUIVOS

O sistema permitirá upload apenas para recursos autorizados, como o logotipo da empresa.

Arquivos aceitos:

* PNG
* JPG
* WEBP

Todos os arquivos deverão passar por validação de tipo e tamanho antes do armazenamento.

---

# 12. DOCUMENTAÇÃO DAS APIs

Todas as APIs deverão possuir documentação automática utilizando OpenAPI e Swagger.

A documentação deverá apresentar:

* Endpoint.
* Método HTTP.
* Objetivo.
* Permissões necessárias.
* Campos obrigatórios.
* Campos opcionais.
* Validações.
* Exemplos de requisição.
* Exemplos de resposta.
* Possíveis erros.

Essa documentação servirá como referência oficial para desenvolvimento, manutenção e integração futura.

---

# Resumo da Arquitetura das APIs

| Área          | Decisão                                                                                       |
| ------------- | --------------------------------------------------------------------------------------------- |
| Arquitetura   | REST API                                                                                      |
| Framework     | Django REST Framework                                                                         |
| Comunicação   | HTTPS + JSON                                                                                  |
| Versionamento | `/api/v1/`                                                                                    |
| Autenticação  | E-mail/Senha + Google OAuth                                                                   |
| Sessão        | Persistente com renovação automática e novo login após aproximadamente 30 dias de inatividade |
| Segurança     | Token, RBAC, HTTPS, Rate Limiting, Validação, Sanitização, Logs                               |
| Multi-Tenant  | Isolamento automático por empresa                                                             |
| Documentação  | OpenAPI + Swagger                                                                             |
| Integrações   | Evolution API e Asaas                                                                         |
| Uploads       | PNG, JPG e WEBP                                                                               |
| Webhooks      | Evolution API e Asaas                                                                         |


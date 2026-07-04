
# DOCUMENTO DE ARQUITETURA DO BANCO DE DADOS

**Projeto:**
Micro-SaaS de Confirmação Automatizada de Agendamentos via WhatsApp

---

# Objetivo

Definir a arquitetura responsável pelo armazenamento, organização, integridade, relacionamento e recuperação dos dados do sistema, garantindo segurança, desempenho, escalabilidade e facilidade de evolução do produto.

---

# 1. ARQUITETURA DO BANCO DE DADOS

## Tecnologia

O banco de dados oficial do sistema será o **PostgreSQL**.

Foi escolhido por oferecer alta confiabilidade, excelente desempenho, compatibilidade nativa com Django, suporte a grandes volumes de dados e recursos avançados de integridade e segurança.

Todo o armazenamento permanente do SaaS será realizado através do PostgreSQL.

---

## Modelo de Banco

O sistema utilizará um modelo **Multi-Tenant com Banco Único**.

Todas as empresas compartilharão o mesmo banco de dados físico, porém cada registro estará obrigatoriamente vinculado à empresa proprietária através do identificador da empresa.

Exemplo:

Empresa A

↓

Pacientes

↓

Consultas

↓

Históricos

Empresa B

↓

Pacientes

↓

Consultas

↓

Históricos

Nenhuma empresa poderá acessar registros pertencentes a outra empresa.

Todo acesso será filtrado automaticamente pelo sistema.

---

# 2. ESTRUTURA DAS ENTIDADES

A arquitetura será organizada pelas seguintes entidades principais.

## Empresa

Representa cada cliente do SaaS.

Responsável por armazenar informações como:

* nome da empresa;
* CPF ou CNPJ;
* plano contratado;
* status da assinatura;
* configurações gerais;
* unidade principal.

Cada empresa possuirá seus próprios usuários, pacientes, profissionais, consultas e configurações.

---

## Unidade

A arquitetura será preparada desde o início para suportar múltiplas unidades da mesma empresa.

Embora essa funcionalidade não esteja disponível no MVP, sua estrutura permanecerá preparada para futuras expansões.

Cada unidade poderá possuir seus próprios profissionais, consultas e usuários.

---

## Usuário

Representa todas as pessoas autorizadas a acessar o sistema.

Cada usuário estará vinculado a uma única empresa.

O controle de permissões utilizará o modelo **RBAC (Role Based Access Control)**.

Papéis iniciais:

* Administrador
* Secretária

Novos papéis poderão ser adicionados futuramente sem necessidade de alterar a arquitetura principal.

---

## Paciente

Os pacientes possuirão uma tabela exclusiva.

Cada paciente será cadastrado apenas uma vez dentro da empresa.

As consultas utilizarão referência ao paciente já existente.

Isso evita duplicação de informações e permite manter um histórico centralizado.

Cada paciente armazenará informações como:

* nome;
* telefone;
* data de cadastro;
* empresa responsável.

Quando uma nova consulta for cadastrada utilizando um telefone já existente, o sistema localizará automaticamente o paciente cadastrado.

---

## Profissional

Representa médicos, dentistas ou demais profissionais cadastrados pela empresa.

O uso do profissional será opcional conforme configuração da empresa.

Cada profissional poderá estar associado a diversas consultas.

---

## Consulta

Representa o principal registro operacional do sistema.

Cada consulta estará obrigatoriamente vinculada a:

* empresa;
* paciente.

Opcionalmente poderá possuir vínculo com:

* profissional;
* unidade.

Serão armazenadas informações como:

* data;
* horário;
* status;
* observações;
* horários dos lembretes;
* token de confirmação.

---

## Histórico

Todas as alterações relevantes serão registradas automaticamente.

Exemplos:

* criação;
* edição;
* cancelamento;
* alteração de configurações;
* alteração de usuários;
* alteração do WhatsApp;
* alterações administrativas.

O histórico permanecerá disponível durante os últimos 30 dias, conforme regra de negócio definida.

---

## Templates de Mensagens

As mensagens personalizadas utilizadas no WhatsApp serão armazenadas em uma tabela própria.

Cada empresa poderá possuir seus próprios modelos de mensagem.

Os templates utilizarão variáveis dinâmicas.

Exemplo:

Nome do paciente

Data

Horário

Profissional

Empresa

As variáveis serão substituídas automaticamente durante o envio.

---

## Configurações

As configurações utilizarão uma **abordagem híbrida**.

Configurações simples serão armazenadas em uma estrutura única utilizando **JSONB**.

Exemplos:

* tema do sistema;
* horário do primeiro lembrete;
* horário do segundo lembrete;
* preferências do dashboard;
* configurações gerais.

Recursos mais complexos utilizarão tabelas próprias.

Exemplos:

* usuários;
* templates;
* assinatura;
* WhatsApp;
* histórico.

Essa abordagem reduz a complexidade da arquitetura e facilita futuras expansões.

---

# 3. RELACIONAMENTOS

A estrutura principal do banco seguirá o seguinte relacionamento lógico.

Empresa

↓

Usuários

↓

Pacientes

↓

Consultas

↓

Históricos

↓

Templates

↓

Configurações

Cada entidade permanecerá isolada dentro de sua própria empresa.

---

# 4. IDENTIFICAÇÃO DOS REGISTROS

Todas as entidades principais utilizarão **UUID (Universally Unique Identifier)** como identificador.

Essa abordagem oferece:

* maior segurança;
* impossibilidade prática de prever identificadores;
* facilidade de integração futura;
* melhor compatibilidade com arquiteturas distribuídas.

As entidades que utilizarão UUID incluem:

* Empresa;
* Unidade;
* Usuário;
* Paciente;
* Profissional;
* Consulta.

---

# 5. INTEGRIDADE DOS DADOS

O banco aplicará regras de integridade para impedir inconsistências.

Exemplos:

* consultas não poderão existir sem empresa;
* consultas não poderão existir sem paciente;
* usuários sempre pertencerão a uma empresa;
* profissionais somente poderão ser utilizados pela própria empresa;
* registros não poderão referenciar dados inexistentes.

Essas validações serão reforçadas tanto pelo banco de dados quanto pela aplicação Django.

---

# 6. EXCLUSÃO DE REGISTROS

O sistema utilizará **Soft Delete (Exclusão Lógica)** sempre que aplicável.

Ao excluir um registro:

* ele deixará de aparecer para os usuários;
* continuará armazenado para auditoria e recuperação quando permitido pelas regras do sistema.

Essa abordagem reduz riscos de perda acidental de informações.

---

# 7. DESEMPENHO

Para garantir consultas rápidas mesmo com milhares de registros, serão utilizados índices nos principais campos de pesquisa.

Os principais índices incluem:

* empresa;
* telefone;
* data;
* horário;
* status da consulta;
* profissional;
* paciente.

Essa estratégia reduz significativamente o tempo de busca e melhora a escalabilidade do sistema.

---

# 8. STATUS DOS REGISTROS

As entidades utilizarão estados controlados pelo sistema.

### Consulta

* Agendada
* Mensagem Enviada
* Confirmada
* Cancelada
* Solicitação de Alteração

### Empresa

* Ativa
* Inadimplente
* Suspensa
* Cancelada

### WhatsApp

* Conectado
* Desconectado
* Aguardando Conexão

Todos os status serão controlados exclusivamente pelas regras de negócio do sistema.

---

# 9. BACKUP E RECUPERAÇÃO

O banco de dados utilizará backup automático hospedado na infraestrutura principal.

Os backups serão realizados periodicamente e mantidos por até 30 dias.

Essa estratégia permite recuperação em casos de:

* falha de servidor;
* exclusão acidental;
* corrupção de dados;
* falhas operacionais.

---

# Resumo da Arquitetura

| Área               | Decisão                                           |
| ------------------ | ------------------------------------------------- |
| Banco de Dados     | PostgreSQL                                        |
| Modelo             | Banco Único Multi-Tenant                          |
| Controle de Acesso | RBAC                                              |
| Pacientes          | Tabela exclusiva                                  |
| Profissionais      | Tabela própria                                    |
| Consultas          | Relacionadas ao paciente e empresa                |
| Configurações      | Arquitetura híbrida (JSONB + tabelas específicas) |
| Templates WhatsApp | Modelos dinâmicos                                 |
| Identificadores    | UUID                                              |
| Exclusão           | Soft Delete                                       |
| Integridade        | Restrições no Banco + Django                      |
| Desempenho         | Índices estratégicos                              |
| Backup             | Automático com retenção de 30 dias                |

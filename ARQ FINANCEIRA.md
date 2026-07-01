# DOCUMENTO DE ARQUITETURA FINANCEIRA

## Projeto

Micro-SaaS de Confirmação Automatizada de Agendamentos via WhatsApp

---

# 1. OBJETIVO DA ARQUITETURA FINANCEIRA

Esta arquitetura define toda a estrutura financeira do SaaS, estabelecendo os custos operacionais, ferramentas utilizadas, estratégia de precificação, modelo de assinatura, fluxo de recebimento e diretrizes de escalabilidade financeira.

O objetivo é garantir que o crescimento da plataforma ocorra com alta margem de lucro, custos previsíveis e sustentabilidade no longo prazo.

---

# 2. MODELO DE NEGÓCIO

## Modelo Comercial

Software como Serviço (SaaS)

Modelo de cobrança:

Assinatura recorrente.

A receita da plataforma será baseada exclusivamente em assinaturas recorrentes de empresas e prestadores de serviços que trabalham com agendamento.

Não haverá cobrança por mensagem enviada.

Não haverá cobrança por quantidade de consultas.

Não haverá cobrança por quantidade de pacientes.

O cliente pagará apenas uma assinatura recorrente, independentemente da utilização da plataforma dentro dos limites definidos pelo serviço.

---

# 3. INFRAESTRUTURA FINANCEIRA

## Servidor Principal

Fornecedor:

Hetzner Cloud

Responsável por hospedar:

* Django
* PostgreSQL
* Redis
* Celery
* Evolution API

Estratégia adotada:

Toda a infraestrutura do MVP permanecerá centralizada em uma única VPS para reduzir custos, simplificar a administração do sistema e acelerar o desenvolvimento.

A separação de servidores será considerada apenas quando houver necessidade real de escalabilidade.

---

## Banco de Dados

PostgreSQL

Responsável pelo armazenamento permanente de:

* Empresas
* Usuários
* Pacientes
* Consultas
* Profissionais
* Configurações
* Histórico

---

## Redis

Responsável pelo armazenamento temporário das filas de tarefas.

O Redis não armazena dados permanentes do negócio.

Sua função é manter tarefas temporárias utilizadas pelo Celery.

Exemplo:

Enviar lembrete para determinado paciente no horário programado.

Após a execução da tarefa, ela poderá ser descartada automaticamente.

---

## Celery

Motor responsável pela automação do sistema.

Responsável por:

* envio automático de lembretes
* tarefas agendadas
* execução automática dos processos

Celery é considerado componente essencial da plataforma.

---

## Evolution API

Responsável pela integração entre o SaaS e o WhatsApp das empresas.

Cada empresa conectará seu próprio WhatsApp através da leitura de QR Code.

---

## SSL

Ferramenta:

Let's Encrypt

Responsável por:

* criptografia das informações
* proteção dos dados transmitidos
* navegação segura utilizando HTTPS

Item obrigatório da infraestrutura.

---

## Backup

Fornecedor:

Hetzner Backup

Responsável pela recuperação do sistema em caso de falhas.

Os backups protegerão principalmente:

* banco de dados
* configurações
* informações das empresas

---

## Domínio

Fornecedor:

Registro.br

Domínio principal da plataforma utilizando a extensão .com.br.

---

## E-mail Transacional

Fornecedor:

Resend

Responsável por:

* recuperação de senha
* confirmações
* comunicações automáticas do sistema

---

## Proxy

Fornecedor:

Proxy-Cheap

Estratégia adotada:

1 cliente = 1 proxy dedicado.

Objetivo:

* isolamento operacional
* redução dos riscos relacionados à Evolution API
* proteção das demais empresas caso uma delas enfrente bloqueios ou limitações

Os proxies serão adquiridos conforme o crescimento da base de clientes.

---

# 4. MODELO DE RECEBIMENTO

Gateway de pagamento:

Asaas

Responsável por:

* cobrança recorrente
* geração de assinaturas
* confirmação automática de pagamentos
* integração com o sistema

Formas de pagamento disponíveis:

* Pix
* Cartão de Crédito
* Boleto

O cliente escolherá uma das formas de pagamento durante a contratação.

Após a confirmação do pagamento, o acesso permanecerá ativo.

Em caso de inadimplência, o sistema poderá bloquear automaticamente a utilização da plataforma conforme as regras definidas.

---

# 5. MODELO DE PRECIFICAÇÃO

## Plano Mensal

Valor:

**R$ 120,00 por mês**

Desconto:

**0%**

O plano mensal será utilizado como referência para todos os demais planos da plataforma.

---

## Plano Trimestral

Valor:

**R$ 330,00**

Equivalente a:

**R$ 110,00 por mês**

Desconto:

**Aproximadamente 8%**

---

## Plano Semestral

Valor:

**R$ 600,00**

Equivalente a:

**R$ 100,00 por mês**

Desconto:

**Aproximadamente 17%**

---

## Plano Anual

Valor:

**R$ 1.140,00**

Equivalente a:

**R$ 95,00 por mês**

Desconto:

**Aproximadamente 21%**

---

## Estratégia Comercial

O plano mensal será utilizado como referência de preço da plataforma.

Os planos Trimestral, Semestral e Anual oferecerão descontos progressivos para incentivar contratos de maior duração, aumentar a retenção de clientes, reduzir o índice de cancelamentos (churn) e melhorar o fluxo de caixa da empresa por meio de pagamentos antecipados.

A política de precificação foi definida buscando equilíbrio entre competitividade, previsibilidade financeira e alta margem operacional, mantendo o modelo sustentável para o crescimento da plataforma no longo prazo.
##Período de Teste e Cobrança

O SaaS oferecerá um período de 14 dias gratuitos para novos clientes, permitindo que a empresa configure o sistema, conecte o WhatsApp e utilize todas as funcionalidades disponíveis antes da contratação.

Durante o período de teste, todos os recursos do plano estarão liberados, sem limitações de funcionalidades.

Ao término dos 14 dias, o acesso ao sistema será bloqueado automaticamente até que a empresa escolha um dos planos disponíveis e conclua o pagamento através da plataforma Asaas.

Os planos disponíveis serão:

Mensal: R$ 120,00
Trimestral: R$ 330,00 (aproximadamente 8% de desconto)
Semestral: R$ 600,00 (aproximadamente 17% de desconto)
Anual: R$ 1.140,00 (aproximadamente 25% de desconto)

Todas as cobranças, renovações e confirmações de pagamento serão processadas automaticamente pela plataforma Asaas.

Após a confirmação do pagamento, o acesso ao sistema será restabelecido automaticamente, mantendo todos os dados da empresa e suas configurações.

---

# 6. CUSTOS OPERACIONAIS

A plataforma será composta por custos fixos e custos variáveis.

Os custos fixos correspondem à infraestrutura necessária para manter o SaaS em funcionamento.

Os custos variáveis crescerão proporcionalmente ao aumento da quantidade de clientes ativos, principalmente em relação aos proxies dedicados utilizados pela integração com o WhatsApp.

A estratégia financeira prioriza manter baixos custos fixos durante o MVP e permitir que os custos variáveis acompanhem o crescimento da receita.

---

# 7. DIRETRIZES FINANCEIRAS

Prioridades do MVP

* minimizar custos fixos
* reduzir complexidade operacional
* utilizar infraestrutura unificada
* validar rapidamente o mercado

Durante a fase inicial não serão adotadas infraestruturas distribuídas ou soluções empresariais de alto custo.

Toda expansão deverá ocorrer apenas após validação comercial do produto.

---

# 8. ESTRATÉGIA DE ESCALABILIDADE FINANCEIRA

A infraestrutura será expandida conforme o crescimento da base de clientes.

A prioridade será manter elevada margem operacional antes de aumentar custos.

Novos investimentos em servidores, infraestrutura ou serviços ocorrerão apenas quando houver necessidade comprovada de capacidade.

O crescimento financeiro deverá acompanhar o crescimento da receita, evitando despesas antecipadas que reduzam a lucratividade do negócio.

---

# 9. PRINCÍPIOS FINANCEIROS DO PROJETO

Toda decisão financeira deverá seguir os seguintes princípios:

* manter custos fixos reduzidos;
* maximizar margem operacional;
* priorizar simplicidade no MVP;
* investir em escalabilidade somente após validação comercial;
* proteger a estabilidade da plataforma;
* garantir previsibilidade financeira;
* utilizar assinaturas recorrentes como principal fonte de receita;
* manter o modelo sustentável para crescimento de longo prazo.

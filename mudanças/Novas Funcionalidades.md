
# Novas Funcionalidades

Implementar as funcionalidades abaixo sem alterar a arquitetura existente do sistema.

---

# 1. Central de Gráficos

Adicionar um novo atalho no topo do Dashboard.

Nome:

**Gráficos**

Ao clicar, abrir uma nova página exclusiva para análises da empresa.

Nesta página deverão existir diversos cards com gráficos separados.

Os primeiros gráficos deverão ser:

* Consultas Agendadas
* Consultas Confirmadas
* Consultas Canceladas
* Solicitações de Alteração

Cada gráfico deverá permitir visualizar os dados por:

* Hoje
* Últimos 7 dias
* Últimos 30 dias
* Este mês
* Período personalizado

Utilizar gráficos modernos e profissionais.

---

# 2. Gráficos por Profissional

Dentro da página de gráficos, adicionar um card chamado:

**Profissionais**

Ao acessar esta área:

* listar todos os profissionais cadastrados;
* ao selecionar um profissional, exibir os gráficos individuais dele.

Exemplos:

* quantidade de consultas;
* confirmações;
* cancelamentos;
* solicitações de alteração;
* evolução ao longo do tempo.

Cada profissional deverá possuir seu próprio painel estatístico.

---

# 3. Área Plus

Adicionar um novo card chamado:

**Gendap Plus**

Nesta tela deverá existir uma barra de progresso dos 14 dias gratuitos.

A barra deverá diminuir automaticamente conforme os dias forem passando.

Exemplo:

Dia 1 → barra cheia.

Dia 7 → metade.

Dia 14 → completamente finalizada.

---

## Quando terminar o período gratuito

Após completar os 14 dias:

Ao entrar no sistema, exibir automaticamente uma tela informando que o período gratuito foi encerrado.

Nesta tela deverão aparecer todos os planos disponíveis.

---

## Planos

### Plano Mensal

Valor:

**R$ 120,00**

Desconto:

**0%**

Economia:

**R$ 0,00**

---

### Plano Trimestral

Valor:

**R$ 330,00**

Equivalente:

**R$ 110,00 por mês**

Desconto:

**8%**

Economia:

**R$ 30,00**

---

### Plano Semestral

Valor:

**R$ 600,00**

Equivalente:

**R$ 100,00 por mês**

Desconto:

**17%**

Economia:

**R$ 120,00**

---

### Plano Anual

Valor:

**R$ 1.140,00**

Equivalente:

**R$ 95,00 por mês**

Desconto:

**21%**

Economia:

**R$ 300,00**

---

Cada plano deverá apresentar de forma clara:

* valor total;
* valor mensal equivalente;
* percentual de desconto;
* valor economizado;
* botão para contratação.

A apresentação deve ser profissional, moderna e fácil de comparar.

---

# 4. Suporte

Adicionar um novo item na barra lateral.

Nome:

**Suporte**

Utilizar um ícone apropriado.

Ao clicar:

abrir automaticamente uma conversa no WhatsApp oficial da Gendap.

O número deverá ficar centralizado em configuração para facilitar alterações futuras.

Caso o usuário esteja em um computador:

abrir o WhatsApp Web.

Caso esteja em um celular:

abrir diretamente o aplicativo do WhatsApp.

Não implementar o número fixo no código; deixar essa informação configurável.

---

Ao finalizar toda a implementação:

* validar todas as novas funcionalidades;
* executar a suíte completa de testes;
* garantir que nenhuma funcionalidade existente foi afetada;
* corrigir qualquer regressão antes de concluir a entrega.

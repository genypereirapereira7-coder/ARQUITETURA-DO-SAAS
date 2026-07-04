
# Documento de Arquitetura do Front-end

**Projeto:**
Micro-SaaS de Confirmação Automatizada de Agendamentos via WhatsApp

---

# Objetivo

Definir toda a arquitetura da interface do sistema (Frontend), estabelecendo a organização das telas, navegação, componentes visuais, experiência do usuário (UX), identidade visual e padrões de interação.

Esta arquitetura serve como referência oficial para o desenvolvimento da interface do SaaS, garantindo padronização, facilidade de manutenção, consistência visual e excelente experiência para os usuários.

---

# 1. Arquitetura Geral da Interface

## Modelo da aplicação

O sistema utilizará uma interface administrativa (Dashboard Web) desenvolvida para computadores, com adaptação responsiva para tablets e dispositivos móveis.

Toda a navegação ocorrerá dentro do próprio Dashboard, evitando recarregamentos desnecessários da aplicação.

---

## Estrutura Principal

Após o login, o usuário será direcionado automaticamente para o Dashboard.

A interface será composta por:

* Menu lateral recolhível
* Barra superior
* Área principal de conteúdo
* Sistema de notificações
* Sistema de modais
* Toasts de sucesso e erro

---

# 2. Layout Geral

## Menu Lateral

O menu lateral será fixo.

Permitirá recolhimento quando desejado.

Quando recolhido:

* exibirá apenas os ícones
* manterá toda a navegação funcional

O logotipo da empresa ficará localizado na parte superior do menu lateral.

Itens principais do menu:

* Dashboard
* Consultas
* Profissionais
* Histórico
* Configurações
* Perfil
* Sair

---

## Barra Superior

A barra superior será utilizada para:

* pesquisa rápida
* notificações
* perfil do usuário
* troca de tema (Claro/Escuro)

O perfil ficará localizado no canto superior direito.

Ao clicar no perfil serão exibidas as opções:

* Meu Perfil
* Configurações
* Alterar Tema
* Sair

---

# 3. Dashboard

O Dashboard será a tela principal do sistema.

## Parte Superior

Serão exibidos cards contendo indicadores rápidos.

Exemplos:

* Consultas Agendadas
* Consultas Confirmadas
* Consultas Canceladas
* Solicitações de Alteração

---

## Filtros rápidos

O Dashboard permitirá visualizar:

* Hoje
* Próximos 7 dias
* Próximas consultas
* Todas

O usuário poderá alternar rapidamente entre essas opções.

---

## Área Principal

Logo abaixo dos indicadores será exibida a tabela das consultas.

Ordenação padrão:

Consultas mais próximas primeiro.

---

# 4. Pesquisa Global

O sistema possuirá pesquisa integrada.

Será possível pesquisar:

* telefone
* profissional

Ao localizar um paciente pelo telefone:

ao clicar sobre ele o sistema abrirá automaticamente todo seu histórico.

A pesquisa será realizada enquanto o usuário digita, sem necessidade de pressionar Enter.

---

# 5. Cadastro de Consultas

O cadastro será realizado através de um Modal.

Campos:

* Nome do paciente
* Telefone
* Data
* Horário
* Profissional (opcional)

Ao salvar:

* botão ficará desabilitado
* será exibido Spinner
* cadastro será realizado
* Toast de sucesso aparecerá
* Modal será fechado
* Dashboard será atualizado automaticamente

---

# 6. Edição de Consultas

A edição utilizará exatamente o mesmo Modal utilizado para criação.

Os campos serão carregados automaticamente.

Após salvar:

* Dashboard atualizado
* Lembretes reagendados automaticamente
* Toast de confirmação

---

# 7. Exclusão de Consultas

Nenhuma consulta será removida diretamente.

Sempre será exibido o Modal:

"Tem certeza que deseja excluir esta consulta?"

Botões:

Cancelar

Excluir

---

# 8. Cadastro de Profissionais

Será exibido em tela própria.

Permitirá:

* cadastrar profissional
* editar profissional
* excluir profissional

A pesquisa será realizada pelo nome.

---

# 9. Histórico

O Histórico será apresentado em tabela.

Permitirá:

* pesquisa por telefone
* filtro por período

O histórico armazenará os últimos 30 dias.

---

# 10. Configurações

As configurações serão organizadas em páginas separadas.

Cada configuração possuirá sua própria tela.

Exemplos:

Configuração dos lembretes

Configuração das mensagens

Alteração da empresa

Gerenciamento de usuários

WhatsApp

Segurança

---

# 11. Sistema de Alertas

O sistema utilizará dois modelos de comunicação.

## Toast

Utilizado para:

* sucesso
* avisos rápidos

Será exibido no canto inferior direito.

---

## Alertas

Erros aparecerão:

* abaixo do campo correspondente

Quando necessário:

Toast complementar.

---

## Alertas do Sistema

Problemas importantes aparecerão através de um pequeno indicador vermelho na barra superior.

Ao clicar:

o usuário visualizará todos os problemas encontrados.

Exemplos:

WhatsApp desconectado

Falha de envio

Erro de autenticação

Problemas de configuração

---

# 12. Paginação

Todas as tabelas utilizarão paginação.

Opções:

* 10 registros
* 25 registros
* 50 registros
* 100 registros

Padrão:

25 registros por página.

---

# 13. Ordenação

Todas as tabelas permitirão ordenação clicando no cabeçalho.

Exemplos:

Nome

Telefone

Data

Horário

Status

---

# 14. Loading

Sempre que houver processamento:

será exibido Spinner.

Isso impede ações duplicadas e melhora a experiência do usuário.

---

# 15. Empty State

Quando não existirem registros, serão exibidas mensagens amigáveis.

Exemplos:

"Nenhuma consulta encontrada."

Botão:

"Criar primeira consulta"

---

# 16. Atualização Automática

O Dashboard será atualizado automaticamente sempre que ocorrer:

* nova consulta
* confirmação
* cancelamento
* alteração
* mudança de status

O usuário não precisará atualizar a página manualmente.

---

# 17. Sistema de Temas

O sistema possuirá:

Modo Claro

Modo Escuro

No primeiro acesso:

o sistema detectará automaticamente o tema do sistema operacional.

O usuário poderá alterar quando desejar.

---

# 18. Identidade Visual

Fonte principal:

Inter

Biblioteca de ícones:

Bootstrap Icons

---

## Paleta de cores

### Modo Claro

Fundo branco

Cards cinza claro

Botão principal azul

Sucesso verde

Erro vermelho

Aviso amarelo

---

### Modo Escuro

Fundo cinza escuro

Cards cinza médio

Texto branco

Botão principal azul

---

# 19. Responsividade

Desktop será a plataforma principal.

Em dispositivos móveis:

* menu lateral transforma-se em menu hambúrguer
* cards ficam empilhados
* tabelas adaptam-se para lista
* formulários tornam-se responsivos

---

# 20. Acessibilidade

A interface seguirá boas práticas de acessibilidade.

Inclui:

* contraste adequado
* foco por teclado
* botões acessíveis
* navegação consistente

---

# 21. Atalhos do Sistema

Serão disponibilizados atalhos para aumentar a produtividade.

Exemplos:

Ctrl + N

Nova consulta

Ctrl + F

Pesquisar

Esc

Fechar modal

---

# 22. Feedback Visual

Toda interação fornecerá retorno visual.

Exemplos:

* botões alteram suavemente a cor ao passar o mouse
* cards possuem leve animação
* campos inválidos ficam destacados
* componentes apresentam transições discretas

---

# 23. Atualização da Identidade da Empresa

Ao alterar:

* logotipo
* nome da empresa

toda a interface será atualizada automaticamente, sem necessidade de recarregar a página.

---

# 24. Páginas de Erro

O sistema possuirá páginas próprias para erros.

### Erro 403

Acesso não permitido.

---

### Erro 404

Página não encontrada.

---

### Erro 500

Erro interno do sistema.

As páginas seguirão a identidade visual do SaaS e orientarão o usuário sobre o que ocorreu.

---

# Resumo da Arquitetura

| Área              | Decisão                       |
| ----------------- | ----------------------------- |
| Interface         | Dashboard Administrativo      |
| Navegação         | Menu lateral recolhível       |
| Tema              | Claro e Escuro                |
| Responsividade    | Desktop + Mobile              |
| Pesquisa          | Tempo real                    |
| Cadastro          | Modal                         |
| Atualização       | Automática                    |
| Alertas           | Toast + Indicadores           |
| Histórico         | Pesquisa + filtros            |
| Configurações     | Telas separadas               |
| Fonte             | Inter                         |
| Ícones            | Bootstrap Icons               |
| Paginação         | 10 / 25 / 50 / 100            |
| Loading           | Spinner                       |
| Feedback          | Visual imediato               |
| Acessibilidade    | Implementada                  |
| Atalhos           | Sim                           |
| Identidade Visual | Atualização automática        |
| Páginas de Erro   | 403, 404 e 500 personalizadas |

---

**Objetivo Final**

Esta arquitetura define toda a experiência visual e operacional do Front-end do SaaS, estabelecendo um padrão consistente para todas as telas e interações. Ela servirá como documento oficial para orientar o desenvolvimento da interface, reduzindo ambiguidades, facilitando a implementação por ferramentas de IA e garantindo uma experiência moderna, intuitiva, responsiva e alinhada às melhores práticas de desenvolvimento de software.

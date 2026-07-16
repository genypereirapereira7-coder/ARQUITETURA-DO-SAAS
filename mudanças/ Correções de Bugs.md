# Correções de Bugs e Ajustes de Regras de Negócio

Corrigir os seguintes problemas encontrados durante a validação funcional do sistema.

## 1. Cards do Dashboard

Os cards:

* Agendadas
* Confirmadas
* Canceladas
* Solicitações de Alteração

devem funcionar como filtros rápidos.

Ao clicar em qualquer card, o Dashboard deve atualizar automaticamente a tabela exibindo apenas as consultas correspondentes ao status selecionado.

Exemplo:

* Agendadas → listar apenas consultas agendadas.
* Confirmadas → listar apenas consultas confirmadas.
* Canceladas → listar apenas consultas canceladas.
* Solicitações de Alteração → listar apenas consultas com solicitação de alteração.

---

## 2. Edição de Pacientes

Existe um bug na edição.

Após alterar:

* nome;
* telefone;

e salvar, as alterações não estão sendo persistidas.

Corrigir para que toda edição seja salva corretamente.

---

## 3. Histórico

Na coluna "Responsável", não exibir o e-mail do usuário.

Exibir apenas o nome do administrador ou secretário responsável pela ação.

---

## 4. Configuração dos Lembretes

Remover completamente qualquer referência interna de regras de negócio.

Exemplos:

* RN-008
* RN-010
* RN-002

Esses identificadores nunca devem aparecer na interface do usuário.

Devem permanecer apenas no código e na documentação técnica.

---

## 5. Novo Usuário

Na criação de usuários, remover qualquer texto interno relacionado às regras de negócio.

Também remover o texto:

1. RN-008
2. RN-010
3. RN-002

caso esteja sendo exibido para o usuário sem necessidade operacional.

---

## 6. Confirmação ao Sair

Ao clicar em "Sair", exibir um modal de confirmação.

Mensagem:

"Tem certeza que deseja sair da sua conta?"

Botões:

* Cancelar
* Sair

---

## 7. Validação de Telefone

Implementar validação completa para telefones brasileiros.

Não permitir salvar números inválidos.

A validação deve ocorrer tanto:

* no cadastro;
* quanto na edição.

---

## 8. Paciente Duplicado

Durante o cadastro de uma consulta, quando o usuário informar um telefone já existente na empresa:

o sistema deve identificar automaticamente o paciente.

Exibir uma mensagem informando que já existe um paciente com esse telefone.

Disponibilizar um botão:

"Preencher automaticamente"

Ao clicar, preencher automaticamente os dados do paciente existente.

Evitar duplicação de pacientes.

---

## 9. Pesquisa

Padronizar todas as telas que possuem pesquisa.

Utilizar sempre o mesmo componente:

* campo compacto;
* ícone de pesquisa;
* comportamento idêntico em todas as páginas.

---

## 10. Profissionais

Ao clicar sobre qualquer profissional cadastrado, abrir sua página contendo:

* todas as consultas realizadas por esse profissional;
* histórico completo;
* ordenação cronológica.

---

## 11. Desativação de Administradores

Antes de desativar um administrador, exibir uma confirmação adicional.

Mensagem:

"Tem certeza que deseja desativar este administrador?"

Botões:

* Cancelar
* Desativar

Nenhum administrador deve ser desativado imediatamente sem confirmação.

---

Ao finalizar todas as correções:

* validar toda a implementação;
* executar a suíte completa de testes;
* garantir que nenhuma funcionalidade existente foi afetada;
* corrigir qualquer regressão encontrada antes de concluir a entrega.

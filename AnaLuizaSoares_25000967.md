# Avaliação — Engenharia de Software
**Sistema Integrado de Gestão de Farmácia — MVP Definido pelo Estudante**

Aluno: Ana Luiza Soares  
RA: 25000967 
Data: 25/03/2026 

---

# 1. Definição do MVP
Meu MVP foca na integração entre venda, estoque e financeiro, cobrindo desde o cadastro de clientes e produtos até a baixa automática de mercadoria e geração de lançamentos em contas a receber (vendas a prazo) ou a pagar (compras de fornecedores), garantindo que nenhuma transação ocorra sem a devida atualização em tempo real.

Dentro do MVP haverá o Cadastro de clientes/produtos, processo de venda (à vista e a prazo), baixa automática de estoque e geração de contas a receber/pagar. E fora do MVP poderá ter relatórios complexos de BI como indicadores de desempenho, transferências entre unidades e gestão de impostos.
O foco será na resolução da dessincronização entre setores, garantindo que a venda reflita instantaneamente no estoque e no financeiro.


---

# 2. Regras de Negócio (mínimo: 5)

**RN01** — **Venda de receita controlada:** Medicamentos de controle especial só poderão ser vendidos mediante validação e retenção da receita adequada.

**RN02** — **Estoque Mínimo:** O sistema deve emitir um alerta visual ao gerente quando o saldo de um produto atingir o limite definido.  

**RN03** — **Saída de mercadoria:** Qualquer venda, perda ou devolução de produto deverá ter baixa automática em tempo real.  

**RN04** — **Vendas a Prazo:** Somente clientes devidamente cadastrados e sem débitos atrasados poderão realizar compras a prazo.

**RN05** — **Bloqueio de venda sem estoque:** O sistema deverá impedir a compra de produtos sem saldo disponível.



---

# 3. Requisitos Funcionais (mínimo: 8)

**RF01** — O sistema deve realizar o cadastro de produtos com os dados fundamentais: descrição, preço, fabricante e lote.

**RF02** — O sistema deve utilizar o código de barras ou nome para pesquisar os produtos.

**RF03** — O sistema deve conectar produtos, quantidades e vendedor ao registrar vendas.

**RF04** — O sistema deve cadastrar rapidamente novos clientes no ato da venda.  

**RF05** — O sistema deve gerar automaticamente lançamentos em Contas a Receber para vendas a prazo.  

**RF06** — O sistema deve atualizar o estoque automaticamente após a venda ser completada (pagamento). 

**RF07** — O sistema deve permitir registro de autorização de receitas pelo farmacêutico. 

**RF08**— O sistema deve emitir comprovante de venda. 



---

# 🛡 4. Requisitos Não Funcionais (mínimo: 4)

**RNF01 — **Sincronização de dados:** O sistema deve atualizar a base de dados após qualquer alteração de estoque.

**RNF02 — **Retenção de Dados das Receitas:** O sistema deve manter o registro das receitas autorizadas conforme legislação vigente.

**RNF03 — **Estabilidade:** O sistema deve aguentar o funcionamento contínuo de 24h em todos os dias da semana.

**RNF04 — **Impressão de Comprovante:** O sistema deve emitir de forma rápida o cupom de venda.  


---

# 5. Casos de Uso (mínimo: 10)

**UC01** — Realizar Venda

**UC02** — Autenticar Usuário

**UC03** — Consultar Estoque

**UC04** — Emitir Comprovante

**UC05** — Cadastrar Cliente (Atendente)

**UC06** — Validar Receita Médica (Farmacêutico)

**UC07** — Aplicar Desconto Especial (Gerente)

**UC08** — Registrar Entrada de Mercadoria

**UC09** — Realizar Lançamento Financeiro

**UC10** — Gerar Relatório de Vendas

<img width="1206" height="831" alt="image" src="https://github.com/user-attachments/assets/2c2a4e04-cfdb-4618-80ba-c6b517b6fbce" />

---

# 6. Documentação dos Casos de Uso
**UC01 — Realizar Venda**

**Ator(es):** Atendente

**Descrição:** Registrar a venda de produtos para o cliente e processar o pagamento.

**Pré-condições:** Usuário verificado e produtos disponíveis em estoque.

**Pós-condições:** Estoque atualizado e venda registrada no banco de dados.

### Fluxo Principal
1. Atendente inicia nova venda.
2. Atendente identifica os produtos via código de barras.
3. Sistema verifica a disponibilidade de cada item.
4. Atendente confirma o método de pagamento.
5. Sistema registra a venda e gera o cupom 

### Fluxos Alternativos / Exceções
- FA01 — Cliente não cadastrado: Atendente realiza o registro rápido.
- FA02 — Medicamento controlado: O sistema solicita a validação da receita pelo farmacêutico

### Relacionamentos
- **Include:** UC02, UC03, UC04.

- **Extend:** UC05, UC06, UC07.

<img width="479" height="1113" alt="image" src="https://github.com/user-attachments/assets/54db93f1-aca4-4f89-8bb1-eed8366c9a8a" />

---

**UC02 — Autenticar Usuário**

**Ator(es):** Todos os Atores

**Descrição:** Validação de credenciais para acesso às atividades do sistema de acordo com o perfil.

**Pré-condições:** Sistema operacional e banco de dados ativos.

**Pós-condições:** Usuário com sessão ativa e permissões de acesso liberadas.

### Fluxo Principal
1. Usuário insere login e senha na tela inicial.
2. Sistema criptografa a senha e compara com a base de dados.
3. Sistema identifica o perfil do usuário (Atendente, Farmacêutico, Gerente, etc.).
4; Sistema libera o menu principal correspondente às permissões do perfil.

### Fluxos Alternativos / Exceções
- FA01 — Credenciais inválidas: Sistema nega o acesso e solicita nova tentativa.
- FA02 — Usuário bloqueado: Sistema informa que o usuário deve procurar o Administrador.

### Relacionamentos
- **Include:** UC01, UC08, UC09 e UC10.

<img width="509" height="517" alt="image" src="https://github.com/user-attachments/assets/38793b0a-64ff-4c2d-94b1-55079148be4f" />

---
**UC03 — Consultar Estoque**

**Ator(es):** Atendente e Gerente

**Descrição:** Verificação da quantidade disponível de um item em tempo real.

**Pré-condições:** Produto cadastrado no sistema.

**Pós-condições:** Informação de saldo e localização do item exibida na tela.

### Fluxo Principal
1. Usuário digita o nome ou bipar o código do produto.
2. Sistema consulta o saldo atual na unidade local.
3. Sistema exibe a quantidade disponível e o preço unitário.

### Fluxos Alternativos / Exceções
- FA01 — Produto inexistente: Sistema sugere busca por fabricante ou categoria.
- FA02 — Estoque zerado: Sistema sugere consulta em outras unidades da rede.

### Relacionamentos
- **Include:** UC01 e UC08.

<img width="531" height="505" alt="image" src="https://github.com/user-attachments/assets/6f5ad1ea-f624-4aa9-841d-0b4241bad571" />

---
**UC04 — Emitir Comprovante**

**Ator(es):** Atendente

**Descrição:** Geração de documento físico ou digital com o resumo da transação.

**Pré-condições:** Venda finalizada com sucesso.

**Pós-condições:** Cupom impresso ou enviado ao cliente.

###  Fluxo Principal
1. Sistema processa os dados da venda concluída.
2. Sistema formata os dados itens, valores e data.
3. Sistema envia o comando para a impressora local.
4 Atendente entrega o comprovante ao cliente.

### Fluxos Alternativos / Exceções
- FA01 — Falha na impressora: Atendente reinicia o comando.

### Relacionamentos
- **Include:** UC01.

<img width="455" height="467" alt="image" src="https://github.com/user-attachments/assets/5d57f9b9-b6e5-4d6d-b1d8-9adb0a1e9ab5" />

---
**UC05 — Cadastrar Cliente**

**Ator(es):** Atendente

**Descrição:** Inclusão de novos clientes na base de dados para histórico e convênios.

**Pré-condições:** CPF do cliente não cadastrado previamente.

**Pós-condições:** Cadastro criado no banco de dados.

### Fluxo Principal
1. Atendente acessa o formulário de cadastro.
2. Insere Nome, CPF, Telefone e Endereço.
3. Sistema valida o formato dos documentos.
4. Sistema salva o novo registro e gera o ID do cliente.

### Fluxos Alternativos / Exceções
- FA01 — CPF já cadastrado: Sistema exibe os dados atuais para atualização.

### Relacionamentos
- **Extend:** UC01.

<img width="461" height="413" alt="image" src="https://github.com/user-attachments/assets/58c25366-9907-48df-98b9-9f7a6ce3d760" />

---
**UC06 — Validar Receita Médica**

**Ator(es):** Farmacêutico

**Descrição:** Conferência de receitas para liberação de medicamentos controlados.

**Pré-condições:** Item de venda classificado como "Controlado".

**Pós-condições:** Autorização registrada e vinculada à venda.

### Fluxo Principal
1. Farmacêutico recebe o alerta de validação pendente.
2. Confere os dados do médico (CRM) e a validade da receita física.
3. Insere os dados da receita no sistema (Data, CRM, Paciente).
4. Confirma a liberação para que a venda possa ser paga.

### Fluxos Alternativos / Exceções
- FA01 — Receita irregular: Farmacêutico nega a validação.

### Relacionamentos
- **Extend** UC01.

<img width="487" height="413" alt="image" src="https://github.com/user-attachments/assets/22b7cd06-a998-4a06-a6c8-e70a5887de0d" />

---
**UC07 — Aplicar Desconto Especial**

**Ator(es):** Gerente

**Descrição:** Autorização de preços abaixo da margem padrão do sistema.

**Pré-condições:** Solicitação de desconto superior ao limite do atendente.

**Pós-condições:** Valor da venda recalculado com o novo desconto.

### Fluxo Principal
1. Atendente solicita o desconto na tela de venda.
2. Sistema exige a senha de autorização do Gerente.
3. Gerente avalia o valor e insere suas credenciais.
4. Sistema aplica o novo preço e prossegue com a venda.

### Fluxos Alternativos / Exceções
- FA01 — Desconto negado: Gerente cancela a solicitação.

### Relacionamentos
- **Extend:** UC01.

<img width="500" height="413" alt="image" src="https://github.com/user-attachments/assets/7cb6c0e0-2991-409e-96f7-79c9e702b676" />

---
**UC08 — Registrar Entrada de Mercadoria**

**Ator(es):** Gerente

**Descrição:** Atualização de estoque e custos a partir de compras de fornecedores.

**Pré-condições:** Usuário autenticado como Gerente.

**Pós-condições:** Saldos de estoque atualizados.

### Fluxo Principal
1. Gerente inicia a entrada de nota fiscal.
2. Identifica o fornecedor e os itens recebidos.
3. Sistema atualiza as quantidades em estoque.
4. Sistema envia os dados para registro de dívida no financeiro.

### Fluxos Alternativos / Exceções
- FA01 — Divergência de quantidade: Gerente registra a diferença e abre chamado de devolução.

### Relacionamentos
- **Include:** UC02, UC03.

<img width="467" height="413" alt="image" src="https://github.com/user-attachments/assets/4815105b-0c0f-40eb-8db3-52a41a0d8db0" />

---
**UC09 — Realizar Lançamento Financeiro**

**Ator(es):** Setor Financeiro

**Descrição:** Registro de contas a pagar e receber.

**Pré-condições:** Usuário autenticado e venda a prazo ou compra.

**Pós-condições:** Título financeiro registrado com data de vencimento e status.

### Fluxo Principal
1. Sistema recebe os dados de uma venda a prazo ou entrada de mercadoria.
2. Sistema gera o lançamento com valor, data de emissão e vencimento.
3. Usuário do financeiro valida e confirma o lançamento.
4 Sistema altera o status para "Aberto".

### Fluxos Alternativos / Exceções
- FA01 — Lançamento manual: Usuário insere despesas fixas sem vínculo com venda/compra.

### Relacionamentos
- **Include:** UC02.

<img width="481" height="413" alt="image" src="https://github.com/user-attachments/assets/59715eff-6fe8-4b79-853a-65d9ba038611" />

---
**UC10 — Gerar Relatório de Vendas**

**Ator(es):** Gerente e Administrador

**Descrição:** Apresentação de dados de vendas para análise gerencial.

**Pré-condições:** Usuário autenticado e existência de vendas no período selecionado.

**Pós-condições:** Relatório exibido em tela ou exportado.

### Fluxo Principal
1. Usuário seleciona o tipo de relatório e o período.
2. Sistema processa os dados de vendas e estoque.
3. Sistema organiza as informações em formato de lista ou tabela.
4. Usuário visualiza ou exporta o resultado.

### Fluxos Alternativos / Exceções
- FA01 — Sem dados no período.

### Relacionamentos
- **Include:** UC02.


### Inserir o diagrama de atividades do Caso de Uso, demonstrando tudo o fluxo princial e alternativos/exceções.

<img width="470" height="505" alt="image" src="https://github.com/user-attachments/assets/a80c1c9d-3d5e-41c0-b7bb-8f16e3611e83" />

---


# CDS Views - Projetos Práticos

Este repositório contém projetos práticos para praticar a criação de CDS Views no SAP utilizando o Eclipse. Cada projeto utiliza tabelas padrão do SAP GUI e implementa diferentes funcionalidades para aprimorar o conhecimento sobre CDS Views.

## Conteúdo Estudado

Os projetos foram desenvolvidos com base nos seguintes conceitos:

- CDS Views Básico
- Group By e Having
- Campos Calculados, Funções, Casting e Case
- Joins
- Associação
- Union
- Parâmetros

## Projetos

### **Projeto 1: Relatório de Vendas por Cliente**
**Objetivo:** Criar uma CDS View que exiba o total de vendas por cliente.

**Tabelas utilizadas:**
- `VBAK` (Documentos de vendas - Cabeçalho)
- `VBAP` (Itens de vendas)
- `KNA1` (Clientes)

**Recursos utilizados:**
- Joins
- Group By
- Funções agregadas (`SUM` para calcular o total de vendas)

---

### **Projeto 2: Estoque de Materiais por Centro**
**Objetivo:** Criar uma CDS View que liste os materiais e seus estoques por centro.

**Tabelas utilizadas:**
- `MARD` (Estoque por centro)
- `MAKT` (Descrição de materiais)
- `T001W` (Centros)

**Recursos utilizados:**
- Joins
- Casting (converter tipos de dados)
- Case (para categorizar materiais)

---

### **Projeto 3: Relatório de Pedidos de Compras Abertos**
**Objetivo:** Criar uma CDS View para listar os pedidos de compra que ainda não foram entregues.

**Tabelas utilizadas:**
- `EKKO` (Cabeçalho de pedido de compras)
- `EKPO` (Itens do pedido)
- `LFA1` (Fornecedores)

**Recursos utilizados:**
- Joins e Associações
- Condição `WHERE` para filtrar pedidos não entregues
- Funções para calcular valores pendentes

---

### **Projeto 4: Comparação de Faturamento Anual**
**Objetivo:** Criar uma CDS View para comparar o faturamento dos últimos dois anos.

**Tabelas utilizadas:**
- `VBRK` (Cabeçalho de faturas)
- `VBRP` (Itens da fatura)

**Recursos utilizados:**
- Group By e Having
- Funções agregadas
- Union para consolidar diferentes anos

---

### **Projeto 5: Relatório de Prazos de Pagamento por Cliente**
**Objetivo:** Criar uma CDS View para exibir os clientes e seus prazos de pagamento.

**Tabelas utilizadas:**
- `KNA1` (Clientes)
- `KNB1` (Dados financeiros do cliente)
- `T052` (Condições de pagamento)

**Recursos utilizados:**
- Joins e Associações
- Parâmetros para filtrar clientes por país ou tipo de conta

---

## Referências
- [Playlist de estudos no YouTube](https://www.youtube.com/watch?v=pSg0PR0hzjc&list=PLnpMwD8LFgjhsNU6J2m4BiyjBpXhTdUaj)


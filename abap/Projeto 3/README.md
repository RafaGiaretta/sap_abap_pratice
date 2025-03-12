# Relatório de Vendas com Detalhes de Produtos e Clientes

## Descrição do Projeto
Este projeto tem como objetivo gerar um relatório detalhado de vendas no SAP. O sistema buscará informações sobre:
- **Pedidos de venda** (VBAK)
- **Itens de venda** (VBAP)
- **Dados de clientes** (KNA1)
- **Informações sobre materiais vendidos** (MARA)

O relatório permitirá a aplicação de filtros e será exibido de forma estruturada, incluindo cálculos do total de vendas por cliente e por produto.

## Requisitos Funcionais
O usuário poderá selecionar os seguintes filtros:
- **Número do pedido de venda** (VBELN)
- **Data do pedido de venda** (AUDAT)
- **Código do cliente** (KUNNR)
- **Código do material** (MATNR)

O relatório exibirá as seguintes informações:
1. **Informações do pedido de venda:**
   - Número do pedido
   - Data do pedido
   - Código do cliente
2. **Detalhes dos itens do pedido:**
   - Número do item
   - Quantidade
   - Valor
3. **Dados do cliente:**
   - Nome do cliente
   - Informações de contato
4. **Detalhes do material:**
   - Nome
   - Descrição
   - Quantidade

## Tecnologias Utilizadas
- **SAP ABAP** para desenvolvimento do relatório
- **SAP GUI** para execução
- **Tabelas SAP**: VBAK, VBAP, KNA1, MARA

## Como Executar
1. Acesse o ambiente SAP e abra o SAP GUI.
2. Execute o relatório através da transação correspondente.
3. Informe os filtros desejados.
4. Visualize e analise os resultados gerados.

## Contribuição
Contribuições são bem-vindas! Sinta-se à vontade para abrir um *pull request* ou sugerir melhorias via *issues*.

## Licença
Este projeto está sob a licença MIT. Consulte o arquivo `LICENSE` para mais detalhes.


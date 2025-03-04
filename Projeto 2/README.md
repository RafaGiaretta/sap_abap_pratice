# Extrator de Dados Mestres - SAP ABAP

## 1. Objetivo

Desenvolver um programa SAP ABAP para extração e integração dos dados mestres do portal Nota de Débito, utilizando exclusivamente tabelas customizadas. Dessa forma, elimina-se a dependência de tabelas standard do sistema, permitindo total controle sobre os cadastros e facilitando a manutenção e futuras atualizações.

---

## 2. Escopo do Projeto

### Utilização Exclusiva de Tabelas Customizadas

Todos os dados mestres serão armazenados e gerenciados por tabelas criadas especificamente para este projeto (prefixo **ZEXT\_**).

### Áreas de Dados a Serem Gerenciadas

- Empresa
- Sociedade Parceira
- Divisão
- Centro
- Plano de Contas/Contas
- Centro de Custo
- Centro de Lucro
- Ordem de Investimento
- Elemento PEP
- Network
- Parâmetros e Constantes
- Log de Extração

### Geração de Arquivos

Os dados serão extraídos e gravados em arquivos de texto (`.txt`) com os campos separados pelo caractere `|` e, paralelamente, convertidos para PDF. Os arquivos serão salvos em um diretório configurável (ex.: `\SAPIDES\sapmnt\trans`).

### Agendamento e Execução

A execução será realizada por meio de **job (agendamento diário)**, processando os registros criados ou alterados conforme a data informada na seleção.

---

## 3. Estrutura das Tabelas Customizadas

A seguir, apresenta-se a definição das tabelas a serem criadas e seus principais campos:

### 3.1. ZEXT_EMPRESA

**Finalidade:** Armazenar os dados das empresas.

**Campos:**

- `EMPRESA_ID` (CHAR 4) – Chave primária
- `NOME` (VARCHAR 50)
- `CNPJ` (CHAR 14)
- `INSCRICAO_ESTADUAL` (VARCHAR 20)
- `PAIS` (CHAR 3)
- `ENDERECO` (VARCHAR 100)
- `CIDADE_ESTADO` (VARCHAR 50)
- `CEP` (CHAR 8)
- `MOEDA_PADRAO` (CHAR 3)

**Valores para Tabela:**

```sql
INSERT INTO ZEXT_EMPRESA VALUES ('7000', 'Empresa Alpha', '12345678000190', 'ISENTO', 'BR', 'Av. Paulista, 1000', 'Sao Paulo/SP', '01310000', 'BRL');
INSERT INTO ZEXT_EMPRESA VALUES ('7020', 'Empresa Beta', '98765432000195', '123456789', 'BR', 'Rua das Flores, 200', 'Rio de Janeiro/RJ', '20040030', 'BRL');
INSERT INTO ZEXT_EMPRESA VALUES ('7060', 'Empresa Gamma', '11223344556677', '654321987', 'BR', 'Av. Atlantica, 300', 'Copacabana/RJ', '22041001', 'BRL');
INSERT INTO ZEXT_EMPRESA VALUES ('7100', 'Empresa Delta', '99887766554433', '112233445', 'BR', 'Rua 7 de Setembro, 400', 'Belo Horizonte/MG', '30130000', 'BRL');
INSERT INTO ZEXT_EMPRESA VALUES ('7150', 'Empresa Epsilon', '55667788990011', '99887766', 'BR', 'Av. das Nações, 500', 'Curitiba/PR', '80010200', 'BRL');

```

### 3.2. ZEXT_SOCIEDADE

**Finalidade:** Armazenar os dados da Sociedade Parceira.

**Campos:**

- `SOCIEDADE_ID` (CHAR 4) – Chave primária
- `NOME` (VARCHAR 50)
- `RAIZ` (VARCHAR 50)
- `PAIS` (CHAR 3)
- `MOEDA` (CHAR 3)
- `RUA` (VARCHAR 100)
- `CEP` (CHAR 8)
- `CIDADE` (VARCHAR 50)

**Valores para cadastro:**

```sql
INSERT INTO ZEXT_SOCIEDADE VALUES ('SP01', 'Sociedade Alpha', 'RAIZ1', 'BR', 'BRL', 'Rua A, 10', '01001000', 'Sao Paulo');
INSERT INTO ZEXT_SOCIEDADE VALUES ('SP02', 'Sociedade Beta', 'RAIZ2', 'BR', 'BRL', 'Av. B, 20', '02002000', 'Sao Paulo');
INSERT INTO ZEXT_SOCIEDADE VALUES ('RJ01', 'Sociedade Gamma', 'RAIZ3', 'BR', 'BRL', 'Rua C, 30', '03003000', 'Rio de Janeiro');
INSERT INTO ZEXT_SOCIEDADE VALUES ('RJ02', 'Sociedade Delta', 'RAIZ4', 'BR', 'BRL', 'Av. D, 40', '04004000', 'Rio de Janeiro');
INSERT INTO ZEXT_SOCIEDADE VALUES ('MG01', 'Sociedade Epsilon', 'RAIZ5', 'BR', 'BRL', 'Rua E, 50', '05005000', 'Belo Horizonte');

```

### 3.3. ZEXT_DIVISAO

**Finalidade:** mazenar informações das divisões da organização.

**Campos:**

- `DIVISAO_ID (CHAR 2) – Chave primária`
- `DESCRIÇÃO (VARCHAR 50)`

**Valores para cadastro:**

```sql
INSERT INTO ZEXT_DIVISAO VALUES ('01', 'Divisão Comercial');
INSERT INTO ZEXT_DIVISAO VALUES ('02', 'Divisão Financeira');
INSERT INTO ZEXT_DIVISAO VALUES ('03', 'Divisão Operacional');
INSERT INTO ZEXT_DIVISAO VALUES ('04', 'Divisão de RH');
INSERT INTO ZEXT_DIVISAO VALUES ('05', 'Divisão de TI');

```

### 3.4. ZEXT_CENTRO

**Finalidade:** Registrar os centros de trabalho ou produção.

**Campos:**

- `CENTRO_ID (CHAR 4) – Chave primária`
- `NOME (VARCHAR 50)`
- `EMPRESA_ID (CHAR 4) – Referência para ZEXT_EMPRESA`

**Valores para cadastro:**

```sql
INSERT INTO ZEXT_CENTRO VALUES ('C001', 'Centro Alpha', '7000');
INSERT INTO ZEXT_CENTRO VALUES ('C002', 'Centro Beta', '7020');
INSERT INTO ZEXT_CENTRO VALUES ('C003', 'Centro Gamma', '7060');
INSERT INTO ZEXT_CENTRO VALUES ('C004', 'Centro Delta', '7100');
INSERT INTO ZEXT_CENTRO VALUES ('C005', 'Centro Epsilon', '7150');

```

### 3.5. ZEXT_CONTAS

**Finalidade:** Gerenciar o Plano de Contas, com todos os atributos necessários.

**Campos:**

- `CONTA (CHAR 10) – Chave primária`
- `PLANO_CONTA (CHAR 4)`
- `DESCRICAO (VARCHAR 100)`
- `CONTA_BALANCO (CHAR 10)`
- `CENTRO (CHAR 4)`
- `MATERIAL (CHAR 1)`
- `CCUSTO (CHAR 1)`
- `ORDEM (CHAR 1)`
- `PEP (CHAR 1)`
- `NETWORK (CHAR 1)`
- `BL_LAN_PLANO (CHAR 1)`
- `EMPRESA (CHAR 4)`
- `BL_LAN_EMPRESA (CHAR 1)`

**Valores para cadastro:**

```sql
INSERT INTO ZEXT_CONTAS VALUES ('0000000001', '1000', 'Conta de Ativo', '0000000001', 'C001', 'X', 'X', 'X', 'X', 'X', 'X', '7000', 'X');
INSERT INTO ZEXT_CONTAS VALUES ('0000000002', '1001', 'Conta de Passivo', '0000000002', 'C002', 'X', ' ', 'X', ' ', 'X', ' ', '7020', ' ');
INSERT INTO ZEXT_CONTAS VALUES ('0000000003', '1002', 'Conta de Receita', '0000000003', 'C003', ' ', 'X', ' ', 'X', ' ', 'X', '7060', 'X');
INSERT INTO ZEXT_CONTAS VALUES ('0000000004', '1003', 'Conta de Despesa', '0000000004', 'C004', 'X', 'X', ' ', ' ', 'X', 'X', '7100', ' ');
INSERT INTO ZEXT_CONTAS VALUES ('0000000005', '1004', 'Conta de Lucro', '0000000005', 'C005', ' ', ' ', 'X', 'X', ' ', ' ', '7150', 'X');

```

### 3.6. ZEXT_CENTROCUSTO

**Finalidade:** Registrar os centros de custo da organização.

**Campos:**

- `CENTROCUSTO_ID (CHAR 10) – Chave primária`
- `AREA_CONTABILIDADE (CHAR 4)`
- `DESCRICAO (VARCHAR 100)`
- `EMPRESA (CHAR 4)`
- `UNIDADE (CHAR 2)`
- `RESPONSAVEL (VARCHAR 50)`
- `BLOQUEADO (CHAR 1)`
- `VALIDO_DESDE (DATE)`
- `VALIDO_ATE (DATE)`

**Valores para cadastro:**

```sql
INSERT INTO ZEXT_CENTROCUSTO VALUES ('CC00000001', 'AC01', 'Centro de Custo Alpha', '7000', '01', 'João Silva', 'X', '2024-01-01', '2024-12-31');
INSERT INTO ZEXT_CENTROCUSTO VALUES ('CC00000002', 'AC02', 'Centro de Custo Beta', '7020', '02', 'Maria Souza', ' ', '2024-01-01', '2024-12-31');
INSERT INTO ZEXT_CENTROCUSTO VALUES ('CC00000003', 'AC03', 'Centro de Custo Gamma', '7060', '01', 'Carlos Lima', 'X', '2024-01-01', '2024-12-31');
INSERT INTO ZEXT_CENTROCUSTO VALUES ('CC00000004', 'AC04', 'Centro de Custo Delta', '7100', '03', 'Ana Pereira', ' ', '2024-01-01', '2024-12-31');
INSERT INTO ZEXT_CENTROCUSTO VALUES ('CC00000005', 'AC05', 'Centro de Custo Epsilon', '7150', '02', 'Paulo Santos', 'X', '2024-01-01', '2024-12-31');

```

### 3.7. ZEXT_CENTROLUCRO

**Finalidade:** Gerenciar os centros de lucro.

**Campos:**

- `CENTROLUCRO_ID (CHAR 10) – Chave primária`
- `DESCRICAO (VARCHAR 100)`
- `EMPRESA (CHAR 4)`
- `RESPONSAVEL (VARCHAR 50)`
- `BLOQUEADO (CHAR 1)`
- `VALIDO_DESDE (DATE)`
- `VALIDO_ATE (DATE)`

**Valores para cadastro:**

```sql
INSERT INTO ZEXT_CENTROLUCRO VALUES ('CL00000001', 'Centro de Lucro Alpha', '7000', 'João Silva', ' ', '2024-01-01', '2024-12-31');
INSERT INTO ZEXT_CENTROLUCRO VALUES ('CL00000002', 'Centro de Lucro Beta', '7020', 'Maria Souza', 'X', '2024-01-01', '2024-12-31');
INSERT INTO ZEXT_CENTROLUCRO VALUES ('CL00000003', 'Centro de Lucro Gamma', '7060', 'Carlos Lima', ' ', '2024-01-01', '2024-12-31');
INSERT INTO ZEXT_CENTROLUCRO VALUES ('CL00000004', 'Centro de Lucro Delta', '7100', 'Ana Pereira', 'X', '2024-01-01', '2024-12-31');
INSERT INTO ZEXT_CENTROLUCRO VALUES ('CL00000005', 'Centro de Lucro Epsilon', '7150', 'Paulo Santos', ' ', '2024-01-01', '2024-12-31');

```

### 3.8. ZEXT_ORDEM

**Finalidade:** Gerenciar as ordens de investimento.

**Campos:**

- `ORDEM_ID (CHAR 12) – Chave primária`
- `DESCRICAO (VARCHAR 100)`
- `EMPRESA (CHAR 4)`
- `UNIDADE (CHAR 4)`
- `RESPONSAVEL (VARCHAR 50)`
- `BLOQUEADO (CHAR 1)`
- `SISTEMA_STATUS (CHAR 1)`
- `USUARIO_STATUS (CHAR 1)`
- `DATA_CRIACAO (DATE)`

**Valores para cadastro:**

```sql
INSERT INTO ZEXT_ORDEM VALUES ('OR0000000001', 'Ordem de Investimento Alpha', '7000', 'U001', 'João Silva', ' ', 'A', 'A', '2024-02-01');
INSERT INTO ZEXT_ORDEM VALUES ('OR0000000002', 'Ordem de Investimento Beta', '7020', 'U002', 'Maria Souza', 'X', 'B', 'B', '2024-02-01');
INSERT INTO ZEXT_ORDEM VALUES ('OR0000000003', 'Ordem de Investimento Gamma', '7060', 'U003', 'Carlos Lima', ' ', 'A', 'A', '2024-02-01');
INSERT INTO ZEXT_ORDEM VALUES ('OR0000000004', 'Ordem de Investimento Delta', '7100', 'U004', 'Ana Pereira', 'X', 'B', 'B', '2024-02-01');
INSERT INTO ZEXT_ORDEM VALUES ('OR0000000005', 'Ordem de Investimento Epsilon', '7150', 'U005', 'Paulo Santos', ' ', 'A', 'A', '2024-02-01');

```

### 3.9. ZEXT_PEP

**Finalidade:** Gerenciar os elementos PEP.

**Campos:**

- `PEP_ID (CHAR 12) – Chave primária`
- `DESCRICAO (VARCHAR 100)`
- `EMPRESA (CHAR 4)`
- `UNIDADE (CHAR 4)`
- `RESPONSAVEL (VARCHAR 50)`
- `BLOQUEADO (CHAR 1)`
- `SISTEMA_STATUS (CHAR 1)`
- `USUARIO_STATUS (CHAR 1)`
- `DATA_CRIACAO (DATE)`

**Valores para cadastro:**

```sql
INSERT INTO ZEXT_PEP VALUES ('PEP000000001', 'Elemento PEP Alpha', '7000', 'U001', 'João Silva', ' ', 'A', 'A', '2024-03-01');
INSERT INTO ZEXT_PEP VALUES ('PEP000000002', 'Elemento PEP Beta', '7020', 'U002', 'Maria Souza', 'X', 'B', 'B', '2024-03-01');
INSERT INTO ZEXT_PEP VALUES ('PEP000000003', 'Elemento PEP Gamma', '7060', 'U003', 'Carlos Lima', ' ', 'A', 'A', '2024-03-01');
INSERT INTO ZEXT_PEP VALUES ('PEP000000004', 'Elemento PEP Delta', '7100', 'U004', 'Ana Pereira', 'X', 'B', 'B', '2024-03-01');
INSERT INTO ZEXT_PEP VALUES ('PEP000000005', 'Elemento PEP Epsilon', '7150', 'U005', 'Paulo Santos', ' ', 'A', 'A', '2024-03-01');

```

### 3.10. ZEXT_NETWORK

**Finalidade:** Gerenciar os dados relativos às networks.

**Campos:**

- `NETWORK_ID (CHAR 12) – Chave primária`
- `OPERACAO (VARCHAR 50)`
- `PEP (CHAR 12)`
- `DESCRICAO (VARCHAR 100)`
- `EMPRESA (CHAR 4)`
- `UNIDADE (CHAR 4)`
- `RESPONSAVEL (VARCHAR 50)`
- `BLOQUEADO (CHAR 1)`
- `SISTEMA_STATUS (CHAR 1)`
- `USUARIO_STATUS (CHAR 1)`
- `DATA_CRIACAO (DATE)`

**Valores para cadastro:**

```sql
INSERT INTO ZEXT_NETWORK VALUES ('NW0000000001', 'Operacao A', 'PEP000000001', 'Network Alpha', '7000', 'U001', 'João Silva', ' ', 'A', 'A', '2024-04-01');
INSERT INTO ZEXT_NETWORK VALUES ('NW0000000002', 'Operacao B', 'PEP000000002', 'Network Beta', '7020', 'U002', 'Maria Souza', 'X', 'B', 'B', '2024-04-01');
INSERT INTO ZEXT_NETWORK VALUES ('NW0000000003', 'Operacao C', 'PEP000000003', 'Network Gamma', '7060', 'U003', 'Carlos Lima', ' ', 'A', 'A', '2024-04-01');
INSERT INTO ZEXT_NETWORK VALUES ('NW0000000004', 'Operacao D', 'PEP000000004', 'Network Delta', '7100', 'U004', 'Ana Pereira', 'X', 'B', 'B', '2024-04-01');
INSERT INTO ZEXT_NETWORK VALUES ('NW0000000005', 'Operacao E', 'PEP000000005', 'Network Epsilon', '7150', 'U005', 'Paulo Santos', ' ', 'A', 'A', '2024-04-01');

```

### 3.11. ZEXT_PARAMETROS

**Finalidade:** Armazenar parâmetros dinâmicos para a execução do extrator.

**Campos:**

- `PARAM_ID (CHAR 10) – Chave primária`
- `DESCRICAO (VARCHAR 50)`
- `VALOR (VARCHAR 20)`

**Valores para cadastro:**

```sql
INSERT INTO ZEXT_PARAMETROS VALUES ('PAR001', 'Data Extração', '2024-05-01');
INSERT INTO ZEXT_PARAMETROS VALUES ('PAR002', 'Plano Contas', '1000');
INSERT INTO ZEXT_PARAMETROS VALUES ('PAR003', 'Diretorio', '\\SAPIDES\\sapmnt\\trans');
INSERT INTO ZEXT_PARAMETROS VALUES ('PAR004', 'Formato Arquivo', 'TXT');
INSERT INTO ZEXT_PARAMETROS VALUES ('PAR005', 'Formato PDF', 'PDF');

```

### 3.12. ZEXT_CONSTANTES

**Finalidade:** Armazenar constantes utilizadas no processamento.

**Campos:**

- `CONSTANTE_ID (CHAR 10) – Chave primária`
- `DESCRICAO (VARCHAR 50)`
- `VALOR (VARCHAR 20)`

**Valores para cadastro:**

```sql
INSERT INTO ZEXT_CONSTANTES VALUES ('CON001', 'FILIAL', '7000,7020,7060');
INSERT INTO ZEXT_CONSTANTES VALUES ('CON002', 'OBJ_CONTA', 'SACH');
INSERT INTO ZEXT_CONSTANTES VALUES ('CON003', 'OBJ_CCUSTO', 'KOSTL');
INSERT INTO ZEXT_CONSTANTES VALUES ('CON004', 'OBJ_CLUCRO', 'PRCTR');
INSERT INTO ZEXT_CONSTANTES VALUES ('CON005', 'CAT_ORDER', '01,02,03');

```

### 3.13. ZEXT_LOG

**Finalidade:** Registrar os eventos e erros ocorridos durante o processo de extração.

**Campos:**

- `LOG_ID (NUMC 10) – Chave primária`
- `DATA_EXECUCAO (DATE)`
- `TIPO_REGISTRO (VARCHAR 20) – Ex.: “Erro”, “Aviso”, “Info”`
- `MENSAGEM (VARCHAR 200)`
- `STATUS (CHAR 1) – Indicador (ex.: ‘E’ para erro, ‘W’ para aviso, ‘S’ para sucesso)`

**Valores para cadastro:**

```sql
INSERT INTO ZEXT_LOG VALUES ('0000000001', '2024-05-01', 'Erro', 'Erro ao validar parâmetros', 'E');
INSERT INTO ZEXT_LOG VALUES ('0000000002', '2024-05-01', 'Aviso', 'Registro duplicado detectado', 'W');
INSERT INTO ZEXT_LOG VALUES ('0000000003', '2024-05-01', 'Info', 'Extração iniciada com sucesso', 'S');
INSERT INTO ZEXT_LOG VALUES ('0000000004', '2024-05-01', 'Erro', 'Falha ao gerar arquivo PDF', 'E');
INSERT INTO ZEXT_LOG VALUES ('0000000005', '2024-05-01', 'Info', 'Extração concluída com sucesso', 'S');

```

---

## 4. Processamento e Geração dos Arquivos

### Leitura e Validação

O programa ABAP realizará a leitura dos dados das tabelas customizadas, aplicando validações para garantir que os campos obrigatórios estejam preenchidos. Caso algum dado crítico esteja ausente, o erro será registrado na tabela `ZEXT_LOG` e o processamento será interrompido para o respectivo objeto.

### Montagem dos Arquivos

Para cada área (ex.: EMPRESA, SOCIEDADE, DIVISÃO, etc.), os dados serão extraídos e organizados conforme o layout definido:

- Arquivos `.txt` com os nomes dos campos no cabeçalho e registros separados por `|`.
- Os mesmos dados serão convertidos para **PDF**, mantendo uma formatação amigável para impressão.

### Agendamento

A execução do extrator será agendada (**job diário**), considerando os registros criados ou alterados na data de interesse.

---

## 5. Tratamento de Erros

Toda inconsistência ou exceção será registrada na tabela `ZEXT_LOG`, possibilitando a rastreabilidade e a posterior análise para correção de falhas.

---

## 6. Conclusão

Com a implementação das tabelas customizadas (**ZEXT\_\***) e a inclusão de cadastros iniciais para cada área, o novo projeto elimina a dependência das tabelas padrão do SAP. Essa abordagem garante maior **flexibilidade, controle dos dados e facilidade para futuras manutenções ou alterações**.

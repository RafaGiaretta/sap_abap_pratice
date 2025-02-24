# Sistema de Gerenciamento de Tarefas

## Objetivo
Criar um sistema simples que permita a realização das operações CRUD (Criar, Ler, Atualizar e Excluir) para gerenciar tarefas ou atividades. Esse projeto ajudará a consolidar os conhecimentos iniciais de ABAP e servirá como base para desenvolver funcionalidades mais avançadas no futuro.

## Funcionalidades Principais
### Cadastro de Tarefas
- Criação de uma tarefa informando dados como título, descrição, data de criação, data de vencimento, status e prioridade.

### Consulta de Tarefas
- Exibição de um relatório com as tarefas cadastradas.
- Implementação de filtros (por status, data ou prioridade) usando seleção de tela.

### Atualização e Exclusão
- Possibilidade de atualizar os dados de uma tarefa já cadastrada.
- Opção para excluir tarefas que não são mais necessárias.

### Exibição de Dados com ALV (opcional)
- Se você já estudou ou tiver interesse, utilize a funcionalidade ALV para melhorar a visualização dos dados.

## Estrutura do Projeto
### 1. Modelagem de Dados
#### Tabela Customizada
Crie uma tabela no Data Dictionary com os seguintes campos, por exemplo:
- ID_TAREFA (chave primária)
- TITULO
- DESCRICAO
- DATA_CRIACAO
- DATA_VENCIMENTO
- STATUS (Ex: "Pendente", "Em Andamento", "Concluída")
- PRIORIDADE (Ex: "Alta", "Média", "Baixa")

### 2. Desenvolvimento do Programa ABAP
#### Seleção de Tela (Selection Screen)
Crie uma tela para entrada de dados e filtros. Utilize comandos como PARAMETERS e SELECT-OPTIONS.

#### Lógica do Programa
- **Inserção**: Valide os dados e insira um novo registro na tabela.
- **Consulta**: Use comandos de seleção (como SELECT ... FROM ...) para buscar registros e mostrá-los.
- **Atualização**: Implemente a lógica para alterar dados existentes, solicitando ao usuário o ID da tarefa.
- **Exclusão**: Permita a remoção de registros com base em critérios definidos.

#### Exibição dos Dados
Inicialmente, você pode utilizar comandos simples como WRITE para exibir os dados. Se optar por ALV, explore as classes e funções (como CL_GUI_ALV_GRID ou funções como REUSE_ALV_GRID_DISPLAY) para uma apresentação mais profissional.

### 3. Testes e Validação
- Teste cada funcionalidade individualmente:
  - Verifique a criação de tarefas com dados válidos e inválidos.
  - Teste os filtros na consulta para assegurar que os resultados estão corretos.
  - Realize atualizações e exclusões e confirme que os dados são manipulados conforme o esperado.
- Adicione mensagens de erro e confirmação para orientar o usuário durante as operações.

## Pontos de Aprendizado e Expansão
### Consolidação dos Conceitos Básicos
Este projeto reúne a criação de tabelas, manipulação de dados, estruturas de controle e interação via seleção de tela.

### Utilização de ALV
Se você ainda não explorou, a implementação do ALV será um ótimo desafio para melhorar a apresentação dos dados e aprender sobre a interface do usuário no SAP.

### Validação e Tratamento de Erros
Aprenda a validar as entradas do usuário e tratar possíveis exceções, melhorando a robust

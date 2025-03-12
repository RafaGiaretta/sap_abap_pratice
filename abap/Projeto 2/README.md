# Extração de Dados Mestres para o Portal Nota de Débito

## Visão Geral
Este repositório contém o código-fonte de um programa responsável pela extração de dados mestres para o portal Nota de Débito. Os dados devem ser filtrados conforme a opção selecionada e podem ser salvos localmente ou em um servidor.


<img src="https://i.ibb.co/whh2VNyz/image.png">

## Estrutura do Repositório
O repositório é composto pelos seguintes arquivos principais:

- **include_TOP**: Contém as variáveis utilizadas no programa.
- **include_SEL**: Contém a configuração da tela de seleção.
- **include_f01**: Contém os forms dos PERFORM do código.
- **Main**: Contém o código principal do programa.

## Instruções para Configuração
Para garantir o funcionamento correto do programa, siga as etapas abaixo para inserir os valores corretamente em cada arquivo include:

1. **include_TOP**
   - Defina as variáveis globais necessárias para a execução do programa.
   - Exemplo: `DATA: it_parametros TYPE TABLE OF ty_parametros, " Tabela interna de parametros
                     wa_parametros TYPE ty_parametros. " Work area de parametros`

2. **include_SEL**
   - Configure a tela de seleção de acordo com os parâmetros desejados.
   - Exemplo: `SELECTION-SCREEN BEGIN OF BLOCK b1 WITH FRAME TITLE TEXT-001.`

3. **include_f01**
   - Defina os formulários e códigos PERFORM necessários.
   - Exemplo:
     ```
     FORM buscar_cpnj 
       " Lógica para extração dos dados
     ENDFORM.
     ```

4. **Main**
   - Certifique-se de incluir os arquivos corretamente utilizando `INCLUDE`.
   - Exemplo:
     ```
     INCLUDE include_TOP.
     INCLUDE include_SEL.
     INCLUDE include_f01.
     ```

## Considerações Finais
Este programa foi desenvolvido para facilitar a extração de dados mestres para o portal Nota de Débito. Caso necessite de ajustes ou novas funcionalidades, modifique os arquivos de include conforme as necessidades do projeto.


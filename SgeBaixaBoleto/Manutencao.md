# Manutenção do SgeBaixaBoleto

## Log de Erros

- Diante de qualquer erro, é ideal verificar o log de erros localizado na pasta Sistemas/Sge/SgeBaixaBoleto/Log
- Dentro da pasta contém os arquivos de log referente a data, salvo no padrão ddMMyy
- Por exemplo: 26/07/2024 -> O nome do arquivo será Log260724
- As linhas no arquivo de log seguirão um padrão de **Data e Hora -> Acontecimento**
- Exemplo: **29/07/2024 15:46:12 -> Iniciando envio de baixa Itau - Titulo 109552047017**

## Identificador

- O idenficador utilizado no log é o nosso número que é gravado no SGE

## Exemplo de erro

- Ao ocorrer um erro será gravado a linha com o retorno da API
- Como no exemplo abaixo, um título que não existe:
- Exemplo de retorno do Itau:
    - **26/08/24 12:40:34 -> Falha ao baixar título 109552047017 - Erro: Campo: COD-RET | Mensagem: Título não encontrado | Valor:  |**
- Exemplo de retorno do Santander: 
    - **26/08/24 12:40:34 -> Falha ao baixar título 0001552048010 - Erro: Código: 4 | Campo:  | Mensagem: Nosso numero inexistente |**

- Na ocorrência de erros, entrar em contato com o suporte da Sge e informar os logs para a equipe analisar as possíveis causas.


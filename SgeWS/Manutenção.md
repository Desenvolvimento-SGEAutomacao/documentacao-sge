# Suporte e manutenção do Boletopix

## Log de Erros

- Diante de qualquer erro, é ideal verificar o log de erros localizado na pasta Sistemas/Sge/SgeWS/LogGeral
- Dentro da pasta contém os arquivos de log referente a data, salvo no padrão ddMMyy
- Por exemplo: 26/07/2024 -> O nome do arquivo será Log260724
- As linhas no arquivo de log seguirão um padrão de **[NomeDoServiço] [Data e Hora] -> Acontecimento**
- Exemplo: **[SgeWS.BoletoPix] [29/07/2024 15:46:12] -> Iniciando processamento do título 015753149990124N**

## Identificador
- No inicio de cada requisição existirá uma linha com um identificador do titulo informando que a requisição iniciou
- Exemplo: **Iniciando processamento do título 015753149990124N**
- Entendendo o identificador:
- 8 primeiros dígitos se referem ao número do pedido no Sge, no exemplo: 01575314
- Os próximos 3 dígitos se referem a loja em que o título foi emitido, no exemplo: 999
- Os próximos 2 dígitos se referem ao número da parcela, no exemplo: 01
- Os próximos 2 dígitos se referem aos dois ultimos dígitos do ano de emissão do titulo, no exemplo: 24
- E o último dígito, se refere ao tipo do título, no exemplo: N

## Erro ao registrar o boleto

- Sempre que ocorrer um erro ao registrar o boleto, a mensagem exibida será: 
- **"Erro ao registrar o boleto do titulo 12334567 -> Detalhes do erro"**
- **ATENÇÃO: Quando ocorrer algum erro o boleto NÃO será registrado, e o relatório não será carregado, será apresentado uma tela em branco como na imagem abaixo**

    ![alt text](Imagens/RelatorioEmBranco.png)

## Título não encontrado no contas a receber

- Esse título não está sendo encontrado na tabela de contas à receber (TB_DUPR)
- **IdTitulo - Erro - Título não encontrado no contas a receber**

    ![alt text](Imagens/ErroAoEncontrarTituloNaDupr.png)

## Conta corrente não encontrada

- A conta corrente ligada a forma de pagamento utilizada no pedido, não foi encontrada na tabela de contas corrente (TB_CONTACORENTE)
- **IdTitulo - Erro - Conta corrente não encontrada**

    ![alt text](Imagens/ErroAoEncontrarContaCorrenteNaTbContaCorrente.png)

## Devedor não encontrado

- Os dados do devedor não estão sendo encontrados
- Devedor pode ser cliente ou fornecedor
- Tabela de cliente -> TB_CLIE
- Tabela de fornecedor -> TB_FORN
- **IdTitulo - Erro - Devedor não encontrado**

    ![alt text](Imagens/ErroAoEncontrarDevedorNaTbFornOuTbClie.png)

## Token de acesso inválido

- Ocorre quando o token de acesso requisitado é inválido
- Verificar se o Client Id e o Secret Id estão preenchidos e se estão corretos

### Itau

#### Retorno do Itau quando o ClientId está inválido

- **API - Erro: Falha ao obter informações da aplicação filter failed**

    ![alt text](Imagens/ErroItauClientIdInvalido.png)
    

#### Retorno do Itau quando o SecretId está inválido

- **API - Erro: Falha ao Criar token local filter failed**

    ![alt text](Imagens/ErroItauSecretIdInvalido.png)    


#### Retorno do Itau quando o access token está vazio

- **API - Erro na requisição | Código:  | Mensagem: Extrai TokenInfo filter failed**

    ![alt text](Imagens/ErroItauAccessTokenVazio.png)


#### Retorno do Santander quando o access token é inválido

- **API - Erro na requisição | Código: 401 | Mensagem: Unauthorized | Timestamp: 1722371100086 | TrackingId 4aaab88f-c170-46c8-9f9b-fbd3c0272838**

    ![alt text](Imagens/ErroSantanderAccessTokenVazio.png)

### Santander

#### Retorno do Santander quando ClientId ou SecretId estão inválidos

- **API - Erro: unauthorized_client | Mensagem: Invalid client credentials.**

    ![alt text](Imagens/ErroSantanderCredentialInvalida.png)

#### Retorno do Santander quando o WorkspaceId está inválido

- **API - Erro - WorkspaceId inválido**

    ![alt text](Imagens/ErroSantanderWorkspaceInvalido.png)
    
## Boleto já registrado

- Ocorre quando é feito a tentativa de inclusão de um boleto que já está registrado

#### Retorno do Itau

- **API - Erro Código: 422 | Mensagem: Cobranca Hibrida com id de boleto ou txid ja existente na base de dados.**

    ![alt text](Imagens/ErroSantanderBoletoJaExiste.png)

#### Retorno do Santander

-  **API - Erro: Código: 382 | Campo: nsuCode | Mensagem: Nsu ja existente**

    ![alt text](Imagens/ErroSantanderNsuJaExistente.png)
    

## Campo xpto contem caracteres inválidos

- Ocorre quando algum campo contém caracteres inválidos
- Geralmente esses caracteres inválidos vem do cadastro do cliente

### O que fazer
- Instruir o cliente para que remova TODOS os caracteres especiais do cadastro de clientes no Sge
- Essa regra é comum tanto para APIs de banco quanto para SEFAZ

## Nome do pagador inválido

- Exemplo de retorno do santander quando o campo Nome do Pagador contém caracteres inválidos
- **API - Erro: Código: 901 | Campo: payer.name | Mensagem: O campo payer.name permite somente valores alfa numéricos e &**

    ![alt text](Imagens/ErroSantanderNomePagadorInvalido.png)

## Cep inválido

- Exemplo de retorno do itau quando o Cep do pagador está inválido
- **API - Erro: Campo: dado_boleto.pagador.endereco.numero_CEP | Mensagem: CEP do pagador inválido | Valor: 65078956**

    ![alt text](Imagens/ErroItauCepInvalido.png)

## Caminho do certificado não encontrado

- Caso o certificado informado na tela de conta corrente não seja encontrado, irá ocorrer o seguinte erro:
- **Certificado - Erro: Caminho do certificado inacessível: {Caminho informado na conta corrente}**

    ![alt text](Imagens/ErroCaminhoCertificadoInvalido.png)

## Senha do certificado inválida

- Caso a senha informada na tela de conta corrente esteja incorreta, irá ocorrer o seguinte erro:
- **Certificado - Erro: Senha do certificado incorreta**

    ![alt text](Imagens/ErroSenhaCertificadoInvalida.png)

## Erro de conexão

- Caso ocorra algum problema de conexão durante a requisição, o seguinte erro irá ocorrer:
- **API - Erro Este host não é conhecido. {Url}**

    ![alt text](Imagens/ErroDeConexao.png)
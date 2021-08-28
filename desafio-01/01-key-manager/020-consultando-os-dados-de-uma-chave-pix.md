# Consultando os dados de uma chave Pix

## Necessidades

Precisamos disponibilizar um meio de consultar os dados de uma determinada chave Pix, dessa forma outros serviços e sistemas poderão exibir as informações da chave (nome e CPF do titular, banco, agência etc) para seus usuários ou mesmo para validá-las.
   
## Restrições

Poderemos consultar uma chave Pix de duas maneiras diferentes. Portanto, devemos suportar as seguintes abordagens:

1. Para o nosso sistema KeyManager:
    - **Identificador do cliente** e **Pix ID** devem ser obrigatórios;
    - a chave Pix encontrada deve ser de propriedade do cliente;
    - Caso a chave Pix não esteja devidamente [registrada no BCB](015-registrando-e-excluindo-chaves-pix-no-bcb.md), ela não poderá ter suas informações disponibilizadas abertamente, afinal trata-se de uma chave ainda inválida.
   
2. Para outros microsserviços e sistemas:
    - **Chave Pix** deve ser obrigatória e possuir tamanho máximo de 77 caracteres;
    - No caso de nosso sistema **não possuir** a chave Pix informada, ela deve ser consultada no [sistema Pix do BCB](015-registrando-e-excluindo-chaves-pix-no-bcb.md).

A ideia é que nosso sistema KeyManager consiga consultar chaves por Pix ID para seus usuários enquanto outros sistemas e serviços possam consultar os dados de qualquer chave pela própria chave Pix para validação de dados ou mesmo para exibir informações.

## Resultado Esperado

- Em caso de sucesso, deve-se retornar os dados da chave Pix:
  - Pix ID (opcional - necessário somente para abordagem 1);
  - Identificador do cliente (opcional - necessário somente para abordagem 1);
  - Tipo da chave;
  - Valor da chave;
  - Nome e CPF do titular da conta;
  - Dados da conta vinculada a chave Pix:
    - nome da instituição financeira;
    - agência, número da conta e tipo da conta (Corrente ou Poupança);
  - Data/hora de registro ou criação da chave;

- Em caso de chave não encontrada, deve-se retornar status de erro `NOT_FOUND` com uma mensagem amigável para o usuário final;

- Em caso de erro, deve-se retornar o erro específico e amigável para o usuário final;

## Informações de suporte

- Precisa encontrar o nome de uma instituição (participante) pelo seu ISPB? Basta acessar essa [Relação de participantes do STR - Ambiente de Produção do BCB](https://www.bcb.gov.br/pom/spb/estatistica/port/ASTR003.pdf) e exportá-la clicando no link **Arquivo CSV** do PDF;
- Não lembra como declarar o protobuf para um novo serviço? [Nesse vídeo conversamos um pouco sobre o protobuf](https://www.youtube.com/watch?v=Rd7sLrPKDGM&feature=youtu.be);
- Não lembra como tratar erro e retornar um status `NOT_FOUND`? [Nesse vídeo conversamos sobre tratamento de erros com gRPC](https://www.youtube.com/watch?v=bIuEINzEmKs&feature=youtu.be);

## Como nós implementamos
Quer saber como nós da Zup Edu implementamos esse serviço? [Neste vídeo](https://www.youtube.com/watch?v=SNRyo3Phh7s&feature=youtu.be) você vai ver como foi o passo que seguimos para realizar essa tarefa

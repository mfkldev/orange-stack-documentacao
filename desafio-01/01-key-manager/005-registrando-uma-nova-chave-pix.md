# Registrando uma nova chave Pix

## Necessidades

Nosso usuário precisa registrar (cadastrar) uma nova chave Pix para que ele possa gerar cobranças e efetuar pagamentos de cobranças na nossa plataforma.
   
## Restrições

Para registrar uma chave Pix, precisamos que o usuário informe os seguintes dados:

- **Identificador do cliente** deve ser obrigatório:
   - Código interno do cliente na Instituição Financeira existente no [Sistema ERP do Itaú](http://localhost:9091/api/v1/private/contas/todas);

- **Tipo da chave** deve ser obrigatório, e pode ser:
    - CPF;
    - telefone celular;
    - email;
    - chave aleatória;

- **Valor da chave** deve ser válido e único com tamanho máximo de 77 caracteres:
    - Quando tipo for CPF, deve ser obrigatório e usar formato `^[0-9]{11}$` (por exemplo: `12345678901`);
    - Quando tipo for telefone celular, deve ser obrigatório e usar formato `^\+[1-9][0-9]\d{1,14}$` (por exemplo: `+5585988714077`);
    - Quando tipo for email, deve ser obrigatório e um endereço válido;
    - Quando tipo for chave aleatória, o valor da chave **não** deve ser preenchido pois o mesmo deve ser gerado pelo sistema no [formato UUID](https://en.wikipedia.org/wiki/Universally_unique_identifier);

- **Tipo de conta** associada a chave Pix deve ser obrigatória, e pode ser:
    - Conta Corrente;
    - Conta Poupança;

## Resultado Esperado

- Em caso de sucesso:
   - a chave Pix deve ser registrada e armazenada no sistema;
   - deve-se retornar um ID interno ("Pix ID") para representar a chave Pix criada pelo sistema;

- Em caso de chave já existente, deve-se retornar status de erro `ALREADY_EXISTS` com uma mensagem amigável para o usuário final;

- Em caso de erro, deve-se retornar o erro específico e amigável para o usuário final;

## Informações de suporte

- Os dados do cliente e de sua conta corrente **devem ser obtidos do [Sistema ERP do Itaú](http://localhost:9091/swagger-ui/index.html?configUrl=/v3/api-docs/swagger-config#/)**; 

- Para criar os serviços gRPC é necessário criar um arquivo Protobuf. Tem dúvidas sobre como criar um protobuf? [Esse vídeo pode te ajudar com o passo a passo](https://www.youtube.com/watch?v=Rd7sLrPKDGM&feature=youtu.be)

- Para salvar os dados no banco de dados, vamos precisar criar uma camada de comunicação com o banco de dados. Tem dúvidas sobre como criar essa camada de comunicação com o banco de dados? [Esse vídeo pode te ajudar](https://www.youtube.com/watch?v=pWu2mqaKFEc&feature=youtu.be)

- Para se comunicar com o sistema do Itaú temos que fazer uma requisição HTTP. Quer saber como podemos criar um cliente HTTP com Micronaut? [Esse vídeo pode te ajudar](https://www.youtube.com/watch?v=9nPRHbToxAc&feature=youtu.be)

- Uma boa prática é receber dados como URLs através de configurações dinâmicas. Podemos ler esses dados lá do `application.yaml`.? [Aqui tem um exemplo que mostra como fazer isso]()

- Precisa tratar os diversos tipos de erros e retornar o status apropriado da sua API? Vale a pena assistir esse [vídeo sobre tratamento de erros](https://www.youtube.com/watch?v=bIuEINzEmKs&feature=youtu.be);

- Quer saber o porquê não trafegamos as chaves do PIX abertamente? [Aqui tem uma explicação sobre boas práticas de trafegar dados sensíveis]()

- Precisa validar os dados de entrada de forma declarativa? Aqui discutimos como usar as [anotações da Bean Validation](https://www.youtube.com/watch?v=Vw1uB_8EeX4&feature=youtu.be);
  
- Para cada tipo de chave fazemos uma validação diferente. Quer saber como criar uma validação customizada com Micronaut? [Aqui tem um vídeo que pode te ajudar](https://www.youtube.com/watch?v=UCHFApcJVW0&feature=youtu.be)

## Sugestões de busca de conteúdo

- Precisa trabalhar com REGEX em Kotlin? Com certeza [esse artigo](https://www.baeldung.com/kotlin/regular-expressions) pode te ajudar;

- Quer entender um pouco mais sobre os possíveis status numa API gRPC? [Aqui você pode conhecer cada um deles e entender quando utilizá-los](https://developers.google.com/maps-booking/reference/grpc-api/status_codes)
  
- Como está seu arquivo Protobuf? Lembre-se sempre de definir um [valor default para o tipo `Enum`](https://developers.google.com/protocol-buffers/docs/proto3#enum);

- Precisa converter um objeto do modelo gRPC para um objeto de modelo de domínio? Uma forma elegante de fazer isso em Kotlin é com [Extension Functions](https://medium.com/collabcode/adicionando-extension-functions-no-kotlin-17092afbe0c3);

## Como nós implementamos
Quer saber como nós da Zup Edu implementamos esse serviço? [Neste vídeo](https://www.youtube.com/watch?v=62872eBIMxE&feature=youtu.be) Você vai ver como foi o passo que seguimos para realizar essa tarefa

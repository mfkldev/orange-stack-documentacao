# Testando o Registro de chave Pix

## Necessidades

Nós finalizamos a implementação do endpoint responsável por [registrar uma nova chave Pix](005-registrando-uma-nova-chave-pix.md), mas a entrega ainda não está concluída. Precisamos testar a funcionalidade para garantir que ela funcionará em produção. 

Eu sei, eu sei... você já testou sua aplicação de ponta a ponta, não é mesmo? A verdade é que embora tenhamos feito os testes com a ferramenta [BloomRPC](https://appimage.github.io/BloomRPC/) nós fizemos isso de forma totalmente **manual**. Mas será que foi suficiente?

Testes manuais são ótimos e super válidos no ciclo de desenvolvimento de um software, mas não dá para ignorar que eles são caros. O que estou querendo dizer é que qualquer alteração no código requer que façamos todos os testes novamente, pois somente assim será possível descobrir o impacto das mudanças. Enfim, muito trabalho para um(a) desenvolvedor(a), não é mesmo?

Soma a isso o fato de que testes manuais são repetitivos e feitos por um ser humano, o que maximiza as chances de erros. Por esse motivo, vamos cobrir nosso código com **testes automatizados**, que nada mais são do que um programa que testa outro programa, desse modo sempre que fizermos alguma mudança no código basta rodarmos nossa bateria de testes. Portanto, **testes automatizados fazem parte da entrega** num time que preza pela qualidade de suas entregas.

Ter uma bateria de testes bem escrita e funcionando nos permite ter um ciclo de entrega mais curto e seguro, nos ajuda a encontrar e corrigir erros mais rapidamente; e claro, o desenvolvedor(a) terá mais confiança em modificar ou refatorar código, afinal se ele(a) cometer algum erro, por menor que seja, a bateria de testes vai alertá-lo(a) em questão de segundos.

Vamos escrever nosso primeiro teste?
   
## Restrições

Escrever testes automatizados para o endpoint gRPC de Registro de chave Pix implementado de tal forma que os testes garantem o que foi especificado na atividade.

Para guiá-lo(a) nessa atividade, elencamos algumas restrições e pontos de atenção:

- favoreça a escrita de **testes de unidade** para lógicas de negócio que não fazem integração com serviços externos (banco de dados, APIs REST, mensageria, sistema de arquivos etc);
- favoreça a escrita de **testes de integração** para lógicas de negócio que conversam com serviços externos, como banco de dados, APIs REST etc;
- para tornar o teste mais próximo da produção, nos testes de integração **levante um servidor gRPC embarcado** e consuma os endpoints nos testes de integração;
- lembre-se de **testar os fluxos alternativos**, como cenários de erros do sistema ou entrada de dados inválida pelo usuário/serviço;
- favoreça o uso de um **banco de dados em memória** para facilitar a limpeza dos dados e simplificar o ambiente na sua pipeline de CI/CD;
- favoreça **mocks para chamadas à serviços externos**, como a API REST do Sistema ERP-ITAÚ e do Sistema Pix do BCB;
- fique sempre de olho na **cobertura do seu código**, especialmente nas branches de código, como `if`, `else`, `while`, `for`, `try-catch` etc;

Quer entender por que adotamos as restrições acima? [Assiste a esse vídeo](https://www.youtube.com/watch?v=IMvjNpG6320) para entender os detalhes do porquê acreditamos que esse é um bom caminho.

## Resultado Esperado

O que esperamos ao final dessa atividade e que também consideramos importante:

- ter um percentual de cobertura de no mínimo **90% do código de produção**;
- ter coberto cenários felizes (happy-path) e fluxos alternativos;
- não precisar de instruções especiais para preparar o ambiente ou para rodar sua bateria de testes;
- sua bateria de testes deve rodar tanto na sua IDE quanto via **linha de comando**;
- que outro desenvolvedor(a) do time consiga rodar facilmente a bateria de testes do seu serviço;

## Informações de suporte

- Não sabe como escrever um teste de unidade em Kotlin? Nesse artigo você aprende [como escrever testes com Kotlin e jUnit 5](](https://www.baeldung.com/kotlin/junit-5-kotlin));
- Está tendo dificuldades para escrever seu primeiro teste de integração com `@MicronautTest`? Não seja por isso, a [documentação do Micronaut](https://micronaut-projects.github.io/micronaut-test/latest/guide/#junit5) é nossa melhor amiga nesse momento;
- Não está fácil escrever o primeiro teste para consumir seu endpoint gRPC? A documentação do Micronaut explica [como testar uma API gRPC](https://micronaut-projects.github.io/micronaut-grpc/snapshot/guide/index.html#_testing_the_server);
- Dificuldade para configurar um banco de dados em memória? Nesse artigo você aprende [como configurar o banco H2 na sua aplicação](https://micronaut-projects.github.io/micronaut-sql/latest/guide/#jdbc);
- Está se perguntando como o Micronaut gerencia as transações com o banco de dados durante os testes? Mais uma vez [a documentação](https://micronaut-projects.github.io/micronaut-test/latest/guide/#_transaction_semantics) está aí para nos ajudar;

## Como nós implementamos

- Quer saber como nós da Zup Edu cobrimos com testes nosso serviço gRPC? [Neste vídeo](https://www.youtube.com/watch?v=gmF_C64phRk) você vai ver como ficou a escrita dos **testes de integração** que implementamos;

- Sabia que nós da Zup Edu favorecemos **testes de unidade** para código que não toca sistemas externos? [Nesse vídeo](https://www.youtube.com/watch?v=M3fhh0YaK88) a gente cobriu as lógicas de negócio com testes de unidade;


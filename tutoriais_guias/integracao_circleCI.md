# CircleCI

CircleCI é uma ferramenta de integração contínua. Ao integrá-la ao GitHub, a ferramenta permite que sejam criados testes automatizados a cada tentativa de atualização na branch master. 

Antes, vamos entender mais sobre a integração contínua. De acordo com a documentação do circleCI:

“A integração contínua é uma prática que incentiva os desenvolvedores a integrar o seu código à branch master de um repositório compartilhado frequentemente. Em vez de criar recursos isoladamente e integrá-los no final de um ciclo de desenvolvimento, o código é integrado ao repositório compartilhado por cada desenvolvedor várias vezes ao longo do dia.”

Basicamente, é um processo que tem como objetivo entregas contínuas sem esquecer da qualidade do código. 

Certo, agora vamos configurar o nosso projeto...

## Como integrar ao GitHub

Acesse o site do CircleCI - `https://circleci.com/`

faça o login na plataforma com o seu GitHub e permita o acesso da sua conta. 

Na tela apresentada, clique em "Add Project" conforme ilustra a figura abaixo:

![img1](./imagens_tutoriais/circleCI/imgci1.png) 

Na tela de Add Projects, no canto superior esquerdo, escolha o seu perfil pessoal ou alguma organização. Então escolha um projeto e clique em "Set Up Project"

![img2](./imagens_tutoriais/circleCI/imgci2.png) 

Na tela de Set Up, selecione a linguagem (Gradle (Java), por exemplo). Na pasta do projeto, crie uma pasta chamada ".circleci" e, nela crie um arquivo chamado "config.yml". Neste arquivo, insera o seguinte código.

```
# Java Gradle CircleCI 2.0 configuration file
#
# Check https://circleci.com/docs/2.0/language-java/ for more details
#
version: 2
jobs:
  build:
    docker:
      # specify the version you desire here
      - image: circleci/openjdk:8-jdk
      
      # Specify service dependencies here if necessary
      # CircleCI maintains a library of pre-built images
      # documented at https://circleci.com/docs/2.0/circleci-images/
      # - image: circleci/postgres:9.4

    working_directory: ~/repo

    environment:
      # Customize the JVM maximum heap limit
      JVM_OPTS: -Xmx3200m
      TERM: dumb
    
    steps:
      - checkout

      # Download and cache dependencies
      - restore_cache:
          keys:
          - v1-dependencies-{{ checksum "build.gradle" }}
          # fallback to using the latest cache if no exact match is found
          - v1-dependencies-

      - run: gradle dependencies

      - save_cache:
          paths:
            - ~/.gradle
          key: v1-dependencies-{{ checksum "build.gradle" }}
        
      # run tests!
      - run: gradle test
```
Após, retorne para a página de Set Up e, na área "Next Steps", clique em "Start building", conforme ilustra a figura a baixo:

![img3](./imagens_tutoriais/circleCI/imgci3.png) 

Agora já temos o circleCI funcionando.  A cada push ele testará o código para verificar se há erros e, nos commits e pull requests, será informado se as modificações estão corretas ou se a ferramenta identificou erros. Um exemplo de verificação do circleCI é ilutrado na figura abaixo:

![img4](./imagens_tutoriais/circleCI/imgci4.png) 

**Legenda**
Vermelho: ocorreu algum erro<br>
Amarelo: CircleCI está processando o código<br>
Verde: não há erros!!!!!

Por Bruno Miguel e Vinicius Oliveira





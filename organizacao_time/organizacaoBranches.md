# Organização das branches

Com o objetivo de manter o histórico da alterações e garantir que funcionalidades não validadas sejam disponibilizadas para os usuários, o repositório do projeto será dividido acordo com as seguintes branches

* **master**: Branch na qual está armazenado o código-fonte do serviço em produção. Todas as alterações nesta branch são inseridas somente pelo SRE da equipe.
* **release**: Branch para integração das funcionalidades desenvolvidas. Após testes realizados nesta branch, o SRE enviar o código-fonte para a branch **master**.
* **feature**: Branch utilizada para commitar as funcionalidades desenvolvidas. 
* **hotfix**: Branch utilizada para commitar correções de bugs no sistema.  
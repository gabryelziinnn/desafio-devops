Minha primeira alteração foi no docker-compose, na qual é necessario para que todas os containers se comuniquem, uma rede em bridge.
Decidi alterar do docker compose, para um cenário no kubernetes para apresentação dos meus conhecimentos para a empresa, e também para que o mesmo seja o mais resiliente possivel.
Kubernetes é o sistema de orquestração de containers mais utilizado no mercado, e para o mundo DevOps ele é indispensável.

Utilizei como base de cluster o RKE (rancher kubernetes engine), como ingress o traefik, e como storage o Longhorn, e para administração do cluster kubernetes é indispensável o uso do RANCHER.

No app-nodejs.yaml inseri o serviço na qual ele está atuando como clusterip para maior segurança( e como utilizarei o ingress para exposição poderá continuar em clusterIP), dentro do mesmo está apontando para a imagem do desafio na qual subi para o dockerhub, ainda sem alterações. Inseri um readiness probe para funcionamento correto do HPA, e também limites e request para os PODs, para que os mesmos atuem em QOs Guaranteed.

No HPA-nodejs.yaml, foi inserido o HPA que atuará com o deployment do app-nodejs.yaml, como métrica para que o mesmo funcione será utilizado 70% do uso da CPU do pod.

Para acesso a aplicação será utilizado o ingress.yaml, para que o mesmo funcione bastaria utilizar o traefik como ingress. Recomendo também para ambiente de produção que seja utilizado um LoadBalancer da AWS, com DNS apontando para wildcards das nossas aplicações, e o ingress atuaria para fazer a exposição dos serviços.

O arquivo mysql.yaml será o nosso banco de dados. Escolhi fazer o uso do Statefulset, pois é a prática recomendada para bancos de dados em kubernetes (e para um possível uso do HPA) para este banco. Para os dados sensíveis foram utilizados secrets (ainda que não estejam estabelecidos os RBACs, por se tratar de um ambiente que não está em produção). A imagem utilizada foi a proposta do curso, porem com a alteração de utilizar o mysql mais atual. Foi inserida persistência de dados para o banco, com tamanho de 10Gib, na storage do longhorn.

Foi inserido um namespace.yaml, para maior organização no cluster da aplicação. O arquivo secret-mysql.yaml contém os dados sensíveis do banco.

O arquivo storage-longhorn.yaml, contém o PersistentVolumeClaim requisitado pelo Statefulset do banco de dados.

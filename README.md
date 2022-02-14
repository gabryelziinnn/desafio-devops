Minha primeira alteração foi no docker-compose, na qual é necessario para que todas os containers se comuniquem, uma rede em bridge.
Decidi alterar do docker compose, para um cenário no kubernetes para apresentação dos meus conhecimentos para a empresa, e também para que o mesmo seja o mais resiliente possivel.
Kubernetes é o sistema de orquestração de containers mais utilizado no mercado, e para o mundo DevOps ele é indispensável.
Utilizei como base de cluster o RKE (rancher kubernetes engine), como ingress o traefik, e como storage o Longhorn, e para administração do cluster kubernetes é indispensável o uso do RANCHER.
No app-nodejs.yaml inseri o serviço na qual ele está atuando como clusterip para maior segurança( e como utilizarei o ingress para exposição poderá continuar em clusterIP), dentro do mesmo está apontando para a imagem do desafio na qual subi para o dockerhub, ainda sem alterações. Inseri um readiness probe para funcionamento do HPA.

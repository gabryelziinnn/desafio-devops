Minha primeira alteração foi no docker-compose, na qual é necessario para que todas os containers se comuniquem, uma rede em bridge.
Decidi alterar do docker compose, para um cenário no kubernetes para apresentação dos meus conhecimentos para a empresa, e também para que o mesmo seja o mais resiliente possivel.
Kubernetes é o sistema de orquestração de containers mais utilizado no mercado, e para o mundo DevOps ele é indispensável.
Utilizei como base de cluster o RKE (rancher kubernetes engine), como ingress o traefik, e como storage o Longhorn.

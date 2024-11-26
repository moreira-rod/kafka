# Projeto kafka em Container Docker.

Um projeto simples kafka para enviar e receber mensagem. Segui a imagem kafka-cluster da confluentinc no link abaixo:

https://github.com/confluentinc/cp-docker-images/tree/5.3.3-post/examples

## Dockerfile para criação da imagem customizada.

docker-compose up -d

## Acessando o container docker.

docker exec -it kafka-kafka-1-1 bash

## Criando um topico kafka.

kafka-topics --create --bootstrap-server localhost:29092 --replication-factor 3 --partitions 3 --topic meutopico

esse é um topico com 3 replicações em 3 partições no server que esta descrito no docker-compose.yml

## Listando os topicos do servidor.

kafka-topics --list --bootstrap-server localhost:29092

## Conectando o topico ao broker atraves do producer.

kafka-console-producer --broker-list localhost:29092 --topic meutopico

## Lendo em outra janela o que foi enviado para o topico atraves do consumer.

kafka-console-consumer --bootstrap-server localhost:29092 --topic meutopico

acresentando o "--from-beginning" ele busca desde o começo tudo que foi enviado, e acresentando o "--group a" logo após o comando acima tudo que esta sendo lido vai para o grupo a. executando 3 vezes esse comando em janelas distintas conseguimos ler as 3 partiçoes do kafka separadamente.

## Lendo as configurações do topico kafka.

kafka-topics --describe --bootstrap-server localhost:29092 --topic meutopico

## Comando para vermos a anatomia do grupo.

kafka-consumer-groups --group a --bootstrap-server localhost:29092 --describe
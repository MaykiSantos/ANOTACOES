# usando repositório LAB - LIAA
para utilizar o repositório local é necessário criar/editar o aquivo /etc/docker/daemon.json e adicionar a seguinte linha:

```
{
    "insecure-registries" : [ "XXX.XXX.XXX.XXX:PPPP" ]
}
```
Onde XXX.XXX.XXX.XXX deve ser substituido pelo IP de comunição com o DockerRegistry e o PPPP sua porta. No caso do LAB-LIAA é utilizado 10.131.14.77:30002.
e reiniciando o servido do docker logo em seguida.

```
sudo service docker reload
```

Caso o procedimento não seja realizado, um erro será exibido ao tentar manimular imanges no DockerRegistry.

´´´
Error response from daemon: Get "https://10.131.14.77:30001/v2/": http: server gave HTTP response to HTTPS client
´´´

### Realizando login

```
docker login 10.131.14.77:30002 -u liaa-rep-local
```
### Realizando logout

```
docker logout 10.131.14.77:30002
```
### Editando nome de imagens

```
docker tag minha-imagem-teste:0.3 10.131.14.77:30001/nome-minha-imagem:0.1
```
### Enviando imagens para oa servidor local

```
docker push 10.131.14.77:30001/nome-minha-imagem:0.1
```


# anotações

#### Exibe o hitorico 
```
cat ~/.docker/config.json
```
#### exibe as informações de configuração do docker
```
docker info
```

#### adicionar secret do registry no kubernetes
```
kubectl create secret docker-registry docker-registry-local \
--docker-server=http://10.131.14.77:30002/v2/ \
--docker-username=meu_usuario \
--docker-password=minha_senha
```

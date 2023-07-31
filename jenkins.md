## instalação do jenkins

Instale as dependencias:
* java JDK 17
* docker engine
* git

Adicione o repositorio no ubuntu e instale a aplicação:
```
curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins
```
Habilite o serviço do jenkins
```
sudo systemctl enable jenkins
```
e inicialize o serviço
```
sudo systemctl start jenkins
```

Caso seja necessario, verifique o status do serviço:
```
sudo systemctl status jenkins
```

## Adicione o usuário do jenkins ao grupo do docker
```
sudo usermod -aG docker jenkins
reboot
```

## Adicione a chave ssh do github

crie a chave ssh no servidor que está executando o jenkins conforme a documentação do [github](https://docs.github.com/pt/authentication/connecting-to-github-with-ssh). adicione a chave privada do git ao jenkins, seguindo os paso a baixo.

1. Exiba sua chave privada dogitando o comando `cat ~/.ssh/nome_sua_chave`
2. Copie o conteudo da sua chave
3. Já no painel do jankins vá para _Gerenciar Jenkins > Credentials > (global) > add credentials_
4. preencha o formulário, conforme a baixo e clique em "Create"
  ![image](https://github.com/MaykiSantos/ANOTACOES/assets/58126683/5c5cba50-5630-44b7-ab19-a0e38679fafb)

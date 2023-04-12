# Primeiros passos

## Instalar o Docker conforme o seu sistema operacional:
### Windows
1. Download em : https://docs.docker.com/desktop/install/windows-install/
2. Iniciar instalação. Quando solicitado escolher entre WSL ou Hyper V, optar por WSL (Windows SubSystem for Linux)
3. Abrir terminal do windows e executar comando:  `wsl --upgrade`

## Criar projeto
1. Criar nova pasta
2. Criar arquivo(s) do projeto. Ex.: main.py (projeto em Python)
3. criar arquivo Dockerfile

## Criar uma imagem do Docker
Quando seu código estiver pronto e o Dockerfile estiver escrito, tudo o que você precisa fazer é criar sua imagem para que contenha sua aplicação:

`docker build -t python-test .`

A opção '-t' permite que você defina o nome de sua imagem. Em nosso caso, escolhemos 'python-test', mas você pode usar o nome que quiser.

O ponto "." no final do comando indica o PATH em que se encontra o arquivo DockerFile, neste caso, na raiz do projeto.

## Executar uma imagem do Docker / Containers
Quando a imagem for criada, seu código estará pronto para ser lançado. E é a partir destas imagens que podemos criar o que chamamos de *CONTAINERS*. Que são as imagens *em execução*.

Sempre que formos criar um container utilizaremos a sintaxe:

`docker run [image_name]` onde,

`[image_name] = Nome da imagem que queremos que ele utilize`

## Comandos Básicos

|Comando | Descrição |
|--------| --------- |
| docker build -t [image_name] . | Cria uma imagem a partir de um arquivo DockerFile |
| docker images | Lista as imagens existentes em sua máquina local |
|||
| docker run [image_name] | Executa uma imagem, criando um Container. Faz o download da mesma caso não exista no disco local |
| docker run -it [image_name] | Executa uma imagem e vai direto para o terminal da mesma (caso seja imagens de um SO. Ex: Ubuntu) |
| docker ps	| Exibe todos os containers em execução |
| docker ps -a | Exibe todos os containers criados, inclusive os encerrados |
|||
| docker rmi {nome da imagem} | Remove imagens |
| docker rm {ID do container} | Remove containers |

## Docker Composer / Orquestrador de Containers

Docker Compose é o orquestrador de containers da Docker. Através dele você pode trabalhar com vários containers de forma simultânea e integrada. A "regência" desta orquestra se dá através do arquivo chamado docker-compose, semelhante ao Dockerfile, escrito em YAML.

Um Exemplo: Uma Aplicação/container que se interliga a outro que possui somente o banco de dados, volumes etc.

Em resumo, utilizando o Docker Compose, em vez de o administrador executar o docker run na mão para cada container e subir os serviços separados, linkando os containers das aplicações manualmente, temos um único arquivo que vai fazer essa orquestração e vai subir os serviços/containers de uma só vez. Isso diminui a responsabilidade do Sysadmin ou do desenvolvedor de ter que gerenciar o deploy e se preocupar em rodar todos esses comandos para ter a sua aplicação rodando com todas as suas dependências.

Para utilizar o docker-compose você precisa ter em mente que será necessário seguir essas três etapas:

* Definir o ambiente necessário para sua aplicação utilizando um Dockerfile (que pode ser reproduzido em qualquer lugar que tenha Docker instalado);
* Definir no arquivo .yml  quais serviços são essenciais para sua aplicação e a relação entre elas.
* Executar o comando docker-compose up para que seu ambiente seja criado e configurado.
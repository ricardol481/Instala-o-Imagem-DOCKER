# Instala-o-Imagem-DOCKER
<body>
Instalando uma imagem DOCKER com serviço apache

Tutorial, para instalação e inicialização.

Droplet do Ubuntu 16.04 64-bits
Usuário não-root com privilégios sudo (Initial Setup Guide for Ubuntu 16.04 explica como configurar).
Nota: O Docker requer uma versão de 64 bits do Ubuntu, bem como uma versão de kernel maior ou igual a 3.10. O Droplet padrão de 64 bits do Ubuntu 16.04 atende a esses requisitos.

Todos os comandos nesse tutorial devem ser executados como usuário não-root. Se o acesso de root for requerido para o comando, ele será precedido pelo sudo. Initial Setup Guide for Ubuntu 16.04 explica como adicionar usuários e dar a eles o acesso ao sudo.

Passo 1 — Instalando o Docker

O pacote de instalação do Docker disponível no repositório oficial do Ubuntu 16.04 pode não ser a última versão. Para obter a maior e mais recente versão, instale o Docker a partir do repositório oficial do Docker. Essa seção lhe mostra como fazer isso.

Mas primeiro, vamos atualizar o banco de dados de pacotes:

sudo apt-get update
Agora, vamos instalar o Docker. Adicione ao sistema a chave GPG oficial do repositório do Docker:

sudo apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
Adicione o repositório do Docker às fontes do APT:

sudo apt-add-repository 'deb https://apt.dockerproject.org/repo ubuntu-xenial main'
Atualize o banco de dados de pacotes com os pacotes do Docker a partir do novo repositório adicionado:

sudo apt-get update
Certifique-se de que você está instalando a partir do repositório do Docker em vez do repositório padrão do Ubuntu 16.04:

apt-cache policy docker-engine
Você deverá ver uma saída semelhante à seguinte: Output of apt-cache policy docker-engine

docker-engine:
  Installed: (none)
  Candidate: 1.11.1-0~xenial
  Version table:
     1.11.1-0~xenial 500
        500 https://apt.dockerproject.org/repo ubuntu-xenial/main amd64 Packages
     1.11.0-0~xenial 500
        500 https://apt.dockerproject.org/repo ubuntu-xenial/main amd64 Packages
Observe que o docker-engine não está instalado, mas o candidato para instalação é do repositório Docker do Ubuntu 16.04. O número da versão do docker-engine pode ser diferente.

Finalmente, instale o Docker:

sudo apt-get install -y docker-engine
O Docker agora será instalado, o daemon iniciado, e o processo habilitado para iniciar no boot. Verifique que ele está executando:

sudo service docker status
A saída deve ser similar ao seguinte, mostrando que o serviço está ativo e em execução:

[secondary_label Output]
   docker.service - Docker Application Container Engine
   Loaded: loaded (/lib/systemd/system/docker.service; enabled; vendor preset: enabled)
   Active: active (running) since Sun 2016-05-01 06:53:52 CDT; 1 weeks 3 days ago
     Docs: https://docs.docker.com
 Main PID: 749 (docker)
Próximo passo é subir a imagem Docker com Apache

Imagem docker criada para servir como base de estudos ao servidor web apache.

Utilizar: A maquina chicocx do professor onde está a imagem postada.

  sudo docker run -dit --name apache-app --publish=9081:80 chicocx/docker-apache
Para configurar externamente à imagem docker o local onde o apache salvará o site, utilize:

  sudo docker run -dit --name apache-app --publish=9081:80 -v "$PWD":/usr/local/apache2/htdocs/ chicocx/docker-apache
Entrar na máquina/imagem

docker exec -it [aqui é o nome do root da maquina imagem] bash 
sair sem encerrar a máquina:

ctrl p q
Lista o status dos containers

docker ps -a
Exclui os containers que estão parados

docker rm $(docker ps -q -f status=exited)
Lista as imagens baixadas
</body>

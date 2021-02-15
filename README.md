![image20](https://user-images.githubusercontent.com/27836893/90990444-da9fdc00-e577-11ea-89eb-71590afb63c2.png)

<h1 align="center">
 Implantação de Servidor | Amazon AWS - EC2 
</h1>

### O que é o Amazon EC2

O Amazon Elastic Compute Cloud (Amazon EC2) oferece uma capacidade de computação dimensionável na nuvem da Amazon Web Services (AWS). O uso do Amazon EC2 elimina a necessidade de investir em hardware inicialmente, portanto, você pode desenvolver e implantar aplicativos com mais rapidez. Você pode usar o Amazon EC2 para executar o número de servidores virtuais que precisar, configurar a segurança e a rede, e gerenciar o armazenamento. O Amazon EC2 também permite a expansão ou a redução para gerenciar as alterações de requisitos ou picos de popularidade, reduzindo, assim, a sua necessidade de prever o tráfego do servidor.

### Recursos do Amazon EC2

O Amazon EC2 fornece os seguintes recursos:

* Ambientes de computação virtual, conhecidos como instâncias

* Os modelos pré-configurados para suas instâncias, conhecidos como Imagens de máquina da Amazon (AMIs), que empacotam os bits de que você precisa para seu servidor (incluindo o sistema operacional e software adicional)

* Várias configurações de capacidade de CPU, memória, armazenamento e redes para suas instâncias, conhecidas como tipos de instância

* Informações seguras de login para suas instâncias usando pares de chave (a AWS armazena a chave pública e você armazena a chave privada em um lugar seguro)

* Volumes de armazenamento para dados temporários que são excluídos quando você interrompe ou encerra sua instância, conhecidos como volumes de armazenamento de instâncias

* Volumes de armazenamento persistentes para seus dados usando o Amazon Elastic Block Store (Amazon EBS), conhecidos como volumes do Amazon EBS

* Vários locais físicos para seus recursos, como instâncias e volumes do Amazon EBS, conhecidos como regiões e zonas de disponibilidade

* Um firewall que permite especificar os protocolos, portas e intervalos de IPs de origem que podem acessar suas instâncias usando grupos de segurança

* Os endereços IPv4 estáticos para computação em nuvem dinâmica, conhecidos como endereços IP elásticos

* Metadados, conhecidos como tags, que você pode criar e atribuir aos recursos do Amazon EC2

* Redes virtuais isoladas logicamente do restante da Nuvem AWS que você pode criar e conectar à sua própria rede, conhecidas como nuvens privadas virtuais (VPCs)

<hr />
<hr />

### Criando primeira VM em Nuvem - EC2
* Realize o cadastro e/ou login na Amazon AWS
* Navegue até o Console de gerenciamento da AWS
* Localize os serviços da AWS -> Computação -> clique em EC2
* Na nova página, clique em Launch Instance para criar sua nova instância EC2 <br /><br />

* Etapa 01: Escolha uma Amazon Machine Image (AMI) || Step 01: Choose an Amazon Machine Image (AMI)
   * Ubuntu Server 18.04 LTS (HVM), SSD Volume Type | 64-bit (x86) <br /><br />
   
* Etapa 02: Escolha um tipo de instância || Step 02: Choose an Instance Type
   ![instance type](https://user-images.githubusercontent.com/27836893/90992918-fe1f5280-e588-11ea-8289-e48ea0260ce4.PNG) <br /><br />
   
* Etapa 03: configurar os detalhes da instância || Step 03: Configure Instance Details
   * Mantenha as configurações padrão <br /><br />
   
* Etapa 04: adicionar armazenamento || Step 04: Add Storage
   * Mantenha as configurações padrão<br /><br />

* Etapa 05: adicionar tags || Step 05: Add Tags
   * Mantenha as configurações padrão<br /><br />

* Etapa 06: configurar o grupo de segurança || Step 06: Configure Security Group
   * Crie um novo grupo de segurança
   * De um nome para o grupo de segurança
   * Coloque uma breve descrição para o grupo de segurança<br /><br />

* Etapa 07: Revise o lançamento da instância || Step 07: Review Instance Launch
   * Realize a revisão da instancia antes de finalizar
   * Clique em Lançamento/Launch <br /><br />

* Etapa 08: Selecione um par de chaves existente ou crie um novo par de chaves || Step 08: Select an existing key pair or create a new key pair
   * Selecione criar um novo par de chaves
   * De um nome para o par de chaves
   * Realize o download do seu par de chaves
   * Salve esse arquivo em um lugar seguro 
   * Realize um backup desse arquivo em um lugar seguro<br /><br />
   
* OBS: O par de chaves que foi gerado vai ser utilizado para acessar a instancia do servidor EC2

<hr />
<hr />

### Configurando acesso à instância EC2

* Para acessar à instância EC2, será utilizado o software Termius, que por sua vez é um cliente SSH
* Realize o download do software nesse link [Termius](https://termius.com)
* Utilizando o IP atual da instância e o par de chaves que foi gerado na estapa 08 durante a criação da mesma, realize o acesso

<hr />
<hr />

### Apache, liberação de portas e VIM
* Inicie a instância no Console AWS e acesse o servidor pelo Termius
* Para realizar o update e o apgrade, execute: 

```
sudo apt update
sudo apt upgrade
```
 
* Para instalar o apache, execute: 
```
sudo apt install apache2
```

* Para efetuar a liberação da porta 80, adicione uma nova regra de entrada em sua instância no grupo de seguração utilizado
![Capturar](https://user-images.githubusercontent.com/27836893/91085078-49863f00-e623-11ea-99fe-89bf2c11e3cb.PNG)

* Para instalar o editor de texto VIM, execute:
```
sudo apt install vim
```

* Para configurar as opções do editor, execute: 
```
sudo vim /etc/vim/vimrc/
```

* Aperte I para entrar no modo de INSERÇÃO e descomente as seguintes linhas: 
```
if has("syntax")
 syntax on
endif

set background=dark

if has("autocmd")
 au BufReadPost * if line("'\"") > 1 && line("'\"") <= line("$") | exe "normal$
endif

if has("autocmd")
 filetype plugin indent on
endif
```

* Incluir no final do arquivo 
```
set nu
set cursorline
```

* Aperte ESC e digite :wq! para salvar e sair

* Agora com o VIM configurado, execute o seguinte comando para configurar o apache2:
```
sudo vim /etc/apache2/apache2.conf
```

* Dentro do arquivo, edite a linha do KeepAlive para ON

* OBS: O KeepAlive permite que o servidor utilize a mesma conexão para transferir múltiplos arquivos e é uma ótima maneira de reduzir o uso de recursos e aumentar a velocidade do seu site ao mesmo tempo.

<hr />
<hr />

### Virtual Host
* Inicie a instância no Console AWS e acesse o servidor pelo Termius
* Para realizar o update e o apgrade, execute: 

```
sudo apt update
sudo apt upgrade
```

* Para criar a pasta onde vai ficar o virtual Host e a pasta de logs, execute: 
```
 sudo mkdir -p /var/www/html/ids.local/public_html
 sudo mkdir /var/www/html/ids.local/logs
```

* Criamos agora um arquivo de chamada para ids
```
sudo  vim /etc/apache2/sites-available/ids.local.conf
```

* Dentro deste arquivo colocamos a seguinte descrição
```
<VirtualHost *:80>
 ServerAdmin webmaster@ids.local
 ServerName ids.local
 ServerAlias www.ids.local
 DocumentRoot /var/www/html/ids.local/public_html/
 ErrorLog /var/www/html/ids.local/logs/error.log
 CustomLog /var/www/html/ids.local/logs/access.log combined
</VirtualHost>
```

* Para conceder as permissões ao usuário logado
```
sudo chown -R $USER:$USER /var/www/html/ids.local/public_html
sudo chmod -R 755 /var/www/html/
```

* Criando um arquivo de exemplo e preenchendo com html:
```
sudo vim /var/www/html/ids.local/public_html/index.html

<html>
 <head>
   <title>Bem Vindo</title>
   <meta charset="UTF-8">
 </head>
 <body>
    <h1>Parabéns! O seu virtual host está funcionando!</h1>
 </body>
</html>
```

* Para criar um link simbólico, execute:
```
sudo a2ensite ids.local.conf
```

* Agora desative o link principal:
```
sudo a2dissite 000-default.conf
```

* reinicie o servidor apache2 
```
sudo service apache2 restart
```

* Para finalizar, coloque o IP do servidor no navegador e teste se está funcionando corretamente

<hr />
<hr />

### Instalando e Configurando o PostgreSQL

* Inicie a instância no Console AWS e acesse o servidor pelo Termius
* Para realizar o update e o apgrade, execute: 

```
sudo apt update
sudo apt upgrade
```

* Para instalar o postgres, execute:
```
sudo apt install postgresql-10
```

* Para habilitar/ativar o usuário no postgres, execute:
```
sudo -u postgres psql
alter user postgres with encrypted password 'senhaescolhida';
```

* Para habilitar acesso remoto ao servidor, execute:
```
sudo vim /etc/postgresql/10/main/postgresql.conf

Modifique 
# listen_addresses = 'localhost' # what IP address(es) to listen on

Para
listen_addresses = '*' # what IP address(es) to listen on

OBS: descomentando e trocando 'localhost' por '*'
```

* Para modificar as regras de liberação, execute:
```
sudo vim /etc/postgresql/10/main/pg_hba.conf

Atualize as seguintes linhas conforme o exemplo a baixo:

# "local" is for Unix domain socket connections only
local all all  trust

# IPv4 local connections:
host all all 0.0.0.0/0  md5
```

* reinicie o servico postgresql
```
sudo service postgresql restart
```

* Para efetuar a liberação da porta 5432, adicione uma nova regra de entrada em sua instância no grupo de seguração utilizado
![Capturar](https://user-images.githubusercontent.com/27836893/91095612-0c29ad80-e633-11ea-960a-ed5a8a4df226.PNG)

* Para finalizar, acesse o postgresql remotamente e teste se está funcionando corretamente

<hr />
<hr />

### Instalando e Configurando o MySQL, PHP e PHPMyAdmin

* Inicie a instância no Console AWS e acesse o servidor pelo Termius
* Para realizar o update e o apgrade, execute: 

```
sudo apt update
sudo apt upgrade
```

* Para instalar o MySQL, execute: 
```
 sudo apt install mysql-server-5.7
```

* Para realizar alguns ajustes na configuração e criar a nova senha, execute:
```
sudo mysql_secure_installation
```

* Para criar um super usuário no mysql, execute:
```
sudo mysql
GRANT ALL PRIVILEGES ON *.* TO 'ids'@'localhost' IDENTIFIED BY 'senhaescolhida';
```

* Para liberar o acesso remoto, execute:
```
sudo vim /etc/mysql/mysql.conf.d/mysqld.cnf
Comente a linha do bind-address
```

* Para instalar o PHP e ativar seus diretórios, execute
```
sudo apt install php7.2 libapache2-mod-php7.2 php7.2-mysql php7.2-pgsql

sudo mkdir /var/log/php
sudo chown www-data /var/log/php

OBS: (www-data é usuário do apache)
```

* Crie um arquivo teste para verificar as funcionalidades.
```
sudo vim /var/www/html/ids.local/public_html/phpinfo.php

<?php
  phpinfo();
?>
```

* Para instalar o phpmyadmin, execute
```
sudo apt install phpmyadmin

OBS: Selecione o servidor apache2 pois é o utilizado nesse cenário
```

<hr />
<hr />

### Configurando Páginas Pessoais

* Inicie a instância no Console AWS e acesse o servidor pelo Termius
* Para realizar o update e o apgrade, execute: 

```
sudo apt update
sudo apt upgrade
```

* Para ativar o módulo do usário logado, execute:
```
sudo a2enmod userdir
```

* Para atualizar a flag php_admin_flag engine Off, execute:
```
sudo /etc/apache2/mods-available/php7.2.conf

Comente a linha:
php_admin_flag engine Off
```

* Reinicie o apache
```
sudo service apache2 restart
```

* Para criar o diretório public_html, execute: 
```
mkdir ~/public_html
```

* Para criar um template de pré configuração para todos os usuários, execute:
```
sudo mkdir /etc/skel/public_html
sudo chmod 0700 /etc/skel/public_html 

OBS: Com isso os espaços pessoais “herdam” todas as potencialidades do site principal, ou seja, o utilizador tem ativado o suporte para php, as ligações seguras, acesso à base
de dados MySQL, etc.
```

<hr /><hr />

### Configurando Servidor DNS Gratuito - NOIP

* O primeiro passo é criar uma conta no site do serviço gratuito no-ip https://www.noip.com

* Após ter criado a conta, inicialize sua instância na AWS e pegue o IP para configurar o domínio no site

* Feitas as configurações no site do serviço, agora é a hora de configurar o nosso servidor de modo a que ele envie seu novo IP para o no-ip a intervalos regulares, o que faz com que precisemos decorar somente o domínio que registramos, e não mais o IP. Isso facilita a configuração do Termius, por exemplo, não sendo mais necessário mudar o IP nele a cada vez que a instância é parada e iniciada novamente

* Primeiramente vamos fazer o download do arquivo do cliente e descompactá-lo no nosso servidor 

* OBS: Para executar o comando make, que faz a compilação dos arquivos e gera o binário, são necessários dois pacotes que não estão instalados por padrão no Ubuntu (normalmente): o próprio make e o gcc.

```
sudo apt install make
sudo apt install gcc
cd /usr/local/src
wget https:www.noip.com/client/linux/noip-duc-linux.tar.gz
tar xf noip-duc-linux.tar.gz
cd noip-2.1.9-1/
make install
```

* Depois de feita a instalação, é necessário configurar o cliente no-ip, e isso é feito com o comando
```
/usr/local/bin/noip2 -C
```

* Algumas perguntas serão feitas: e-mail cadastrado no site no-ip, senha, qual o tempo de atualização do IP (em minutos), se deseja salvar as alterações e qual o arquivo de configuração.

* Feita a instalação e configuração, é hora de colocar o serviço para rodar. O comando por sua vez, executado no terminal, faz com o que o serviço passe a rodar, mas caso o servidor seja reinicializado, ele precisa ser rodado novamente.
```
/usr/local/bin/noip2
```

* Uma forma prática de automatizar a execução de um comando qualquer, é criando um arquivo chamado ```rc.local``` dentro do diretório ```etc``` e dar permissão de execussão para ele. Para fazer isso, execute os seguintes comandos
```
cd etc/
sudo vim rc.local
```

* Dentro desse arquivo adicione as seguintes linhas 
```
#!/bin/bash
/usr/local/bin/noip2
```

* Para dar permissão de execução ao scritp digite 
```
sudo chmod +x rc.local
```

* A partir deste momento, toda vez que o servidor for reiniciado, o arquivo ```rc.local``` será lido e o seu conteúdo interpretado, e o cliente noip voltará a ser executado automaticamente.

<hr /><hr />

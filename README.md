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

### Configurando acesso à instância EC2

* Para acessar à instacia EC2, será utilizado o software Termius, que por sua vez é um cliente SSH
* Realize o download do software nesse link [Termius](https://termius.com)
* Utilizando o IP atual da instância e o par de chaves que foi gerado na estapa 08 durante a criação da mesma, realize o acesso






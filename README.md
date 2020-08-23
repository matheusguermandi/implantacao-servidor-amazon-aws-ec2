![image20](https://user-images.githubusercontent.com/27836893/90990444-da9fdc00-e577-11ea-89eb-71590afb63c2.png)

<h1 align="center">
 Implatacao de Servidor - Amazon AWS EC2 
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

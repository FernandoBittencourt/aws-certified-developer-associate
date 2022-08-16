# AWS Certified Developer Associate
## AWS Regions
* A AWS tem regiões ao redor do mundo com nomes "us-east-1", "eu-west-3",...
* Uma região é um cluster (conjunto) de data centers.
* A maioria dos serviços tem escopo de região (region-scoped).
* Os critérios de escolha de uma região pode ser baseado em compliance, proximidade com o cliente, disponibilidade de serviços e preço.
## AWS Availability Zone (AZ)
* Cada região contém zonas de disponibilidade (AZ) com nomes "ap-southeast-2a","ap=southeast-2b".
* Contendo normalmente 3 zonas de disponibilidade por região, sendo o mínimo 2 e o máximo 6.
* Cada AZ é um ou mais datacenters com redundâncias de energia, rede e conectividade. São separados uns dos outros, isolados de desastres.
* Eles são conectados, com redes de alta banda e baixa latência.
## AWS Identity and Access Management (IAM)
* O AWS Identity and Access Management (IAM) é um serviço que ajuda controlar o acesso aos recursos da AWS de forma segura. 
* O IAM serve controlar quem está autenticado (fez login) e autorizado (tem permissões) a utilizar os recursos.
* É um serviço global.
* O Root Account criado por default, não deve ser utilizado e nem compartilhado.
* Os usuários (Users) são pessoas da sua organização que podem ser agrupados. 
* Cada um dos grupos (Groups) só pode conter usuários e não outros grupos.
* Os usuários podem pertencer a múltiplos grupos ou até mesmo a nenhum grupo.
* Alguns serviços da AWS precisam realizar ações a outros serviços da AWS e para isso é preciso incluir permissões com IAM Roles.
* As políticas (Policies) são um documento json que definem as permissões (Permissions) para requisições de serviços na AWS e pode ser usado com ser usado por Users, Groups e Roles. O recomentado é garantir o mínimo de privelegios possivel.
* Uma policy contém um id, uma versão e um ou mais statements (declarações).
* Um Statement em uma IAM policy consiste em Sid (Um identificador), Effect (Allow ou Deny), Principal (account/user/role), Action (lista de ações sobre o recurso), Resource(lista de recursos que a ação será aplicada) e Condition (Condição para que a politica seja válida).
* As boas práticas se segurança sugerem o uso de políticas de password (uso de senhas "fortes") e o uso de autenticação por multi fator (MFA).
* Para acesso programático (CLI/SDK) deve utilizar uma chave de acesso (Access key) gerada e são análogas a uma senha.
* IAM Credentials Report é uma ferramenta de segurança que gera um relatório que lista os usuários de sua conta e o status de suas credenciais, útil para auditoria.
* IAM Access Advisor mostra as permissões de serviço concedidas a um usuário e quando esses serviços foram acessados pela última vez. É possivel usar essas informações para revisar suas políticas.
## Elastic Compute Cloud (EC2)
* Na representação da infraestrutura como um serviço, o EC2 se comporta como uma máquina virtual alugada.
* É possivel definir o sistema operacional, a quantidade de CPU, RAM e o armazenamento, que pode ser conectado a rede (EBS/EFS) ou um hardware (EC2 Instance Store). Definir a rede (velocidade e Ip público), regras de firewall (security group) e um bootstrap script (EC2 User Data, comando de inicialização da máquina).
* É possivel definir o bootstrap script através do EC2 User Data, que é comando que será executado pelo usuário root uma única vez na primeira inicialização. Normalmente contém solicitações de atualização, download de softwares, entre outras dependências.
### Tipos de instâncias (EC2 Instance Types)
* É possivel definir tipos diferentes de instancias otimizadas para atender casos especificos.
* Segue a convenção "m5.2xlarge", sendo m= classe da instância, 5 = geração, 2xlarge = tamanho.
#### Propósito Geral (General Purpose)
* Ótimo para uma diversidade de cargas de trabalho, como servidores da Web ou repositórios de código
* É balanceada entre memoria, cpu e rede.
#### Computação otimizada (Compute Optimized)
* Ótimo para tarefas de computação intensiva que exigem alto desempenho processadores.
#### Memoria Otimizada (Memory Optimized)
* Desempenho rápido para cargas de trabalho que processam grandes conjuntos de dados na memória.
#### Armazenamento otimizado (Storage Optimized)
* Ótimo para tarefas de armazenamento intensivo que exigem alta leitura e gravação sequencial acesso a grandes conjuntos de dados no armazenamento local.
## Security Group
* O Security Group representa um firewalll. Ele controla como o tráfego é permitido dentro ou fora de nossas instâncias do EC2.
* O Security Group contêm apenas regras de permissão (allow rules). Podem ser referenciados por IP ou por um security group.
* Eles regulam o acesso as portas, faixa de ips, controle de rede de entrada (inbound/de outra para a instancia) e de saida (outbound/da instancia para a saida).
* Os security groups podem ser associados a multiplas instancias, restringido em uma combinação de região/VPC.
* Todo o tráfego de entrada é bloqueado por padrão e todo o tráfego de saida é permetido por padrão.
* Problemas de timeout, podem estar associados a um problema de security group. Problemas de connection refused, podem ser associados a um erro da aplicação ou a aplicação não foi iniciada.
## EC2 Instances Purchasing Options
### On-Demand Instances
* Recomendado para cargas de trabalho de curto prazo e ininterruptas. 
* Tem o custo mais alto, mas sem pagamento adiantado. O preço previsível e o pagamento é calculado por segundo.
* Sem compromisso de longo prazo.
### Instâncias reservadas (EC2 Reserved Instances)
* É necessario reservar atributos de instância específicos (tipo de instância, região, locação, sistema operacional)
* É preciso definir um período de reserva, que pode ser 1 ano ou 3 anos. Sendo quanto maior o tempo, maior o desconto.
* As opções de pagamento são sem adiantamento, com adiantamento parcial e com adiantamento total. Sendo a mais barata a que o adiantamento é total e a mais cara sem o adiantamento.
* O escopo da Instância Reservada pode ser Regional or Zonal (capacidade de reserva em uma AZ).
* Recomendado para aplicações de uso em estado estacionário. Por exemplo, um banco de dados.
* Existe uma variação um pouco mais cara, chamada **Convertible Reserved Instance**, ao qual é possivel mudar o tipo de instância, família de instâncias, sistema operacional, escopo e locação.
### EC2 Savings Plans
* Recebe um desconto com base no uso a longo prazo.
* Restrito para uma família de instâncias específica e região da AWS, mas flexível para tamanho da instância, sistema operacional  e locação.
### EC2 Spot Instances
* O mais barato entre todos. (cost-efficient)
* Instâncias que você pode “perder” a qualquer momento se seu preço máximo for menor que o preço spot atual.
* Não deve ser usado para tarefas criticas.
### EC2 Dedicated Hosts
* Um servidor físico com capacidade de instância do EC2 totalmente dedicado ao seu uso.
* Atende aos requisitos de compliance e permite vincular suas licenças de software ao servidor existentes.
* É a opção mais cara entre todos os tipos.
* Para opção de pagamento pode ser por On-Demand ou reservada (1 ou 3 anos).
### EC2 Dedicated Instances
* As instâncias são executadas em hardware que é dedicado à você.
* Pode compartilhar hardware com outros instâncias na mesma conta.
### EC2 Capacity Reservations
* Serve para reservar a capacidade das instâncias sob demanda em uma AZ específica por qualquer duração.
* Nenhum desconto é aplicado para este tipo.
* Adequado para cargas de trabalho ininterruptas de curto prazo que precisam estar em um AZ específico.
## EBS Volume
* Um volume EBS (Elastic Block Store) é uma drive de rede (não é um drive fisico) que você pode anexar para suas instâncias enquanto elas são executadas.
* Permite que suas instâncias persistam dados, mesmo após o término. Funcionando analogamente como um disco.
* Eles só podem ser montados em uma instância por vez, mas uma instancia pode conter mais de um EBS.
* Eles estão vinculados a uma zona de disponibilidade (AZ) específica.
* É possível fazer um backup (snapshot) do EBS. Não é necessario, apesar de recomendado, desanexar o EBS para fazer o snapshot. É possivel copiar o snapshot para outro AZ ou região.
* Por padrão, ao terminar uma instancia EC2 o tipo de root volume será excluído, pois seu atributo "Delete On Termination" é marcado por padrão. Quaisquer outros tipos de volume do EBS não serão excluídos, pois seu atributo "Delete On Termination" está desabilitado por padrão.
### EBS Volume Types
* gp2 / gp3 (SSD): Volume SSD de proposito geral que equilibra preço e desempenho para uma grande variedade de cargas de trabalho.
* io1 / io2 (SSD): Volume SSD de mais alto desempenho para baixa latência ou cargas de trabalho de alto rendimento.
* st1 (HDD): Volume de HDD de baixo custo projetado para cargas de trabalho de alta taxa de transferência acessadas com frequência.
* sc1 (HDD): Volume de HDD de menor custo projetado para cargas de trabalho acessadas com menos frequência.
* Somente gp2/gp3 and io1/io2 (os que são SSD) pode ser usado como "boot volumes".
### EBS Multi-Attach – io1/io2 family
* Anexe o mesmo volume EBS a várias instâncias do EC2 na mesma AZ.
* Cada instância tem permissões leitura e gravação para o volume.
## EC2 Instance Storage
*  EC2 Instance Store são discos de hardware de alto desempenho. Como o EBS tem uma boa performance, mas limitada. O instance storage atende cenarios em que é necessario esse alto desempenho.
*  Melhor desempenho de I/O.
*  Perdem o armazenamento se forem interrompidos, ou seja, existe o risco de perder dados se houver uma falha. São úteis para buffer, cache e outros conteúdos temporários.
## Elastic File System (EFS)
* NFS (network file system) gerenciado que pode ser montado em diversas instancias de EC2 em multi-AZ. Usa o protocolo NFSv4.1.
* Altamente disponível, escalável, caro (3x gp2) e com pagamento por uso.
* Usa o grupo de segurança para controlar o acesso ao EFS.
* Compatível com AMI baseada em Linux (não Windows).
* Criptografia em rest usando KMS.



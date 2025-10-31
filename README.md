##  🚀 Desafio DIO: Gerenciamento e Documentação de Instâncias EC2 na AWS
#  📋 Visão Geral do Projeto
Este repositório é o entregável do Desafio de Projeto da DIO, focado em consolidar os conhecimentos sobre o gerenciamento do serviço Elastic Compute Cloud (EC2) da Amazon Web Services (AWS).

O objetivo principal foi transformar a experiência prática de criação, configuração e ciclo de vida de uma instância EC2 em uma documentação clara e estruturada, utilizando o GitHub como ferramenta de compartilhamento técnico.

#  🎯 Objetivos de Aprendizagem Alcançados
Ao completar o desafio e documentar o processo, os seguintes conceitos foram aplicados e consolidados:

Lançamento de Instância: Compreensão e aplicação de todos os passos para o launch de uma VM (Máquina Virtual) na nuvem AWS.

Segurança e Conectividade: Configuração correta de Security Groups (Grupos de Segurança) e uso de Key Pairs (Pares de Chave) para acesso seguro via SSH.

Ciclo de Vida da Instância: Diferenciação e uso prático das ações de Stop, Start e Terminate.

Documentação Técnica: Organização de um repositório público no GitHub com foco na clareza e estrutura de processos.

#  🛠️ Detalhes da Implementação Técnica (Passo a Passo)
A implementação seguiu as boas práticas na AWS e concentrou-se no gerenciamento de uma instância de teste.

1. Configuração da Instância
Detalhe	Configuração Utilizada	Justificativa/Insight
AMI (Amazon Machine Image)	Amazon Linux 2 AMI	Escolha de um sistema operacional leve e compatível com a camada gratuita (Free Tier).
Tipo de Instância	t2.micro	Escolhido para se manter dentro dos limites da camada gratuita da AWS.
Key Pair	Criada nova (desafio-ec2-key.pem)	Essencial para autenticação segura. O arquivo .pem foi baixado para o ambiente local.
VPC e Subnet	Default	Utilização da configuração padrão para simplificar a rede neste laboratório.
2. Configuração do Grupo de Segurança (Security Group)
Um novo Security Group foi configurado para atuar como firewall virtual:

Tipo de Regra	Protocolo	Porta	Fonte (Source)	Propósito
Inbound	SSH	22	My IP	Permite acesso seguro via terminal, fundamental para o gerenciamento. (Recomendado: limite ao seu IP para segurança).
Inbound	HTTP	80	0.0.0.0/0	Permite que um servidor web básico instalado na instância seja acessível publicamente.
3. Conexão e Comandos Essenciais
Após o status da instância mudar para Running, a conexão foi realizada via SSH.

bash
# 1. Ajustar permissão da chave (necessário apenas em Linux/macOS)
chmod 400 desafio-ec2-key.pem

# 2. Conectar à instância (substitua o IP e o nome do arquivo)
ssh -i "desafio-ec2-key.pem" ec2-user@<IP_PÚBLICO_DA_SUA_INSTÂNCIA>

# Comandos de Exemplo Executados na Instância (Amazon Linux)
sudo yum update -y                    # Atualiza os pacotes do SO
sudo yum install httpd -y             # Instala o servidor web Apache
sudo systemctl start httpd            # Inicia o serviço web
sudo systemctl enable httpd           # Habilita o serviço para iniciar automaticamente
4. Gerenciamento do Ciclo de Vida
Foi realizada a prática de gerenciamento do ciclo de vida:

Ação	Descrição	Impacto em Custos e Dados
Stop	Desliga a instância de forma controlada.	A cobrança da instância para, mas o EBS (armazenamento) continua sendo cobrado.
Start	Liga a instância novamente.	A cobrança é retomada. Geralmente, a instância recebe um novo IP Público (a menos que um IP Elástico seja usado).
Terminate	Deleta a instância permanentemente.	A cobrança é encerrada. Por padrão, o volume EBS também é deletado, garantindo a remoção de todos os custos.
💡 Conceitos Chave e Insights Adquiridos
Esta seção destaca os aprendizados mais importantes do laboratório:

Chave de Segurança (Key Pair): É o método de autenticação criptografada. A chave privada (.pem) é insubstituível e, se perdida, o acesso via SSH à instância é impossível.

Firewall no Nível da Instância: O Security Group é a primeira linha de defesa, atuando como um firewall que só permite o tráfego que você explicitamente autoriza nas portas e protocolos definidos.

Diferença de Ciclo de Vida: É crucial entender que Stop (Parar) não é o mesmo que Terminate (Encerrar/Deletar). Parar uma instância mantém o armazenamento e a configuração, mas encerrá-la remove todos os recursos associados.

MetaDados da Instância: Aprendi a visualizar os metadados da instância (http://169.254.169.254/latest/meta-data/) para obter informações como IP local, ID da instância e Key Pair.

🚀 Próximos Passos e Aprimoramento
Como continuidade deste aprendizado, os próximos passos seriam:

IP Elástico (EIP): Configurar um EIP para associar um endereço IP público estático à instância, garantindo que o IP não mude após um Stop/Start.

User Data: Utilizar o campo User Data na criação da instância para injetar e executar scripts bash automaticamente na primeira inicialização (ex: instalar um servidor web de forma automatizada).

Monitoramento: Configurar alarmes básicos do CloudWatch para monitorar métricas como utilização da CPU e o status da instância.

👨‍💻 Autor
Repositório Desenvolvido por: RUI FRANCISCO

📝 Notas Finais
Este projeto serviu como uma excelente oportunidade para consolidar o conhecimento prático sobre o serviço EC2 da AWS, desde a criação até o gerenciamento do ciclo de vida das instâncias, sempre com foco em segurança e boas práticas.

Instruções para uso:

Clone este repositório

Personalize as configurações de acordo com suas necessidades

Siga os passos documentados para replicar o ambiente

Adicione suas próprias capturas de tela na pasta images

⭐ Se este projeto foi útil para você, não esqueça de dar uma estrela no repositório!

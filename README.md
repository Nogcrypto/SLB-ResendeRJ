Trabalho do módulo de NFT da Universidade Católica de Pernambuco.
Programado por Nogcrypto e elaborado por Rômulo Parente , Marise Figueras e Rolando Priviero.

Projeto de NFT aplicado na tokenização imobiliária que consiste em fragmentar duas NFTs de operações diferentes em 1.000.000 de frações, onde cada uma será mintada em valores entre R$100 e R$200 com boas taxas de retorno frente a inflação.

A NFT SLB-ResendeRJ é uma operação de sale and leaseback, em que está sendo armazenado em um contrato inteligente chamado "SLBResendeRJ" que herda de um contrato "MyERC1155", que herda de "ERC1155" da biblioteca OpenZeppelin. Esse contrato gerencia tokens ERC-1155.

O contrato temvárias funções de segurança para transferir, queimar e criar novos tokens, além de vários eventos que são emitidos quando essas operações são realizadas. Ele também possui uma função "fragment" que permite ao proprietário fragmentar o ativo em frações menores e distribuir para outros endereços.


InterfaceWeb
 Bibliotecas importadas: ipfs-api e web3.js.
 
 Usa a biblioteca web3.js para se conectar a um smart contract em uma blockchain, usando o provedor de conexão HTTP com o endereço de um nó do indufa específico. Ele também usa a biblioteca ipfs-api para recuperar a imagem do IPFS usando o CID recuperado do contrato inteligente. Ele faz isso definindo o endereço da API do Pinata, a chave e o segredo da API. E também recupera o elemento da imagem da página HTML e atribui a ela a imagem recuperada do IPFS.
 
 Uso a função "require" do Node.js para importar a biblioteca web3.js e cria uma nova instância da classe Web3. E depois importa a biblioteca ipfs-api especificando as configurações do host, porta, protocolo e cabeçalhos com a chave e segredo da API do Pinata. Utiliza o método pin.get() para recuperar a imagem do IPFS usando o CID recuperado do contrato. Também exibe a imagem recuperada na página HTML. Realiza chamada para as funções "getValue" e "getCapRate" do contrato inteligente e exibe o resultado no console.

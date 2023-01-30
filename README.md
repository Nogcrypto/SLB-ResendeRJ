Trabalho do módulo de NFT da Universidade Católica de Pernambuco.
Programado por Nogcrypto e elaborado por Rômulo Parente , Marise Figueras e Rolando Priviero.

Projeto de NFT aplicado na tokenização imobiliária que consiste em fragmentar uma NFT sendo do tipo de operação Sale and Leaseback em 2.000.000 de frações, onde acontecerá o mint na rede polygon.

Este contrato inteligente foi criado usando a linguagem de programação Solidity e a biblioteca 'ERC1155LazyMint' da ThirdWeb. Ele foi deployado na Blockchain da Polygon e utiliza o padrão de token ERC1155. O total supply é especificado pela array 'supplies', que tem dois elementos, cada um com o valor de 1.000.000. O max supply não foi especificado e pode ser adicionado posteriormente pelo proprietário do contrato.

As informações adicionais ou metadados sobre o imóvel podem ser encontradas na descrição na Opensea. O objetivo deste contrato inteligente é mintar NFTs de uma coleção de pacotes, onde cada usuário só pode reivindicar um NFT por coleção. A verificação é feita por meio do mapeamento 'member'. O contrato também possui métodos para cunhar as NFTs, verificar se um usuário pode reivindicar uma NFT e verificar o número total de NFTs cunhadas por coleção.

A biblioteca 'ERC1155LazyMint' importada no contrato e as verificações realizadas na função mintNFTs são outros aspectos interessantes que podem ser incluídos. Além disso, as regras de emissão, como a limitação de um usuário só poder reivindicar um NFT por coleção, e a estrutura de dados 'member' usada para registrar as reivindicações de NFTs também são interessantes de se considerar.

Uma das coisas a se enfatizar é que mostra a segurança e o controle na emissão desses NFTs. No futuro, novos projetos relacionados a real estate podem ser lançados pelo nosso grupo, mas isso ainda não há nada concreto.

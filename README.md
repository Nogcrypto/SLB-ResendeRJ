// SPDX-License-Identifier: MIT
pragma solidity 0.8.17;

import "@openzeppelin/contracts/token/ERC1155/ERC1155.sol";

  abstract contract MyERC1155 is ERC1155 {
    event Transfer (address indexed from, address indexed to, uint256 indexed tokenId, uint256 amount);
    event Mint(address to, uint256 tokenId, uint256 amount);
    event Burn(address from, uint256 tokenId, uint256 amount);
    event OwnershipTransferError(address msgSender, address owner, uint256 tokenId);

    constructor() {

    }

    function _transferFrom(address from, address to, uint256 tokenId, uint256 amount) internal override {
      super._transferFrom(from, to, tokenId, amount);
      emit Transfer(from, to, tokenId, amount);

    }

    function _mint(address to, uint256 tokenId, uint256 amount) internal override {
      super._mint(to, tokenId, amount);
      emit Mint(to, tokenId, amount);
    }

    function _burn(address from, uint256 tokenId, uint256 amount) internal override {
      super._burn(from, tokenId, amount);
      emit Burn(from, tokenId, amount);
    }

  }
  
  import "path/artifacts/teste.sol";

  contract SLBResendeRJ is MyERC1155 {
    address owner;
    string public name;
    string public location;
    string public imageHash;
    uint256 public landArea;
    uint256 public builtArea;
    uint256 public value;
    uint256 public capRate;
    mapping(address => bool) public tokens; // mapping para armazenar quais tokens pertencem a qual endereço
    uint256 public totalSupply;
    address[] public whitelist;
    mapping (address => uint256) public fragments; // mapping para armazenar a quantidade de fragmentos de cada endereço
    uint256 public maxSupply = 2000000; // limite máximo de fragmentos
    mapping(uint256 => address) public tokenIdToOwner; 
    
    

    constructor() public {
        owner = msg.sender;
        name = "SLB Resende-RJ";
        location = "Resende-RJ";
        landArea = 70000;
        builtArea = 33533;
        value = 100000000;
        capRate = 11.4;
        totalSupply = 1000000;
        whitelist.push(msg.sender);
    }

    function fragment() public {
        require(msg.sender == owner, "Apenas o proprietario pode fragmentar a NFT"); // verifica se o remetente é o proprietário
        require(totalSupply + 2000000 <= maxSupply, "Nao e possivel fragmentar mais, limite maximo alcancado"); // verifica se o totalSupply não ultrapassa o limite
        require(fragments[msg.sender] < totalSupply, "Voce ja possui todos os fragmentos"); // verifica se o remetente já possui todos os fragmentos existentes
        require(fragments[msg.sender] != totalSupply, "Voce ja possui todos os fragmentos existentes, nao e possivel adicionar mais");
        for (uint i = 0; i < 2000000; i++) {
            require(tokenIdToOwner[totalSupply + i] == address(0), "Esse fragmento ja foi atribuido");
            tokenIdToOwner[totalSupply + i] = msg.sender;
        }
        if (msg.sender != owner) {
            emit OwnershipTransferError(msg.sender, owner, totalSupply);
            return;
        }

        fragments[msg.sender] += 2000000; // adiciona os fragmentos ao endereço do remetente
        totalSupply += 2000000; // adiciona os fragmentos ao totalSupply
    }

    function getValue() public view returns (uint256) {
        return value;
    }

    function getCapRate() public view returns (uint256) {
        return capRate;
    }

    function transfer(address to, uint256 tokenId, uint256 amount) public {
        address tokenOwner = tokenIdToOwner[tokenId];
        _transferFrom(msg.sender, to, tokenId, amount);
        require(msg.sender == owner, "Apenas o proprietario pode transferir a NFT"); // verifica se apenas o proprietário transfere a NFT
        require(msg.sender == tokenOwner, "Voce nao e o proprietario deste token"); // Verifica se e o proprietario do token
        require(whitelist.indexOf(tokenOwner) != -1, "Voce nao esta na whitelist"); // verifica se o remetente está na whitelist
        require(tokenIdToOwner[tokenId] == msg.sender, "Voce nao possui esse token"); // verifica se o remetente possui o token
        require(tokens[to] == true, "O destinatario ja possui um token"); // verifica se o destinatário já possui um token
        require(tokenId > 0 && tokenId <= totalSupply, "Token invalido"); // verifica se o token id está dentro do limite
        require(to != address(0), "Endereco destino invalido");
        tokens[msg.sender] = false;
        tokens[to] = true;
        tokenIdToOwner[tokenId] = to;
        emit Transfer(msg.sender, to, tokenId);
        }

    function mint(address to, uint256 tokenId, uint256 amount) public {
      require(msg.sender == owner, "Apenas o proprietario pode adicionar mais tokens");
      require(tokenId > 0 && tokenId <= totalSupply, "Token invalido");
      require(amount > 0, "A quantidade deve ser maior do que zero");
      totalSupply += amount;
      fragments[to] += amount;
      tokenIdToOwner[tokenId] = to;
      tokens[to] = true;
      emit Mint(to, tokenId, amount);
    }

    function burn(address from, uint256 tokenId, uint256 amount) public {  
      require(msg.sender == owner, "Apenas o proprietario pode queimar tokens");
      require(tokenId > 0 && tokenId <= totalSupply, "Token invalido");
      require(amount > 0, "A quantidade deve ser maior do que zero");
      totalSupply -= amount;
      emit Burn(from, tokenId, amount);
      }
      function setImageHash(string memory newImageHash) public {
        require(msg.sender == owner, "Somente o proprietario pode atribuir o hash da imagem");
        imageHash = newImageHash;
    
      }

      function getImageHash() public view returns (string memory) {
        return imageHash;
      }  

      
    



    
}

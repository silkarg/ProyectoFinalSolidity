///////////////////////VERSION FINAL//////////////////////////
// "SPDX-License-Identifier: MIT"
// Proyecto Final Bootcamp Blockdemy - Web3Latinas: Participación Electoral

pragma solidity ^0.8.0; 

contract eleccion{ 
// Variables de Estado
   uint deployDate;
   uint tiempo = 1 minutes; // 300 or 5*60 - Limite de tiempo para votar 

// Solo invoca una vez cuando se implementa el contrato
    constructor(){ 
        deployDate = block.timestamp;
    }
     
// Registro Candidatos    
    struct candidato{
        uint id; // identificador del candidato
        string nombre; // nombre del candidato
        uint nvoto; // numero de votos acumulados del candidato
    }

// Registro Electores
    struct elector{
        bool voted; //si es true, el elector ya voto
    }

  
    candidato public candidato1 = candidato({
        id: 1,
        nombre: "Juan Gonzalez",
        nvoto: 0
    });
        
    candidato public candidato2 = candidato({
        id: 2,
        nombre: "Julia Garcia",
        nvoto: 0
    });

    candidato public candidato3 = candidato({
        id: 3,
        nombre: "Maria Romero",
        nvoto: 0
    });


// Agregaría un mapping para poder cambiar la variable voted de cada elector
    mapping(address => elector) electores;
    mapping(address => candidato) _candidato; 
    mapping(address => uint) balance;

// Obtener la direccion del elector
    function getElector() public view returns (address) {    
        return msg.sender;
    }

// El votante ejerce su voto
    function getVoto(uint nuevobalance) public {
        //verifica limite de tiempo para votar
        require (block.timestamp >= (deployDate + tiempo) == false,"El tiempo para votar expiro");

        //Antes de registrar el voto es chequear que este usuario no haya votado antes. 
        require (electores[msg.sender].voted == false,"El usuario ya registro su voto");
        

        balance[msg.sender] = nuevobalance;
        
        if(nuevobalance == 1){
            candidato1.nvoto += 1; 
        } else if (nuevobalance == 2){
            candidato2.nvoto += 1; 
        } else{
            candidato3.nvoto += 1;
        }

        //Cuando llega a esta parte del código el usuario ya votó
        //entonces acá agregamos la marca de que este votante ya registro su voto poniendo en true la variable voted
        electores[msg.sender].voted = true;
    }

// Ganador de las elecciones
    function ganador() public view returns(uint _Id, string memory _Nombre, uint _Nvotos) {
        if (candidato1.nvoto > candidato2.nvoto && candidato1.nvoto > candidato3.nvoto) {
            return (candidato1.id, candidato1.nombre, candidato1.nvoto);
        } else if (candidato2.nvoto > candidato1.nvoto && candidato2.nvoto > candidato3.nvoto) {
            return (candidato2.id, candidato2.nombre, candidato2.nvoto);
        } else{
            return (candidato3.id, candidato3.nombre, candidato3.nvoto);
        }       
    }

// Verifica si ha pasado 1 minuto desde que se implementó el contrato
    function tiempoLimite() public view returns (bool) {
        return (block.timestamp >= (deployDate + tiempo));
    }    
}

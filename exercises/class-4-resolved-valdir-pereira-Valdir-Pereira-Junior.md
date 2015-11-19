# MongoDB - Aula 04 - Exercício
autor: Valdir Pereira Júnior

> db.pokemons.find().pretty()
{
        "_id" : ObjectId("564c9e0d03b96795b09ed6c7"),
        "name" : "Pikachu",
        "description" : "Rato elétrico bem fofinho",
        "type" : "electric",
        "attack" : 55,
        "defense" : 20,
        "height" : 0.4
}
{
        "_id" : ObjectId("564c9e0d03b96795b09ed6c8"),
        "name" : "Bulbassauro",
        "description" : "Chicote de trepadeira",
        "type" : "grass",
        "attack" : 49,
        "height" : 0.4
}
{
        "_id" : ObjectId("564c9e0d03b96795b09ed6c9"),
        "name" : "Charmander",
        "description" : "Esse é o cao chupando manga de fofinho",
        "type" : "fire",
        "attack" : 52,
        "height" : 0.6
}
{
        "_id" : ObjectId("564c9e0d03b96795b09ed6ca"),
        "name" : "Squirtle",
        "description" : "Ejeta água que passarinho nao bebe",
        "type" : "water",
        "attack" : 48,
        "height" : 0.5
}
{
        "_id" : ObjectId("564c9e0d03b96795b09ed6cb"),
        "name" : "chikorita",
        "description" : "Pedaço de folha",
        "type" : "grass",
        "attack" : 100,
        "defense" : 50,
        "height" : 0.9
}
{
        "_id" : ObjectId("564c9e0d03b96795b09ed6cc"),
        "name" : "Growlithe ",
        "description" : "lobo sentimental",
        "type" : "fire",
        "attack" : 40,
        "defense" : 20,
        "height" : 0.7
}
{
        "_id" : ObjectId("564c9e0d03b96795b09ed6cd"),
        "name" : "Magnemite",
        "description" : "Imã voador em formato de olho",
        "type" : "electric",
        "attack" : 20,
        "defense" : 30,
        "height" : 0.3
}
{
        "_id" : ObjectId("564c9e0d03b96795b09ed6ce"),
        "name" : "Onix",
        "description" : "Michoca marombeira pedrificada",
        "type" : "rock",
        "attack" : 20,
        "defense" : 70,
        "height" : 8.8
}
{
        "_id" : ObjectId("564c9e0d03b96795b09ed6cf"),
        "name" : "Horsea",
        "description" : "cavalo marinho bebe",
        "type" : "water",
        "attack" : 20,
        "defense" : 30,
        "height" : 0.4
}
{
        "_id" : ObjectId("564c9e0d03b96795b09ed6d0"),
        "name" : "Trevenant ",
        "description" : "Arvore do mal",
        "type" : "grass",
        "attack" : 60,
        "defense" : 30,
        "height" : 1.5
}



## **Adicionar** 2 ataques ao mesmo tempo para os seguintes pokemons: Pikachu, Squirtle, Bulbassauro e Charmander.

	> var query = {$or: [{name: /pikachu/i}, {name: /squirtle/i}, {name: /bulbassauro/i}, {name: /charmander/i} ] }
	>
	> var mod = {$set: {moves: ["tapa na cara", "chute rapido"]} }
	>
	> var options = {multi: true}
	> db.pokemons.update(query, mod, options)
	WriteResult({ "nMatched" : 4, "nUpserted" : 0, "nModified" : 4 })
	> db.pokemons.find(query).pretty()
	{
        "_id" : ObjectId("564c9e0d03b96795b09ed6c7"),
        "name" : "Pikachu",
        "description" : "Rato elétrico bem fofinho",
        "type" : "electric",
        "attack" : 55,
        "defense" : 20,
        "height" : 0.4,
        "moves" : [
                "tapa na cara",
                "chute rapido"
        ]
	}
	{
        "_id" : ObjectId("564c9e0d03b96795b09ed6c8"),
        "name" : "Bulbassauro",
        "description" : "Chicote de trepadeira",
        "type" : "grass",
        "attack" : 49,
        "height" : 0.4,
        "moves" : [
                "tapa na cara",
                "chute rapido"
        ]
	}
	{
        "_id" : ObjectId("564c9e0d03b96795b09ed6c9"),
        "name" : "Charmander",
        "description" : "Esse é o cao chupando manga de fofinho",
        "type" : "fire",
        "attack" : 52,
        "height" : 0.6,
        "moves" : [
                "tapa na cara",
                "chute rapido"
        ]
	}
	{
        "_id" : ObjectId("564c9e0d03b96795b09ed6ca"),
        "name" : "Squirtle",
        "description" : "Ejeta água que passarinho nao bebe",
        "type" : "water",
        "attack" : 48,
        "height" : 0.5,
        "moves" : [
                "tapa na cara",
                "chute rapido"
        ]
	}



## **Adicionar** 1 movimento em todos os pokemons: `desvio`.##

	> var query = {}
	>
	> var mod = {$push: {moves: "desvio"}}
	>
	> var options = {multi: true}
	> db.pokemons.update(query, mod, options)
	WriteResult({ "nMatched" : 10, "nUpserted" : 0, "nModified" : 10 })



## **Adicionar** o pokemon `AindaNaoExisteMon` caso ele não exista com todos os dados com o valor `null` e a descrição: "Sem maiores informações".##

var query = {name: /NaoExisteMon/i}
var mod = {
  $setOnInsert: {
	name: "NaoExisteMon", 
	description: "Sem maiores informações"
	attack: null, 
	defense: null, 
	height: null, 
  }
}
var options = {upsert: true}
db.pokemons.update(query, mod, options)


## Pesquisar todos o pokemons que possuam o ataque `investida` e mais um que você adicionou, escolha seu pokemon favorito.##


## Pesquisar **todos** os pokemons que possuam os ataques que você adicionou, escolha seu pokemon favorito.##


## Pesquisar **todos** os pokemons que não são do tipo `elétrico`.##


## Pesquisar **todos** os pokemons que tenham o ataque `investida` **E** tenham a defesa **não menor ou igual** a 49.##


## Remova **todos** os pokemons do tipo água e com attack menor que 50.


## Esse item não está no vídeo e se você fizer significa que você lê as coisas, nesse exercício demonstre qual a diferença entre os operadores $ne e $not.


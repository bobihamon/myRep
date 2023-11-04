# myRep 

## My name is hog rider

![my photo!!!](https://i1.sndcdn.com/avatars-xtJu46TM7Vstp28x-3kubIQ-t500x500.jpg)

I'm **javascript blackman**. *This is my example of code*

```javascript

let pokemons;
let promises = [];
let sortedPokemons;

let resultElement = document.getElementById("result")
let navElement = document.querySelector("nav")

const kantoPokemonsUrl = "https://pokeapi.co/api/v2/pokemon?limit=127";
const kantoXHR = new XMLHttpRequest();
kantoXHR.open("GET", kantoPokemonsUrl);
kantoXHR.responseType = "json";
kantoXHR.send();
kantoXHR.onload = () => {
    kantoXHR.response.results.forEach((pokemon) => {
        let promise = new Promise(function (reslove, reject) {
            let xhr = new XMLHttpRequest();
            xhr.open("GET", pokemon.url);
            xhr.responseType = "json";
            xhr.send();
            xhr.onload = () => {
                if (xhr.status == 200) {
                    reslove(xhr.response)
                }else{
                    reject(xhr.statusText)
                }
            };
            xhr.onerror = () => {
                reject(xhr.statusText)
            };
        });
        promises.push(promise)
    });
    Promise.all(promises).then((result)=>{
        pokemons = result
        sortedPokemons = pokemons.sort()
        console.log(pokemons)
        resultElement.innerHTML = ""
        sortedPokemons.forEach(pokemon=>drawPokemon(pokemon))
    })
};


const drawPokemon = (pokemon) =>{
    let pokemonElement = document.createElement("div")
    pokemonElement.classList.add("pokemon")
    pokemonElement.innerHTML = `
        <p>id: #${pokemon.id}</p>
        <hr>
        <h1>${pokemon.name}</h1>
        <img src="${pokemon.sprites.front_default}">
        <div class="status">
            <p class="hp"></p>&#10084; ${pokemon.stats[0].base_stat}</p>
            <p class="attack"></p>&#9876; ${pokemon.stats[1].base_stat}</p>
            <p class="defence"></p>&#128737; ${pokemon.stats[2].base_stat}</p>
        </div>
    `
    let typeList = document.createElement("ul")
    pokemon.types.forEach((type)=>{
        let typeItem = document.createElement("li")
        typeItem.innerText = type.type.name
        typeList.appendChild(typeItem)
    })
    pokemonElement.appendChild(typeList)
    resultElement.appendChild(pokemonElement)
}

let order = 1
let sortForm = document.getElementById("sort-form")

sortForm.addEventListener("change", (event) => {
    if(event.target.name == "order"){
        switch(event.target.value){
            case "upsc":
                order = 1
                break;
            case "desc":
                order = -1
                break;
        }
    }
    switch(sortForm["sort"].value){
       case"id" : 
        sortedPokemons = sortedPokemons.sort((first, second)=>{
            if(first.id > second.id){
                return order
            }
            if(first.id<second.id){
                return -order
            }
            return 0 
        }) 
        break;
       case"name" : 
        sortedPokemons = sortedPokemons.sort((first, second)=>{
            if(first.name > second.name){
                return order
            }
            if(first.name<second.name){
                return -order
            }
            return 0 
        }) 
        break;
       case"hp" : 
        sortedPokemons = sortedPokemons.sort((first, second)=>{
            if(first.stats[0].base_stat > second.stats[0].base_stat){
                return order
            }
            if(first.stats[0].base.stat<stats[0].base.stat){
                return -order
            }
            return 0 
        }) 
        break;
       case"attack" : 
        sortedPokemons = sortedPokemons.sort((first, second)=>{
            if(first.stats[1].base_stat > second.stats[1].base_stat){
                return order
            }
            if(first.name<second.name){
                return -order
            }
            return 0 
        }) 
        break;
       case"defence" : 
        sortedPokemons = sortedPokemons.sort((first, second)=>{
            if(first.stats[2].base_stat > second.stats[2].base_stat){
                return order
            }
            if(first.stats[2].base_stat<stats[2].base_stat){
                return -order
            }
            return 0 
        }) 
        break;
        
    }
    redrawSortPokemons()
})

function redrawSortPokemons(){
    resultElement.innerHTML = ""
    sortedPokemons.forEach(pokemon=>drawPokemon(pokemon))
}

document.getElementById("filter-form").addEventListener("submit", function(event){
    event.preventDefault();
    sortedPokemons = pokemons
    if(event.target["name-filter"].value){
        sortedPokemons = sortedPokemons.filter((pokemon)=>{
            return pokemon.name.indexOf(event.target["name-filter"].value.toLowerCase()) != -1
        })
    }
    if(event.target["hp-filter-form"].value > 10){
        sortedPokemons = sortedPokemons.filter((pokemon)=>{
            return pokemon.stats[0].base_stat >= event.target["hp-filter-form"].value
        })
    }
    if(event.target["hp-filter-to"].value < 250){
        sortedPokemons = sortedPokemons.filter((pokemon)=>{
            return pokemon.stats[0].base_stat <= event.target["hp-filter-to"].value
        })
    }
    if(event.target["attack-filter-form"].value > 5){
        sortedPokemons = sortedPokemons.filter((pokemon)=>{
            return pokemon.stats[1].base_stat >= event.target["attack-filter-form"].value
        })
    }
    if(event.target["attack-filter-to"].value < 130){
        sortedPokemons = sortedPokemons.filter((pokemon)=>{
            return pokemon.stats[1].base_stat <= event.target["attack-filter-to"].value
        })
    }
    if(event.target["defence-filter-form"].value > 5){
        sortedPokemons = sortedPokemons.filter((pokemon)=>{
            return pokemon.stats[2].base_stat >= event.target["defence-filter-form"].value
        })
    }
    if(event.target["defence-filter-to"].value < 180){
        sortedPokemons = sortedPokemons.filter((pokemon)=>{
            return pokemon.stats[2].base_stat <= event.target["defence-filter-to"].value
        })
    }
    redrawSortPokemons()
})
```
My social medias

*[My instagram](https://instagram.com)
*[My telegram](https://t.me/bobi1724)
*[My youtube](https://www.youtube.com/watch?v=dQw4w9WgXcQ&ab_channel=RickAstley)




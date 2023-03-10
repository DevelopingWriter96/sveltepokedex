<script>
   let poke = []
   
   let selectedPoke = []

   let src=""

   let types=[]

   let typeSort=[]

   let type=""

   let selected;

   let pokeBall = {}

   let favorites = []

   async function getPokemon() {
    const res = await fetch('https://pokeapi.co/api/v2/pokemon?limit=100000&offset=0')
    const data = await res.json()

    poke = data.results

    console.log(poke)
   }
   
   async function selectPokemon(select) {
    const res = await fetch(select)
    const data = await res.json()

    selectedPoke = data;

    console.log(selectedPoke)

    src = data.sprites.front_default

    console.log(src)

    types = data.types

    console.log(types);
   }

   async function sortByType(event) {
                type = event;
                console.log(type);
                    fetch(`https://pokeapi.co/api/v2/type/${type}/`)
                        .then(res => res.json())
                        .then(data => {
                            console.log(data);
                            typeSort = data.pokemon;
                        })
            }
    function addFavoritePokemon(pokemon, num) {
        pokeBall = {name: pokemon, url: `https://pokeapi.co/api/v2/pokemon/${num}/`};
        console.log(pokeBall);
        if (favorites.find(favoritePokemon => favoritePokemon.name === pokemon)){
                favorites.splice((favorites.indexOf(pokemon)-1), 1);
                console.log(favorites);
            } else {
                favorites.push(pokeBall);
                console.log(favorites); 
            }
        }
    function loadFavorites() {
        poke = favorites;
        }
</script>

<h1>Gotta Catch Em' All!</h1>
<div><h2>#{selectedPoke.id} {selectedPoke.name}</h2>
<img {src} alt="pokemon">
<h3>Types</h3>
<ul>
{#each types as type}
    <li class={type.type.name}>{type.type.name}</li>
{/each}
</ul>
<h3>Height: {selectedPoke.height / 10} M</h3>
<h3>Weight: {selectedPoke.weight / 10} KG</h3>
<button on:click={addFavoritePokemon(selectedPoke.name, )}>Toggle Favorite Pokemon</button>
<button on:click={loadFavorites}>Sort Favorites</button>
<button on:click={getPokemon}>Get Pokemon</button>
<select bind:value={selected} on:change={sortByType(selected)}>
    <option>Choose One</option>
    <option value="normal">Normal</option>
    <option value="fire">Fire</option>
    <option value="water">Water</option>
    <option value="grass">Grass</option>
    <option value="electric">Electric</option>
    <option value="ice">Ice</option>
    <option value="fighting">Fighting</option>
    <option value="poison">Poison</option>
    <option value="ground">Ground</option>
    <option value="flying">Flying</option>
    <option value="psychic">Psychic</option>
    <option value="bug">Bug</option>
    <option value="rock">Rock</option>
    <option value="ghost">Ghost</option>
    <option value="dark">Dark</option>
    <option value="dragon">Dragon</option>
    <option value="steel">Steel</option>
    <option value="fairy">Fairy</option></select>
<ul>
{#each poke as pokemon}
    <li on:click = {selectPokemon(pokemon.url)} on:keypress={selectPokemon(pokemon.url)}>{pokemon.name}</li>
{/each}
</ul>
<ul>
{#each typeSort as type}
    <li on:click = {selectPokemon(type.pokemon.url)} on:keypress={selectPokemon(type.pokemon.url)}>{type.pokemon.name}</li>
{/each}
</ul>
</div>

<style>
    body {
        background-color: red;
        color: white;
    }

    ul li {
        list-style-type: none;
    }

    .normal {
        color: white;
        background-color: #a8a878;
        text-align: center;
        width: 10%;
        padding: 0.5%;
        
    }

    .fighting {
        color: white;
        background-color: #c03028;
        text-align: center;
        width: 10%;
        padding: 0.5%;
    }

    .flying {
        color: white;
        background-color: #a890f0;
        text-align: center;
        width: 10%;
        padding: 0.5%;
    }

    .poison {
        color: white;
        background-color: #a040a0;
        text-align: center;
        width: 10%;
        padding: 0.5%;
    } 

    .ground {
        color: white;
        background-color: #e0c068;
        text-align: center;
        width: 10%;
        padding: 0.5%;
    }

    .rock {
        color: white;
        background-color: #b8a038;
        text-align: center;
        width: 10%;
        padding: 0.5%;
    }

    .bug {
        color: white;
        background-color: #a8b820;
        text-align: center;
        width: 10%;
        padding: 0.5%;
    } 

    .ghost {
        color: white;
        background-color: #705898;
        text-align: center;
        width: 10%;
        padding: 0.5%;
    }

    .steel {
        color: white;
        background-color: #b8b8d0;
        text-align: center;
        width: 10%;
        padding: 0.5%;
    }

    .fire {
        color: white;
        background-color: #f08030;
        text-align: center;
        width: 10%;
        padding: 0.5%;
    } 
    
    .water {
        color: white;
        background-color: #6890f0;
        text-align: center;
        width: 10%;
        padding: 0.5%;
    } 

    .grass {
        color: white;
        background-color: #78c850;
        text-align: center;
        width: 10%;
        padding: 0.5%;
    }

    .electric {
        color: white;
        background-color: #f8d030;
        text-align: center;
        width: 10%;
        padding: 0.5%;
    } 
    
    .psychic {
        color: white;
        background-color: #f85888;
        text-align: center;
        width: 10%;
        padding: 0.5%;
    } 

    .ice {
        color: white;
        background-color: #98d8d8;
        text-align: center;
        width: 10%;
        padding: 0.5%;
    }

    .dragon {
        color: white;
        background-color: #7038f8;
        text-align: center;
        width: 10%;
        padding: 0.5%;
    } 
    
    .dark {
        color: white;
        background-color: #705848;
        text-align: center;
        width: 10%;
        padding: 0.5%;
    } 

    .fairy {
        color: white;
        background-color: #ee99ac;
        text-align: center;
        width: 10%;
        padding: 0.5%;
    }

</style>
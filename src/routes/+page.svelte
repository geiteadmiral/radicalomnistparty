<script>
    //andre svelte filer
    import Gibby from "./gibby.svelte";
    import Aboutus from "./aboutus.svelte";
    import Images from "./images.svelte";
    import Boxes from "./boxes.svelte";
    import Faq from "./FAQ.svelte";


    //overganger
    //import Typewriter from 'svelte-typewriter';     //npm i -D svelte-typewriter
  //  import { concurrent } from 'svelte-typewriter'
    import { onMount } from "svelte";
    import { fly } from 'svelte/transition';
    import { fade } from "svelte/transition";
    import { slide } from "svelte/transition";

    //funksjon som starter hver gang siden lastes inn
    let loadTransition = false
    onMount(() => loadTransition = true);

    
</script>

<div class = "mainpage" id ="home">
    <div class = "front">
        <div> <!--forskjellige overganger, kommer opp når siden lastes inn-->
            {#if loadTransition}
            <h1 in:slide="{{duration: 2000}}">
                Radical Omnist Party
            </h1> 
            <h3 in:fly="{{ y: 200, duration: 2000, delay: 1000 }}">
                Radical Omnist Party
            </h3> 
            <p in:fade="{{duration: 2000, delay: 2000 }}">Wouldn’t it be great to create a world where everyone gets their opinion heard (while also being completely silenced)? Where all political ideologies , no matter how extreme or absurd, can combine into a perfect utopia (or dystopia)? Radical Omnist Party, or ROMP for short, offers the perfect solution to all silly world conflicts (and creates new and larger ones), by believing in and enforcing everything. </p>
            <button in:slide="{{delay: 3000}}">
                <a href="/learnmore">Learn more</a>
            </button>
            {/if}

        </div>
        {#if loadTransition}
        <div in:fade="{{duration: 2000, delay: 2000 }}">
            <!--Denne er tom nå, men i teorien linkes siden "gibby" til-->
            <Gibby></Gibby>
        </div>
        {/if}
    </div>
    <!--linker til de forskjellige sidene-->
    <div id = "aboutus">
        <Aboutus></Aboutus>
    </div>
    <div id = "values">
        <Boxes></Boxes>
    </div>
    <div id = "logistics">
        <Images></Images>
    </div>
    <div id = "faq">
        <Faq></Faq>
    </div>

    <footer>
        ⓒRadical Omnist Party 2023
    </footer>



</div>


<style>

/*Legger til en margin på hele innholdet fordi navbaren er der*/
.mainpage {
    margin-left:11vw;
}


/*Styler forsiden (det som kommer opp først)*/
.front {
    padding-left: 7vw;
    padding-right: 5vw;
    padding-top: 20vh;
    display: grid;
    grid-template-columns: 6fr 2fr;
    height: 100vh;
}

.front p {
    font-size: 2vh;
}

.front button {
    margin-top: 3vh;
    border: 0.2vw rgb(98, 157, 141) solid;

    box-shadow: none;
    background: none;
    font-size: 4vh;
    padding: 1.5vh;
}

.front a {
    color: rgb(98, 157, 141);
    text-decoration: none;
}

/*Footer*/

footer{
    width: 89vw;
    height: 5vh;
    margin-top: 10vh;
    background-color: rgb(98, 157, 141);
    color: black;
    text-align: center;
    padding-top: 2vh;

}





</style>
<!--Layout er felles for alle sidene-->
<script>

    //overganger
    import { scale } from "svelte/transition";
    import { slide } from "svelte/transition";

   //funksjoner som styrer darkmode og light mode
    let dark = false

    function toggle() {
        window.document.body.classList.toggle('dark-mode')
    }

    function lightMode(){
        dark = true
    }

    function darkMode(){
        dark = false
    }


    //til å åpne og lukke contact-modalen + et varsel som kommer opp når man trykker på submit
    let showContact = false

    function openContact(){
        showContact = true
    }

    function close(){
        showContact = false
    }

    function submit(){
        alert("Question submitted.")
    }

    //åpner og lukker menyen
    let menu = false

    function showMenu() {
        menu = true
    }

    function closeMenu () {
        menu = false
    }

    


    </script>


<body>
    <!--Navbaren-->
    <nav class = "navbar">
            <a href="/"><img src="logo.png" alt=""></a>
        <div>
            <!--Forskjellig knapp avhenig av om dark mode er på eller av-->
            {#if !dark}
            <button on:click={toggle} on:click={lightMode }>
                <div class="lightmode">
                    <i class="fa-solid fa-moon" ></i>
                    <p>Darkmode</p>
                </div>
            </button>
            {:else}
            <button on:click={toggle} on:click={darkMode}>
                <div class="darkmode">
                    <i class="fa-solid fa-sun" ></i>
                    <p>Lightmode</p>
                </div>
            </button>
            {/if}
        </div>

        <!--forskjellige ting vises avhenging av om menu true eller false-->
        {#if !menu}
        <div>
            <button on:click={showMenu}> 
                <i class="fa-solid fa-bars"></i>
                <p>Menu</p>
            </button>
        </div>
        {:else}
        <div>
            <div>
                <button on:click={closeMenu}>
                    <i class="fa-solid fa-x"></i>
                    <p>Menu</p>
                </button>
            </div>
            <!--Link til forskjellige steder på nettsiden-->
            <div in:slide={{duration: 100}} class = "menu">
                <a href="/"><p>Home</p></a>
                <a href="/#aboutus"><p>About Us</p></a>
                <a href="/#values"><p>Core Values</p></a>
                <a href="/#logistics"><p>Logistics</p></a>
                <a href="/#faq"><p>FAQ</p></a>
            </div>
        </div>
        {/if}

        <!--Knapp hvor man kan åpne modalen-->
        <button on:click={openContact}>
            <div class="contact">
                <div>
                    <p>Contact Us</p>
                </div>
                <div>
                    <i class="fa-solid fa-envelope"></i>
                </div>
        </div>
        </button>
    </nav>
</body>

<!--Modalen, vises bare om showContact er true-->
{#if showContact}
<div class ="popup box" transition:scale={{duration: 300}}>
    <div>
        <div class ="close"><button on:click={close}>&times;</button></div>
        <div>
            <h3>Do you have any questions?</h3>
            <p>If you have any questions about ROMP, write them below to contact Radical Omnist Party Europe (ROMPE).
                We will make sure to not respond in 3-5 business days!
            </p>
            <!--Input form hvor man kan skrive-->
            <form>
                <label for="email">Email address:</label><br>
                <input type="email" id = "email" name="email" placeholder="Enter an email address..." > <br>
                <label for="question">Question:</label><br>
                <textarea name = "question" id="question" placeholder="Enter your question..."></textarea>
            </form>
            <!--ikke en faktisk submit knapp som del av inputet fordi jeg har ingen backend-->
            <button class ="submit" on:click={submit}>Submit</button>
        </div>
    </div>
</div>
{/if}
 
<!--slot slik at man kan putte innholdet fra de andre sidene her-->
<slot></slot>

<style>

/*Styler hele bodyen*/
body {
    margin: 0;
    font-family: Arial, Helvetica, sans-serif;
    zoom: 100%
}

/*Mørk og lyd modus*/
:global(body) {
		background-color: #e7e6e6;
		transition: background-color 0.3s
	}
:global(body.dark-mode) {
    background-color: rgb(59, 57, 57);
    color: white;
}

/*Størrelsen til de forskjellige overskriftene*/
:global(h1) {
    font-size: 7vh;
}

:global(h2) {
    font-size: 4vh;
    text-align: center;
}

:global(h4){
    font-size: 2.5vh;
}



/*Navbaren på mørk og lys modus*/
:global(nav){
    background-color: #fafafa;
}

:global(.dark-mode nav){
    background-color: rgb(24, 24, 24);
    color: white;
}

/*Fargen til knappen for fargetemaet, avhenig av mørk eller lys modus*/
.darkmode i{
    color: rgb(255, 222, 6);

}

.lightmode i{
    color: rgb(76, 43, 160);
}




nav{
    position: fixed;
    width: fit-content;
    height: 100vh;
    padding: 2vw;
    display: flex;
    flex-direction: column; 
    padding: auto;
    text-align: center;


}

/*Spesifikt alle divene som er direkte inne i en nav*/
nav > div {
    border-bottom: 1px solid rgb(106, 106, 106);
}


nav button {
    background: none;
    border: none;
    text-align: center;
}

/*Ikonene der*/
nav i {
    color: rgb(98, 157, 141);
    background: none;
    font-size: 2.5vw;
    margin: 1vw;

}

nav p {
    font-size: 1.8vh;
    color: rgb(106, 106, 106);
}

/*Om man klikker over linkene eller knappene*/
a:hover{
    opacity: 0.6;
}

:global(button:hover){
    opacity: 0.8;
    cursor: pointer;
}



a {
    text-decoration: none;
    color: black;
}

/*Kontakt tingen*/
.contact {
    position: fixed;
    bottom: 20px;
    display: flex;

}

.contact i {
    font-size: 2vh;
}


/*Modalen*/
.popup {
    z-index: 1;
    position: fixed;
    margin: auto;
    width: 35vw;
    height: fit-content;
    margin-left: 32.5vw;
    margin-top: 30vh;
    padding: 1.5%;

}



/*Lukkeknappen til modalen*/
.close {
    position: fixed;
    margin-left: 33vw;
    margin-top: -3vh;

}

.close button {
    width: 2vw;
    height: 2vw;
    border-radius: 20px;
    font-size: 1vw;
    text-align: center;
    background-color: rgb(98, 157, 141);
    border: none;
}

/*Form*/
#email {
    width: 15vw;
    margin-bottom: 2vh
}
#question {
    width: 27vw;
    height: 7vh;
}

textarea{
    font-family: Arial, Helvetica, sans-serif;
}

.submit{
    border: 0.2vw rgb(98, 157, 141) solid;

    box-shadow: none;
    background: none;
    font-size: 2vh;
    padding: 1vh;
    color: rgb(98, 157, 141);
}

/*Bildet*/
nav img {
    border: none;
    margin-bottom: 5vh;
    width: 7vw;
    margin-left: auto;
    margin-right: auto;
}

/*Alle bildene på nettsiden*/
:global(img){
    border-radius: 10px;
}



</style>
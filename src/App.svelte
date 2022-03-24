
<!-- Additional Fonts -->
<link href="https://fonts.googleapis.com/css?family=Teko" rel="stylesheet" type="text/css">


<script>
    import Spinner from "./Spinner.svelte";
    import Results from "./Results.svelte";
    import Search from "./Search.svelte";
    import { isHomePage } from "./stores.js";
    import { bubbleSearch } from "./stores.js";
    import { promise } from "./stores.js";
    import { timer } from "./stores.js";
    import { fade } from 'svelte/transition';

    //  Sleep function
    function sleep(ms) {
    return new Promise(resolve => setTimeout(resolve, ms));
} 
    // Makes bubbles go away after 10 seconds
    function checker() {
        if ($timer) {
            $timer = false
            sleep(10000).then(() => { $bubbleSearch = false })
            
        }
    }
    
    setInterval(checker, 1000)

</script>

<main>
    
	<div id="flexcontainer">
        <!-- Top Bar -->        
        {#if $isHomePage == true}
            <div class="homenav">
                <h1 id="title">deep search</h1>
                <Search id="searchBar" />
            </div>
        {:else}
            <div class="topnav">
                <h1 id="title">deep search</h1>
                <Search id="searchBar" />
            </div>
        {/if}
		<div id="mainSearchPage">
		{#await $promise}
			<Spinner />
		{:then result}
			<Results json={result} />
		{:catch error}
			<p style="color: red">{error.message}</p>
		{/await}
		</div>

        {#if $bubbleSearch == true}
            <div id="contaierB">
                <svg id="bubbe"  viewBox="50 0 90 80" xmlns="http://www.w3.org/2000/svg" version="1.1">
                    <circle cx="100" cy="50" r="30" stroke="white" stroke-width="4" fill="none" />
                    <circle cx="85" cy="45" r="1.75" stroke="white" stroke-width="2" fill="white" />
                    <circle cx="95" cy="30" r="3" stroke="white" stroke-width="2" fill="white" />
                </svg>
                <svg  id="bubbe2" viewBox="50 0 130 90" xmlns="http://www.w3.org/2000/svg" version="1.1">
                    <circle cx="100" cy="50" r="30" stroke="white" stroke-width="4" fill="none" />
                    <circle cx="85" cy="45" r="1.75" stroke="white" stroke-width="2" fill="white" />
                    <circle cx="95" cy="30" r="3" stroke="white" stroke-width="2" fill="white" />
                </svg>
                <svg  id="bubbe3"  viewBox="50 0 100 100" xmlns="http://www.w3.org/2000/svg" version="1.1">
                    <circle cx="100" cy="50" r="30" stroke="white" stroke-width="4" fill="none" />
                    <circle cx="85" cy="45" r="1.75" stroke="white" stroke-width="2" fill="white" />
                    <circle cx="95" cy="30" r="3" stroke="white" stroke-width="2" fill="white" />
                </svg>
        </div>
        {:else}
            <p></p>
        {/if}
        
       

	</div>
    
</main>

<meta content="width=device-width, initial-scale=1" name="viewport" />

<style>
    /* Bubble Container to easier group together */
    
    
    #contaierB {
        position: relative;
        z-index: -90;
        opacity: 69%;
        box-sizing: content-box;
        width: 100%;
        height: 100%;
    }
    /* CSS for bubble 1 */
    #bubbe {
        animation: MoveUpDown 12s linear;
        position: absolute;
        left: 20vw;
        bottom: 0;
        width: 100px;
        height: 100px;
    }
    /* CSS for bubble 2 */
    #bubbe2 {
        animation: MoveUpDown 16s linear;
        position: absolute;
        left: 80vw;
        bottom: 0;
        width: 60px;
        height: 60px;
    }
    /* CSS for Bubble 3 */
    #bubbe3 {
        animation: MoveUpDown 20s linear;
        position: absolute;
        left: 50vw;
        bottom: 0;
        width: 60px;
        height: 60px;
    }
    /* Animation for bubble */
    @keyframes MoveUpDown {
        
    0%{
        bottom: 0;
    }
    50% {
        bottom: 100vh;
    }
    100%{
        bottom: 100vh;
    }
    }

    

    /* Overall background */
    :global(body) {
        background-image: linear-gradient(0deg, #182848, #041562,#2980b9);
        backdrop-filter: blur(20px);
        padding: 0;
        margin: 0;
    }
    

    /* CSS for the first search bar */
    .homenav {
        display: flex;
        justify-content: start;
        align-items: center;
        flex-direction: column;
        position: absolute;
        z-index: 1;
        border-radius: 20px;
        width: 50%;
        top: 300px;
        background-color: rgb(33, 50, 94, 1);
        box-shadow: 0 10px 20px rgba(0,0,0,0.05), 0 6px 6px rgba(0,0,0,0.25);
    }
    
    
    /* Top Bar CSS */
    .topnav {
        display: flex;
        justify-content: start;
        align-items: center;
        flex-direction: column;
        position: fixed;
        z-index: 1;
        width: 100%;
        height: 125px;
        background-color: rgb(18, 71, 143, .4);
        box-shadow: 0 10px 20px rgba(0,0,0, .0  5), 0 6px 6px rgba(0,0,0,0.05);    
    }

    
        /* Overall CSS to center things easier */
    #flexcontainer {
        display: flex;
        justify-content: start;
        align-items: center;
        flex-direction: column;
        height: 100vh;
        box-sizing: content-box;
        width: 100%;
    }

    /* Title CSS */
    #title {
        margin-top: 0px;
        font-family: Teko;
        font-size: 50px;
        margin-bottom: 0px;
        position: absolute;
        text-transform: uppercase;
        color: aliceblue;
    }
    /* CSS to make things easier */
    #mainSearchPage {
        height: 100vh;
        width: 100vw;        
        display: flex;
        justify-content: start;
        align-items: center;
        flex-direction: column;
        padding-top: 10%;
        padding-left: 10%;
        padding-right: 10%;
        padding-bottom: 5%;
        box-sizing: border-box;
    }



    @keyframes gradient {
        0% {
            background-position: 0% 50%;
        }
        50% {
            background-position: 100% 50%;
        }
        100% {
            background-position: 0% 50%;
        }
    }

    @media (max-width: 600px){ 

    .homenav {
        width: 75%;
        position: fixed;
        top: 40%;
    }

    }
</style>

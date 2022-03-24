<link href="https://fonts.googleapis.com/css?family=Oswald" rel="stylesheet" type="text/css">

<script>


    export let json;
    import { dataset_dev } from "svelte/internal";
    import { fly, fade, slide, draw } from "svelte/transition";
    import { isHomePage } from "./stores.js";

    let test = ""

    // Made By lil Melvin, Re makes the URL into looking more like a google search
    function processUrl( url ){
        let split = url.split("/");
        let output = "";

        split.forEach((element, index) => {
            if ( index == 0 ){
                output +=  element + "//"

            } else if (index == 1){
                output += "";
            } else if (index + 1 == split.length){
                output += element;
            } else {
                output += element + " " + ">" + " ";
            }
        });
        return output;
    }
    // Limits the amount characters that can be displayed from one description
    function descLimiter(desc) {
        let limiter = desc
        let newDesc =""
        if ( limiter.length > 200 ) {
           newDesc = limiter.substr(0, 200) + "..."
        }
        else {
            newDesc = limiter
        }
        return newDesc
    }
    // Removes "" at the begining and end of name in JSON search result.
    function nameSplitter(name) {
        let Splitter = name
        Splitter = Splitter.replace("\"", "")
        return Splitter
    }


    
</script>
<!-- Handles the JSON data -->
{#if json && "data" in json && "items" in json.data && json.data.items.length > 0}
    <div id="results">
        {#each json.data.items as item}
            <!-- Gives correct listing depending on if there is a description or not -->
            {#if item.description == undefined}
            <!-- This Has no description -->
            <p transition:fly="{{ y: 100, duration: 1000 }}"><a href="{item.url}" target="_blank">{processUrl(item.url)}</a><br><br> {nameSplitter(item.name)}
                <br><br> Description: Not available  <br><br>Published: {item.published_at}  </p>
            {:else}
            <!-- This has a desctiption -->
            <p transition:fly="{{ y: 100, duration: 1000 }}"><a href="{item.url}" target="_blank">{processUrl(item.url)}</a><br><br> {nameSplitter(item.name)}
                <br><br>  {descLimiter(item.description)}  <br><br>Published: {item.published_at}  </p>
            {/if}
        {/each}
    </div>
{:else if json}
<!-- If search failed will show this -->
    <div id="failedSearch" >
        <p  id="failed" in:fade>Failed to find: {JSON.stringify(json.data.q)} <br><br> Closest match: <a style="text-decoration: underline;" href="https://www.youtube.com/watch?v=dQw4w9WgXcQ&ab_channel=RickAstley" target="_blank">{JSON.stringify(json.data.q)}</a> </p>
    </div>
{/if}  


<style>


    #results {
        margin-top: 100px;
    }
    
    /*  General CSS for structure */
    div {
        
        display: flex;
        justify-content: start;
        align-items: center;
        flex-direction: column;
        overflow-y: scroll;
        box-sizing: border-box;
        padding-left: 10%;
        padding-right: 10%;
        max-width: 100%;
        position: relative;
        
    }

    /* CSS failed Search */
    #failedSearch {
        top: 20vh;
    }
    /* Normal CSS for the search Results */
    p {
        color: white;
        border-radius: 25px;
        background-color: rgb(17, 70, 143, 0.4);
        border: 2px solid #035397;
        padding: 20px;
        width: 100%;
        box-sizing: border-box;
        word-wrap: break-word;
        opacity: 0.75   ;
        font-family: Oswald;
    }

    /* When hovering over search result it will highligth the one the crusor is located on */
    p:hover {
        background-color: rgb(57, 110, 176, .6);
    }

    /* CSS when failing to find something */
    #failed {
        color: white;
        background-color: #21325E;
        
    }

    /* CSS for link of URL */
    a {
        color: white;
    }
    /** https://onaircode.com/html-css-custom-scrollbar-examples/ */
    ::-webkit-scrollbar {
        position: relative;
        width: 15px;
        height: 15px;
    }
    ::-webkit-scrollbar-track {
        border-radius: 10px;
        background-color: rgba(4, 21, 98, 0.4);
    }
    ::-webkit-scrollbar-thumb {
        background-image: linear-gradient(45deg, #00aeff, #a68eff);
        background-image:-webkit-linear-gradient(45deg,rgba(255,255,255,.3) 20%,transparent 20%,transparent 40%,rgba(255, 255, 255, 0.3) 40%,rgba(255,255,255,.3) 60%,transparent 60%,transparent 80%,rgba(255, 255, 255, 0.3) 80%);
        border-radius: 10px;
        -webkit-box-shadow: rgba(0, 0, 0, 0.12) 0 3px 13px 1px;  
    }
    ::-webkit-scrollbar-thumb:hover {
        background-image: linear-gradient(45deg, red, green);
        background-image:-webkit-linear-gradient(45deg,rgba(255,255,255,.3) 20%,transparent 20%,transparent 40%,rgba(255, 255, 255, 0.3) 40%,rgba(255,255,255,.3) 60%,transparent 60%,transparent 80%,rgba(255, 255, 255, 0.3) 80%);
        border-radius: 10px;
        -webkit-box-shadow: rgba(0, 0, 0, 0.12) 0 3px 13px 1px;  
        
    }
</style>

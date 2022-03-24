<script>
    import { promise, timer } from "./stores.js";
    import { isHomePage} from "./stores.js";
    import { bubbleSearch } from "./stores.js";

    
    let question;
    async function search() {
        const res = await fetch(
            `https://demo.dataverse.org/api/search?q=` + question
        );
        const json = await res.json();

         if (res.ok) {
            console.log(json)
            $bubbleSearch = true
            $isHomePage = false
            $timer = true
            return json;
        } else {
            throw new Error(json);
        } 
    }
</script>

<div>
    <form id="bar"
        on:submit|preventDefault={() => {
            $promise = search();
        }}
    >
        <input id="inputBar" bind:value={question} placeholder="Search" />
    </form>
</div>

<style>
    div {
        display: flex;
        gap: 10px;
        width: 45%;
        justify-self: center;
        align-items: center;
    }

    form,
    form input {
        width: 100%;
    }

    /* Search Bar CSS */
    #inputBar{
        margin-top: 65px;
        height: 45px;
        color: white;
        background-color: #3E497A;
        border-color: #3e497a00;
        border-radius: 20px;
        border-style: groove;
        outline: none;
        padding-left: 20px;
        
    }
    
</style>

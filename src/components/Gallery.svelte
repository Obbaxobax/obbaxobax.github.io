<script lang="ts">
    export let imageURLs: string[];
    export let Class: string = "";
    export let context: string[] = [];

    let index: number = 0;

    function nextImage(direction: number){
        if(direction > 0 && imageURLs.length - 1 == index){
            index = 0;
            return;
        }
        else{
            index = direction > 0 ? index + 1 : index != 0 ? index - 1 : index = imageURLs.length - 1;
            return;
        }
    }
</script>



<div class="w-full sm:w-[95%] h-fit bg-black bg-opacity-10 mt-2 flex flex-row rounded-md {Class}">
    <button class="{imageURLs.length == 1 ? "bg-opacity-10 bg-slate-500 text-gray-700" : "bg-opacity-25 bg-white"} w-10 h-80 mr-2 rounded-l-md button" on:click={() => nextImage(-1)}>{"\<"}</button>
    {#if imageURLs[index].includes("youtube.com")}
        <div class="h-80 mx-auto py-2 flex flex-col justify-center">
            {#key index}
                <iframe class="max-h-[304px] w-[95%] xl:w-[570px] mx-auto" src={imageURLs[index]} title="Youtube"/>
            {/key}
        </div>
    {:else}
        <div class="h-80 max-w-[80%] mx-auto py-4 flex flex-col justify-center">
            {#key index}
                <img class="max-h-[304px] {context[index] && context[index] != "" ? "h-[276px]" : "h-full"}" src="{imageURLs[index]}" alt="not found"/>
                {#if context[index] && context[index] != ""}
                    <p class="h-7 px-1 pb-1 rounded-b-md bg-black bg-opacity-10 text-center">
                        {context[index]}
                    </p>
                {/if}
            {/key}
        </div>
    {/if}
    <button class="{imageURLs.length == 1 ? "bg-opacity-10 bg-slate-500 text-gray-700" : "bg-opacity-25 bg-white"} w-10 h-80 ml-2 rounded-r-md" on:click={() => nextImage(1)}>{"\>"}</button>
</div>
<slot/>


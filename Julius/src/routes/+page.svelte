<script>
import TableRow from '../components/jsonRow.svelte';
import jsonArray from '../lib/store.js'

let titles = []

   
 function getJson(){   
    let obj =  document.getElementById("jsonText").value;
    const lines = JSON.parse(obj);
    jsonArray.set(Object.entries(lines))
    let toTranslate = []
    $jsonArray.forEach(function(r){
       toTranslate.push([r[1].short_description.value.fr])
       titles.push([r[0]])
    })
    if (toTranslate.length == titles.length){
    } else {
        console.log("Not all the items have a description value FR")
    }
}   

</script>

<div class="container">

    <div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
        <div class="modal-dialog modal-xl">
          <div class="modal-content">
            <div class="modal-header">
              <h1 class="modal-title fs-5" id="exampleModalLabel">JSON file</h1>
              <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
            </div>
            <div class="modal-body">             
                <textarea class="form-control" rows="40">
                    {JSON.stringify({$jsonArray},null,2)}
                </textarea>
            </div>
            <div class="modal-footer">
              <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
              <button type="button" class="btn btn-primary">Save changes</button>
            </div>
          </div>
        </div>
      </div>
           

    <div class="row p-4">
        <div class="col"><h1>Hello Julius</h1></div>
        <div class="input-group">
            <span class="input-group-text">API Deepl</span>
            <input type="text" class="form-control" id="apiKey" value="5166a5ce-5246-e6e4-6893-603327f535d4:fx">
          </div>
</div>

{#if $jsonArray == undefined} 
 <div class="row p-4">
        <div class="col"> Paste JSON here <br> 
            <textarea class="form-control" rows="10" id="jsonText"></textarea>
        </div>
    </div>
        <div class="row p-4">
        <button type="button" class="btn btn-primary" on:click|once={getJson} >Load JSON</button>
</div>
 {:else}
 <div class="row p-4">
    <div class="col"><button type="button" class="btn btn-success" data-bs-toggle="modal" data-bs-target="#exampleModal">Show JSON</button></div>
    </div>
    {#each $jsonArray as posts}
       <TableRow post={posts}></TableRow>
    {/each}

{/if}


    </div>       









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
        translate(toTranslate)
    } else {
        console.log("Not all the items have a description value FR")
    }
}   

function translate(toTranslate) {
		/* let translatedArrayEs = [];
        let translatedArrayEn = [];
		async function translateNow(item) {
			let urlApi =
				'https://api-free.deepl.com/v2/translate?auth_key=75d45bb4-a842-c6de-9b11-cb903d1eb70a:fx&';
			let paramsLangToEs = '&source_lang=FR&target_lang=ES';
            let paramsLangToEn = '&source_lang=FR&target_lang=EN';
			let urlToEs = urlApi.concat('text=', encodeURIComponent(item), '', paramsLangToEs);
            let urlToEn = urlApi.concat('text=', encodeURIComponent(item), '', paramsLangToEn);
			try {
				const responseEs = await fetch(urlToEs);
				const dataEs = await responseEs.json();
				const translationEs = await dataEs.translations[0].text;
				translatedArrayEs.push(translationEs);

                const responseEn = await fetch(urlToEn);
				const dataEn = await responseEn.json();
				const translationEn = await dataEn.translations[0].text;
				translatedArrayEn.push(translationEn);

				if (translatedArrayEn.length == toTranslate.length) {
					generateView(translatedArrayEs,translatedArrayEn)
				}
			} catch (error) {
				console.log(error);
			}
		}
		toTranslate.map(translateNow); 
	}


   */

}




</script>

<div class="container">

    <div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
        <div class="modal-dialog modal-fullscreen">
          <div class="modal-content">
            <div class="modal-header">
              <h1 class="modal-title fs-5" id="exampleModalLabel">Modal title</h1>
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
</div>
{#if $jsonArray == undefined} 
 <div class="row p-4">
        <div class="col"> Paste JSON here <br> 
            <textarea class="form-control" rows="25" id="jsonText"></textarea>
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









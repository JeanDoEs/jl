<script>
    export let post
    import jsonArray from '../lib/store.js'
    let titles = []


function translate(e) {  
    var apiDeepl = document.getElementById("apiKey").value;
    var itemInJson = e.target.id; 
    var translationFR = document.getElementById(itemInJson + "+_fr").value;
    async function translateNow(item) {
        let urlApi =
            'https://api-free.deepl.com/v2/translate?auth_key='+apiDeepl+'&';
        let paramsLangToEs = '&source_lang=FR&target_lang=ES';
        let paramsLangToEn = '&source_lang=FR&target_lang=EN';
        let urlToEs = urlApi.concat('text=', encodeURIComponent(item), '', paramsLangToEs);
        let urlToEn = urlApi.concat('text=', encodeURIComponent(item), '', paramsLangToEn);
        try {
            const responseEs = await fetch(urlToEs);
            const dataEs = await responseEs.json();
            const translationEs = await dataEs.translations[0].text;
            console.log(translationEs)
            document.getElementById(itemInJson + "+_es").value = translationEs

            const responseEn = await fetch(urlToEn);
            const dataEn = await responseEn.json();
            const translationEn = await dataEn.translations[0].text;
            document.getElementById(itemInJson + "+_en").value = translationEn
            console.log(translationEn)

            
        } catch (error) {
            console.log(error);
        }
    }
    translateNow(translationFR); 
}

function saveJson(e){
    var itemInJson = e.target.id;
    var translationEN = document.getElementById(itemInJson + "+_en").value;
    var translationES = document.getElementById(itemInJson + "+_es").value;  
    $jsonArray.forEach(function(r){
       titles.push([r[0]])
    })  
    var itemPostition = titles.flat().indexOf(itemInJson);
    $jsonArray[itemPostition][1].short_description.value.en = translationEN;
    $jsonArray[itemPostition][1].short_description.value.es = translationES;
}

function hide(e){
    var itemInJson = e.target.id;
    var rows = document.getElementById(itemInJson + "+_row")
    var boxes = rows.getElementsByClassName('rowWithInfo');
    for (const box of boxes) {
        if (box.style.display === "none") {
            box.style.display = "flex";
         } else {
           box.style.display = "none";
    }
}  

}

</script>

<div class="container text-center">
<div class="row p-4" id="{post[0]}+_row">
    <div class="col">
    <h2>{post[0]} </h2>  
</div>
 <div class="col">
    <button type="button" class="btn btn-primary" id={post[0]} on:click={saveJson}>Save to JSON</button>
    <button type="button" class="btn btn-success" id={post[0]} on:click|once={translate}>Translate</button>
    <button type="button" class="btn btn-secondary" id={post[0]} on:click={hide}>Hide</button>
</div>
 <div class="rowWithInfo row p-4">   
    <div class="col"> FR: <br><textarea class="form-control" rows="8" id="{post[0]}+_fr">{post[1].short_description.value.fr}</textarea></div>
    <div class="col"> EN: <br> <textarea class="form-control" rows="8" id="{post[0]}+_en">{post[1].short_description.value.en}</textarea> </div>
    <div class="col"> ES: <br> <textarea class="form-control" rows="8" id="{post[0]}+_es" >{post[1].short_description.value.es}</textarea> </div>
</div>
</div>
<div class="row justify-content-md-center rowWithInfo p-4">
  
</div>
<hr>  
</div>  


<style>

    .hide {
        display: none;
    }
</style>
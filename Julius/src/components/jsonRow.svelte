<script>
    export let post
    import jsonArray from '../lib/store.js'
    let titles = []


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
</script>

<div class="row p-4" id="row">
 <h2>{post[0]} </h2>       
 <div class="col"> FR: <br><textarea class="form-control" rows="8" id="{post[0]}+_fr">{post[1].short_description.value.fr}>  </textarea> </div>
    <div class="col"> EN: <br> <textarea class="form-control" rows="8" id="{post[0]}+_en">{post[1].short_description.value.en}</textarea> </div>
        <div class="col"> ES: <br> <textarea class="form-control" rows="8" id="{post[0]}+_es" >{post[1].short_description.value.es}</textarea> </div>
</div>
<div class="row p-4">
    <button type="button" class="btn btn-primary" id={post[0]} on:click={saveJson}>Save to JSON</button>
</div>
<hr>    
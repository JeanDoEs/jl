<script>
    import lines from "../lib/models_tracmax_es.json"
    var array = Object.entries(lines)
   
    let toTranslate = []
    let titles = []

    array.forEach(function(r){
       toTranslate.push([r[1].short_description.value.fr])
       titles.push([r[0]])
    })

    if (toTranslate.length == titles.length){
        translate(toTranslate)
    } else {
        console.log("Not all the items have a description value FR")
    }
    

function translate(toTranslate) {
		let translatedArrayEs = [];
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


    function generateView(translatedArrayEs,translatedArrayEn){

        for (let i = 0; i < array.length; i++) {
           array[i][1].short_description.value.en = translatedArrayEn[i]
           array[i][1].short_description.value.es = translatedArrayEs[i]
        }
    
    }

</script>


<div class="container">



<h1>Hello Julius</h1>
{#each array as post}

<div class="row p-4">
			<h2>{post[0]}</h2>
        
         <div class="col"> FR: <br><textarea class="form-control" rows="8">{post[1].short_description.value.fr}>  </textarea> </div>
            <div class="col"> EN: <br> <textarea class="form-control" rows="8">{post[1].short_description.value.en}</textarea> </div>
                <div class="col"> ES: <br> <textarea class="form-control" rows="8">{post[1].short_description.value.es}</textarea> </div>

        </div>
        <hr>

        
            
            
		{/each}


    </div>       







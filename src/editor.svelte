<script>
	var minRows = 10;
	var maxRows;
	$: minHeight = `${1 + minRows * 1.2}em`;
	$: maxHeight = maxRows ? `${1 + maxRows * 1.2}em` : `auto`;

     var errors = "";
     var scheme = "";
     var url = "";
     var params = "";
     var options = "";

     function makeReq() {
          errors = "";
          var urlToFetch = scheme + '://' + url + '?' + params;
          try {
               var optionsJSON = JSON.parse(options);
               fetch(urlToFetch, optionsJSON)
               .then(response => response.json())
               .then(data => errors=data)
               .catch((error) => {errors = error});
          } catch (e) {
               errors = e;
          }
     }
</script>

<div class="editor">
     <form on:submit|preventDefault={makeReq}>
          <select required class="selector" bind:value={scheme}>
               <option disabled selected hidden value="">Select a URL scheme</option>
               <option value="http">http</option>
               <option value="https">https</option>
          </select>
          <span class="monospace">://</span>
          <input required autocomplete="off" autocorrect="off" autocapitalize="off" spellcheck="false" class="full-width monospace" type="text" placeholder="URL" bind:value={url}>
          <input required autocomplete="off" autocorrect="off" autocapitalize="off" spellcheck="false" class="full-width monospace" type="text" placeholder="parameters" bind:value={params}>
     
          <div class="container">
               <pre
                    aria-hidden="true"
                    style="min-height: {minHeight}; max-height: {maxHeight}"
               >{options + '\n'}</pre>
          
               <textarea required autocomplete="off" autocorrect="off" autocapitalize="off" spellcheck="false" class="non-resizable full-width monospace" placeholder="options" bind:value={options}></textarea>	
          </div>

          <input type="submit" class="make-request-button" value="Make Request ➡️">
     </form>
     <div class="errors">
          {errors}
     </div>
</div>

<style>
	.editor {
          position: fixed;
          width: calc(50% - 20px);
          background-color: var(--main-background);
          height: calc(100% - 20px);
          padding: 10px;
     }
     .non-resizable {
          resize: none;
     }
     .full-width {
          width: 100%;
     }
     .monospace {
          font-family: 'Courier New', Courier, monospace;
     }
     .selector {
          -webkit-appearance: default-button;
          appearance: default-button;
     }
     .make-request-button {
          width: 100%;
          background-image: linear-gradient(#0087ff, #006cff);
          color: #fff;
          border: #60a2ff 1px solid;
     }
     input, textarea {
          border-radius: 5px;
     }
     .container {
		position: relative;
	}
	
	pre, textarea {
		font-family: inherit;
		box-sizing: border-box;
		line-height: 1.2;
		overflow: hidden;
	}
	
	textarea {
		position: absolute;
		width: 100%;
		height: 100%;
		top: 0;
		resize: none;
	}
     .errors {
          color: #f00;
     }
</style>
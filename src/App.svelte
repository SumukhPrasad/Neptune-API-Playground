<script>
	import Viewer from "./viewer.svelte";
     import Editor from "./editor.svelte";
</script>


<svelte:head>
     <title>Neptune</title>
     <style> 
          :root {
               --main-background: #fff;
               --viewer-background: #eee;
               --default-color: #333;
          }
          
          
          @media (prefers-color-scheme: dark) {
               :root {
                    --main-background: #333;
                    --viewer-background: #222;
                    --default-color: #eee;
               }
          }

          body {
               border: 0;
               padding: 0;
               overflow: hidden;
               background-color: var(--main-background);;
               color: var(--default-color);
          }
     }
     </style>
     <meta name="theme-color" media="(prefers-color-scheme: light)" content="#ffffff">
     <meta name="theme-color" media="(prefers-color-scheme: dark)" content="#333">
</svelte:head>
<main>
     <Editor />
     <Viewer />
</main>

<style>
	
</style>
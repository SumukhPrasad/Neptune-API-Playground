<script>
     import {sharedData} from "./shared.js";
     var viewerMainContent = "";
     sharedData.subscribe(value => {
          viewerMainContent = JSON.stringify(value);
     });
</script>

<div class="viewer">
     {viewerMainContent}
</div>

<style>
	.viewer {
          font-family: 'Courier New', Courier, monospace;
          position: fixed;
          width: calc(50% - 28px);
          background-color: var(--viewer-background);
          height: calc(100% - 36px);
          padding: 10px;
          margin-top: 8px;
          margin-right: 4px;
          margin-bottom: 8px;
          margin-left: 50%;
          border-radius: 5px;
          box-shadow: 0 5px 5px rgba(0, 0, 0, 0.25);
     }
</style>
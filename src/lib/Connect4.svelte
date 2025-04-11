<script lang=ts>
  export let fillColor: string ;
  export let row: number;
  export let col: number;
  export function update(newColor: string) {
    fillColor = newColor;
  }
</script>
<style>
div{
  height: 100%;
  width: 100%;
  background-color: #0000FF;
}
.Connect4{
  border:1px;
  border-style:solid;
  border-color:"#0000F0";
}

.inside{
  color: #000000;
  height: 50%;
  font-size: 50%;
  max-width: 50%;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  display: inline-block;
  border:10px;
  border-radius:50%;
}
</style>
<div class=Connect4>
  
  <div class=inside style="background-color: {fillColor};">
    [{col}, {row}]
  </div>
  <!-- <button on:click={() => update("#FF0000")} style="background-color: {fillColor};">Change Color to Red</button>
  <button on:click={() => update("#FFFF00")} style="background-color: {fillColor};">Change Color to Yellow </button> -->
</div>

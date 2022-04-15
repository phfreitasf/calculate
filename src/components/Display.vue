<template>
  <div class="display">
      {{ valor }}
      </div>
</template>

<script>
export default {
  name: "VDisplay",
  props:{
      valor : {type:String}
  }
};
</script>

<style>

.display
{
    grid-column: span 4;
    background-color: #0004;

    display: flex;
    justify-content: flex-end;
    align-items: center;
    font-size: 2.1em;
    padding: 20px;
    overflow: hidden;
}
</style>
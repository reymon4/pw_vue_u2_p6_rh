<template>
  <div class="options_container">
    <h3>Pokemon Options</h3>
    <ul>
      <li>1</li>
      <li>2</li>
      <li>3</li>
      <li>4</li>
    </ul>
  </div>
</template>

<script>
export default {};
</script>

<style scoped>
.options_container ul{
list-style: none;
}
li{
  border: 1px solid rgb(99, 188, 239);
  border-radius: 8vmin;
  margin-bottom: 10px;
  width: 250px;
  background: rgb(99, 188, 239);
  cursor: pointer;

}
li:hover{
  background: rgb(42, 115, 184);
  color: white;
  transition: 0.5s;
}
.options_container{
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>

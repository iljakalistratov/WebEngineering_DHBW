<template>
  <main>
    <div class="search">
      <input type="text" class="searchbar" placeholder="Ort eingeben">
    </div>

  </main>
</template>

<script>

export default {
  name: "App",
  data () {
    return{
      api_key: '1f3e379d7b4cbb2bbb0527cb6b3a654b'
    }
  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body{
  font-family: 'montserrat', sans-serif;
}

#app{
  background-image: url('./assets/cold.jpg');
  background-size: cover;
  background-position: bottom;
  transition: 0.6ms;
}

main{
  min-height: 100vh;
  padding: 25px;

  background-image: linear-gradient(to bottom, rgba(0, 0, 0, 0.1), rgba(0, 0, 0, 0.5));
}

.search {
  width: 100%;
  margin-bottom: 30px;
}

.search .searchbar {
  display: block;
  width: 100%;
  padding: 15px;
  color: #313131;
  font-size: 20px;

  appearance: none;
  border: none;
  outline: none;
  background: none;

  background-color: whitesmoke;
  border-radius: 15px;
}
</style>

<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router';
import { store, updateGesamtsumme, isloggedIn, updateIsloggedIn } from '@/store';

let gesamtPreis = () => {
  return store.value.warenkorb.reduce((total, item) => {
    return total + parseFloat(item.price_brutto) * item.quantity;
  }, 0).toFixed(2);
};

updateGesamtsumme();

let logOutAlert = () => {
  alert('Logout erfolgreich');
};
</script>

<template>
    <header>
      <nav>
        <div class="brand">Buchshop</div>

        <div class="nav-container">
            <div><RouterLink to="/" class="nav-link">Home</RouterLink></div>
            <div><RouterLink to="/katalog" class="nav-link">Katalog</RouterLink></div>
            <div><RouterLink to="/about" class="nav-link">About</RouterLink></div>
        </div>        
        
        <div class="searchbar-container">
          <input type="text" placeholder="Suche..." class="searchbar-input">
          <img src="../images/search-lens.png" class="search-button">
        </div>

        <div class="right-top">
          <div class="warenkorb-container">
              <RouterLink to="/warenkorb" class="nav-link">
                <img src="../../images/warenkorb.png" class="warenkorb_image"> ({{ gesamtPreis() }}€)
              </RouterLink>
          </div>
          <div class="button-container">
            <div v-if="isloggedIn === true" class="nav-link" @click="isloggedIn = false; updateIsloggedIn(false), logOutAlert()">
              <RouterLink to="/Login" class="login-button-text">Logout</RouterLink>
            </div>
            <div v-if="isloggedIn === false" class="nav-link">
              <RouterLink to="/Login" class="login-button-text">Login</RouterLink>
            </div>
          </div>
        </div>
      </nav>
    </header>
    <RouterView />
</template>

<style scoped>
.login-button-text{
  text-decoration: none;
  color: white;
  font-size: 150%;
}
header {
  display: block;
  background-color: black;
  color: white;
  position: fixed;
  width: 100%;
  top: 0;
  z-index: 1;
} 
nav{
  display: flex;
  justify-content: space-between;
  align-items: center;   
  padding: 5px;
  font-size: 250%;     
  border: 2px solid white; 
}
.brand {
  font-size: 1.5em;
  margin-right: 30px;
  padding: 0.1em;
  /* border: 2px solid red; */
}
.nav-container {
  display: flex;
  list-style: none;
  flex-grow: 1;
  padding: 0;  
  /* border: red 2px solid; */
}
.nav-link {
  margin: auto;
  margin-right: 1vw;
  text-decoration: none;
  color: white;
  position: relative;
}

.nav-link::before {
  content: '';
  position: absolute;
  bottom: 0;
  left: 0;
  width: 0;
  height: 2px;
  background-color: #c278ff;
  transition: width 0.3s ease; /* Füge eine sanfte Übergangsanimation hinzu */
}

.nav-link:hover::before {
  width: 100%;
}


.right-top{
  display: flex;

  margin: auto;
  position: absolute;
  right: 0;  
  /* border: 2px solid red; */
}
.button-container{
  display: flex;
  justify-content: flex-end;
  margin-right: 15px;
  list-style: none;
}
.warenkorb_image{
  min-width: 15%;
  max-width: 15%;
  position: relative;
  top: 5px;
}
.warenkorb-container{
  right: 5%;
  justify-content: flex-end;
  margin: auto;
  list-style: none;
}

.searchbar-container{
  display: flex;
  position: relative;
  margin: auto;

  width: 25%;
  height: 3vh;

  right: 25%;

  
  border: 2px solid white;
  border-radius: 100px;
  font-size: 1.5vh;

}

.searchbar-input{
  display: flex;
  position: relative;

  margin: auto;

  height: 100%;
  width: 100%;
  border: none;
  outline: none;
  background: rgba(0, 0, 0, 0);

  font-size: 1.5vh;
  text-decoration: none;
  color: white;



}

.search-button{
  display: flex;



  height: 100%;
  margin-right: 1%;
  padding: 1%;

  position: relative;
  transition: transform 0.15s ease;
}

.search-button:hover{
  transform: scale(0.85);
  cursor: pointer;
}

</style>

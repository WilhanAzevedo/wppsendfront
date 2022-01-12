<template>
  <div class=menu>
    <b-navbar type="dark" variant="dark">
      <b-navbar-nav align="center"  >
        <b-nav-item id="homes">
          <router-link to="/home">Home</router-link>
        </b-nav-item>
        <b-nav-item id="chats">
          <router-link to="/chat">Chat</router-link>
        </b-nav-item>
      </b-navbar-nav>
    </b-navbar>
  </div>
</template>

<script>
export default {
    mounted() {
        this.class();
    },
    name: "Menu",
    data() {
        return {};
    },
    methods: {
        select() {
            
        },
        class() {
            if(this.$route.path == "/home"){
                document.getElementById("homes").classList.add("active");
                document.getElementById("chats").classList.remove("active");
            }else if(this.$route.path == "/chat"){
                document.getElementById("homes").classList.remove("active");
                document.getElementById("chats").classList.add("active");
            }
        } 
    },
};
</script>

<style>
a {
  text-decoration: none;
  font-size: 15px;
  color: #ffffff;
}

a:hover{
    color: #a36513;
}

.menu{
    width: 100%;
}

.navbar{
    text-align: center !important;
    padding-left: 100px;
}

.active{
    background-color: #ffffff;
    border-radius: 10px;
}

.active a{
    color: #000000;
}
</style>
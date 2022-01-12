<template>
  <div>
    <div>
      <Menu />
    </div>
    <div class="home">
      <!-- <b-img
        :src="require('../assets/logo.png')"
        fluid
        alt="Responsive image"
        style="margin-top: 30px"
      ></b-img> -->
      <b-card class="card" bg-variant="dark" text-variant="white">
        <b-card-body>
          <div style="display: flex; width: 50%">
            <b-form class="sel">
              <label for="bairros">Bairro</label>
              <div class="sel">
                <b-form-select
                  class="select"
                  id="bairros"
                  label-field="bairros"
                  :options="options"
                  @change="onChange($event)"
                ></b-form-select>
              </div>
            </b-form>
            <b-form class="sel">
              <label for="sessao">Sessão</label>
              <div class="sel">
                <b-form-select
                  class="select"
                  id="sessao"
                  label-field="sessao"
                  :options="options2"
                ></b-form-select>
              </div>
            </b-form>
            <!-- <b-form class="sel">
          <label for="telefones">Numero</label>
          <div class="sel">
            <b-form-select
                class="select"
              id="telefones"
              label-field="telefones"
              :options="options"
            ></b-form-select>
          </div>
        </b-form> -->
          </div>
          <b-form class="form">
            <b-form-group
              id="input-group-1"
              label="Mensagem"
              label-align-sm="right"
              label-for="textarea"
            >
              <b-form-textarea
                id="textarea"
                placeholder="Digite sua mensagem..."
                v-model="mensagem"
                rows="10"
              ></b-form-textarea>
            </b-form-group>
          </b-form>
          <!-- <div class="input-group mb-1">
          <input type="file" class="form-control" id="inputGroupFile02" accept=".jpg,.gif,.png" @change="changeFile()"/>
        </div> -->
          <div class="button-group">
            <p class="total">Total de contatos neste bairro: {{ total }}</p>
            <b-button
              variant="primary"
              class="button"
              style="margin-left: auto"
              @click="enviar()"
              >Enviar</b-button
            >
          </div>
          <div>
            <progress
              id="bar"
              class="progre"
              value="0"
              :max="total"
              style="margin-top: 20px; width: 100%"
            >
              <span></span>
            </progress>
            <p class="totalenv">Numero de mensagens enviadas</p>
          </div>
        </b-card-body>
      </b-card>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Swal from "sweetalert2";
import Menu from "./Menu.vue";

export default {
  mounted() {
    axios({
      method: "get",
      url: "http://10.19.92.40:8000/api/list/todos",
    }).then((response) => {
      this.options = response.data;
    });
    axios({
      method: "get",
      url: "http://10.19.92.40:8000/api/lista",
    }).then((response) => {
      this.totais = response.data;
    });
  },
  data() {
    return {
      options: [],
      options2: ["adenilson"],
      totais: {},
      total: 0,
      bairro: "",
      mensagem: "",
      enviadas: 0,
      file1: null,
    };
  },
  components: {
    Menu,
  },
  methods: {
    onChange(e) {
      this.total = this.totais[e];
      this.bairro = e;
    },
    enviar() {
      let data = {
        bairro: this.bairro,
        mensagem: this.mensagem,
      };
      let request = new XMLHttpRequest();
      request.open("POST", "http://10.19.92.40:8000/api/enviar", true);
      request.send(JSON.stringify(data));

      Swal.fire({
        title: "Enviando mensagem!",
        text: "",
        icon: "success",
        confirmButtonText: "Ok",
      });

      console.log(this.file1);

      setTimeout(() => {
        this.getEnviadas();
      }, 50000);
    },
    getEnviadas() {
      // const keepAlive = (idInterval) => {
      //  //this.enviadas++
      //  axios({
      //     method: "get",
      //     url: "http://10.19.92.40:8000/api/status",
      //   }).then((response) => {
      //     this.enviadas = response.data[0].enviadas;

      //     document.getElementById("bar").value = this.enviadas;
      //     console.log(this.enviadas);

      //     if (this.enviadas == 0) {
      //       clearInterval(idInterval);
      //       Swal.fire({
      //         title: "Mensagens enviadas!",
      //         text: "",
      //         icon: "success",
      //         confirmButtonText: "Ok",
      //       });
      //     }
      //   });
      // }

      // // aqui coloca uma variavel do data = intervalMSG
      // // viu ai , passei a variavel
      // // lkkkk nome diferente satanas kkk  ia  perguntar aonde tava kkk, mas blz
      // // tem q funfa
      // let idint = setInterval(()=>{
      //   keepAlive(idint)
      // }, 5000)

      let idInterval = setInterval(() => {
        axios({
          method: "get",
          url: "http://10.19.92.40:8000/api/status",
        }).then((response) => {
          this.enviadas = response.data[0].enviadas;

          document.getElementById("bar").value = this.enviadas;
          console.log(this.enviadas);

          if (this.enviadas == 0) {
            clearInterval(idInterval);
            Swal.fire({
              title: "Mensagens enviadas!",
              text: "",
              icon: "success",
              confirmButtonText: "Ok",
            });
          }
        });
      }, 5000);
    },
    changeFile() {
      this.file1 = document.getElementById("inputGroupFile02").files[0];
    },
  },
};
</script>

<style>
.total {
  font-size: 1.5rem;
}

.totalenv {
  font-size: 0.8rem;
}

.card {
  margin-top: 20px;
}

.form {
  margin-bottom: 20px;
}

.button-group {
  display: flex;
  text-align: right;
}

.select {
  width: 100%;
  height: 30px;
  border-radius: 5px;
  margin: 0 auto;
}

.sel {
  width: 100%;
  margin: 0 auto;
  margin-right: 20px;
  margin-bottom: 10px;
}

progress {
  text-align: center;
  height: 40px;
  padding: 10px;
}
progress:after {
  color: black;
  font-size: 0.8rem;
  font-weight: 600;
  content: attr(value) "/" attr(max);
  position: absolute;
}

.home {
  max-width: 700px;
  margin: 0 auto;
  text-align: left;
}
</style>
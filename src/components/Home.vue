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
      <div class="container">
        <div class="row">
          <div class="col-4">
            <b-card class="card" bg-variant="ligth" text-variant="black">
              <b-card-body>
                <div>
                  <b-form class="sel">
                    <label for="cidades">Selecione a cidade</label>
                    <div class="sel">
                      <b-form-select
                        class="select"
                        id="cidades"
                        label-field="cidades"
                        :options="cidades"
                        @change="onChangeCidade($event)"
                      ></b-form-select>
                    </div>
                  </b-form>
                </div>
                <div>
                  <b-form class="sel">
                    <label for="bairros">Selecione o bairro</label>
                    <div class="sel">
                      <b-form-select
                        class="select"
                        id="bairros"
                        label-field="bairros"
                        :options="bairros"
                        @change="onChangeBairro($event)"
                      ></b-form-select>
                    </div>
                  </b-form>
                </div>
                <div>
                  <b-form class="sel">
                    <label for="grupoChips">Selecione o grupo de chips</label>
                    <div class="sel">
                      <b-form-select
                        class="select"
                        id="grupoChips"
                        label-field="grupoChips"
                        :options="grupoChips"
                        @change="onChangeGrupo($event)"
                      ></b-form-select>
                    </div>
                  </b-form>
                </div>
                <div id="nums" class="row"></div>
                <div class="row">
                  <div class="col icons" v-b-popover.hover.top="'Novo Grupo'">
                    <img
                      src="../assets/add-categories.svg"
                      class="cls-1"
                      alt=""
                      v-b-modal.modal-center
                    />
                    <b-modal
                      id="modal-center"
                      centered
                      size="sm"
                      ref="modal"
                      title="Novo grupo"
                      @ok="handleOkGrupo"
                    >
                      <form ref="form">
                        <b-form-group label="Nome" label-for="name-input">
                          <b-form-input
                            id="name-input"
                            v-model="name"
                            required
                            style="width: 95%"
                          ></b-form-input>
                        </b-form-group>
                      </form>
                    </b-modal>
                  </div>
                  <div class="col icons" v-b-popover.hover.top="'Novo Chip'">
                    <img
                      src="../assets/sim-card.svg"
                      class="cls-1"
                      alt=""
                      @click="clickNum"
                    />
                    <button
                      id="openNum"
                      hidden
                      v-b-modal.modal-center2
                    ></button>
                    <b-modal
                      id="modal-center2"
                      centered
                      size="lg"
                      ref="modal"
                      title="Novo numero"
                      @ok="handleOkNumero"
                    >
                      <div class="row">
                        <div class="col-6">
                          <form ref="form">
                            <b-form-group
                              label="Numero"
                              label-for="numero-input"
                            >
                              <b-form-input
                                id="numero-input"
                                v-model="numero"
                                required
                              ></b-form-input>
                            </b-form-group>
                          </form>
                          <div style="display: flex">
                            <form ref="form2">
                              <label for="grupoChips"
                                >Selecione o grupo de chips</label
                              >
                              <b-form-select
                                class="select"
                                style="width: 90%"
                                id="grupoChips"
                                label-field="grupoChips"
                                :options="grupoChips"
                                @change="onChangeGrupo($event)"
                              ></b-form-select>
                            </form>
                            <form>
                              <b-form-group label=" " label-for="btn-numero">
                                <b-button
                                  id="btn-numero"
                                  variant="primary"
                                  style="margin-top: 25%"
                                  @click="handleQRCode"
                                  >QR-Code</b-button
                                >
                              </b-form-group>
                            </form>
                          </div>
                        </div>
                        <div class="col-6">
                          <div
                            id="qrcode"
                            style="height: 270px; text-align:center;"
                          >
                            <div
                              class="spinner-border text-success"
                              style="width: 3rem; height: 3rem; display:none;"
                              role="status"
                              id="spinner"

                            >
                              <span class="visually-hidden">Loading...</span>
                            </div>
                            <img
                              id="qrcodeImg"
                              style="height: 250px"
                              value=""
                            />
                          </div>
                        </div>
                      </div>
                    </b-modal>
                  </div>
                </div>
              </b-card-body>
            </b-card>
          </div>
          <div class="col">
            <b-card class="card" bg-variant="ligth" text-variant="black">
              <b-card-body>
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
                <div class="input-group mb-1">
          <input type="file" class="form-control" id="inputGroupFile02" accept=".jpg,.gif,.png" @change="changeFile()"/>
        </div>
                <div class="button-group">
                  <p class="total">
                    Total de contatos neste bairro: {{ total }}
                  </p>
                  <b-button
                    variant="primary"
                    class="button"
                    style="margin-left: auto"
                    @click="enviar()"
                    >Enviar</b-button
                  >
                </div>
                <div style="text-align: center">
                  <progress
                    id="bar"
                    class="progre"
                    value="0"
                    :max="total"
                    style="margin-top: 20px; width: 100%; margin-bottom: -13px"
                  >
                    <span></span>
                  </progress>
                  <p class="totalenv">Numero de mensagens enviadas</p>
                </div>
              </b-card-body>
            </b-card>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Swal from "sweetalert2";
import Menu from "./Menu.vue";

export default {
  async mounted() {
    try{
    await axios({
      method: "get",
      url: "http://10.19.92.83:8000/api/cidades",
      headers: {
        Authorization: "Bearer " + localStorage.getItem("token"),
      },
    }).then((response) => {
      this.cidades = response.data;
    });
    await axios({
      method: "get",
      url: "http://10.19.92.83:8000/api/grupos",
      headers: {
        Authorization: "Bearer " + localStorage.getItem("token"),
      },
    }).then((response) => {
      this.grupoChips = response.data;
    });
    }catch(e){
      this.$router.push("/");
    }
  },
  data() {
    return {
      cidades: [],
      bairros: [],
      grupoChips: [],
      chips: [],
      totais: {},
      total: 0,
      bairro: "",
      mensagem: "",
      enviadas: 0,
      file1: null,
      name: "",
      numero: "",
      grupo: "",
      img: "",
      cidade: "",
    };
  },
  components: {
    Menu,
  },
  methods: {
    onChangeCidade(e) {
      this.cidade = e;
      axios({
        method: "post",
        url: "http://10.19.92.83:8000/api/list/todos",
        headers: {
          Authorization: "Bearer " + localStorage.getItem("token"),
        },
        data: {
          cidade: e,
        },
      }).then((response) => {
        this.bairros = response.data;
      });
      axios({
        method: "get",
        url: "http://10.19.92.83:8000/api/lista/" + e,
        headers: {
          Authorization: "Bearer " + localStorage.getItem("token"),
        },
      }).then((response) => {
        this.totais = response.data;
      });
    },
    onChangeBairro(e) {
      this.total = this.totais[e];
      this.bairro = e;
    },
    async onChangeGrupo(e) {
      this.grupo = e;

      await axios({
        method: "get",
        url: "http://10.19.92.83:8000/api/grupos/" + e,
        headers: {
          Authorization: "Bearer " + localStorage.getItem("token"),
        },
      }).then((response) => {
        this.chips = response.data;
      });

      let div = document.getElementById("nums");
      if (div.hasChildNodes()) {
        while (div.firstChild) {
          div.removeChild(div.firstChild);
        }
      }

      this.chips.forEach((element) => {
        //console.log(element);
        let tag =
          `<div class="col bdg">` +
          `<span class="badge bg-success">` +
          element +
          `</span>` +
          `</div>`;
        div.innerHTML += tag;
      });
    },
    handleOkGrupo() {
      this.grupoChips.push(this.name);
    },
    handleOkNumero(bvModalEvt) {
      bvModalEvt.preventDefault();
      console.log(document.getElementById("numero-input").value);
    },
    async handleQRCode() {

      let spin = document.getElementById("spinner");
      spin.style.display = "inline-block";

      await axios({
        method: "post",
        url: "http://10.19.92.83:8000/api/newnumber",
        headers: {
          Authorization: "Bearer " + localStorage.getItem("token"),
        },
        data: {
          nome: this.numero,
          grupo: this.grupo,
        },
      });

      await axios({
        method: "post",
        url: "http://10.19.92.83:8000/api/startsession",
        headers: {
          Authorization: "Bearer " + localStorage.getItem("token"),
        },
        data: {
          nome: this.numero,
        },
      }).then((response) => {
        console.log(response.data);
        if (response.data.qrcode) {

          
          spin.style.display = "none";

          let qrcode = document.getElementById("qrcodeImg");
          qrcode.src = "data:image/png;base64," + response.data.qrcode;
        }
      });

      let idInterval = setInterval(async () => {
        console.log("interval");
        await axios({
          method: "post",
          url: "http://10.19.92.83:8000/api/refreshsession",
          headers: {
            Authorization: "Bearer " + localStorage.getItem("token"),
          },
          data: {
            nome: this.numero,
          },
        }).then((response) => {
          console.log(response.data);
          if (response.data.qrcode) {
            spin.style.display = "none";
            let qrcode = document.getElementById("qrcodeImg");
            qrcode.src = response.data.qrcode;
          }
          if (response.data.status == "CONNECTED") {
            clearInterval(idInterval);
            Swal.fire({
              title: "Sucesso!",
              text: "Número cadastrado com sucesso!",
              icon: "success",
              confirmButtonText: "OK",
            });

            this.$bvModal.hide("modal-center2");
          }
        });
      }, 5000);
    },
    clickNum() {
      document.getElementById("openNum").click();
    },
    enviar() {
      let data = {
        cidade: this.cidade,
        bairro: this.bairro,
        mensagem: this.mensagem,
        grupo: this.grupo,
        img: this.img,

      };
      let request = new XMLHttpRequest();
      request.open("POST", "http://10.19.92.83:8000/api/enviar", true);
      request.setRequestHeader(
        "Authorization",
        "Bearer " + localStorage.getItem("token")
      );
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
      }, 15000);
    },
    getEnviadas() {
      let idInterval = setInterval(() => {
        axios({
          method: "get",
          url: "http://10.19.92.83:8000/api/status",
          headers: {
            Authorization: "Bearer " + localStorage.getItem("token"),
          },
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
      console.log(this.file1);

      let reader = new FileReader();
      reader.readAsDataURL(this.file1);
      reader.onload = (e) => {
        this.img = e.target.result;
      };

    },
  },
};
</script>

<style>
#numero-input {
  width: 100%;
  margin: 0;
  height: 40px;
}

.swal2-styled.swal2-confirm {
  background-color: #0b5ed7;
}

.cls-1 {
  max-height: 20px;
}

.icons {
  text-align: center;
  margin-top: 5px;
}

.total {
  font-size: 1.5rem;
}

.totalenv {
  font-size: 0.8rem;
}

.card {
  margin-top: 20px;
  height: 100%;
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
  max-width: 900px;
  margin: 0 auto;
  text-align: left;
}
</style>
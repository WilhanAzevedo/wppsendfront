<template>
  <div>
    <b-img
      :src="require('../assets/logo.png')"
      fluid
      alt="Responsive image"
      style="margin-top:60px;"
    ></b-img>
    <b-card class="card" bg-variant="dark" text-variant="white">
      <b-card-body>
        <div style="display: flex; width:100%;">
        <b-form class="sel">
          <label for="bairros">Bairro</label>
          <div class="sel">
            <b-form-select
            class="select"
              id="bairros"
              label-field="bairros"
              :options="options"
            ></b-form-select>
          </div>
        </b-form>
        <b-form class="sel">
          <label for="telefones">Numero</label>
          <div class="sel">
            <b-form-select
                class="select"
              id="telefones"
              label-field="telefones"
              :options="options"
            ></b-form-select>
          </div>
        </b-form>
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
            ></b-form-textarea>
          </b-form-group>
        </b-form>
        <div class="button-group">
          <b-button variant="primary" class="button">Enviar</b-button>
        </div>
      </b-card-body>
    </b-card>
  </div>
</template>

<script>
export default {
  data() {
    return {
      options: ["Centro", "Imperial", "Paraíso", "Maringá"],
    };
  },
};
</script>

<style>
.card {
  margin-top: 20px;
}

.form {
  margin-bottom: 20px;
}

.button-group {
  text-align: right;
}

.select{
    width: 100%;
    height: 30px;
    border-radius: 5px;
    margin: 0 auto;
}

.sel{
    width: 100%;
    margin: 0 auto;
    margin-right: 20px;
}

</style>
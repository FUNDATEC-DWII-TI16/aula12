<template>
  <div class="container-fluid">
    <div class="row">
      <div class="col-4">
        <label>Nome</label>
        <input v-model="usuario.nome" type="text" class="form-control" />
      </div>
    </div>
    <div class="row">
      <div class="col-4">
        <label>Ativo</label>
        <input v-model="usuario.ativo" type="checkbox" class="form-control" />
      </div>
    </div>
    <div class="row">
      <div class="col-4">
        <button type="button" class="btn btn-primary" @click="salvarUsuario()">
          Salvar
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      usuario: {},
    };
  },
  mounted() {
    fetch("http://191.235.105.128:8080/usuarios/16", {
      method: "GET",
      headers: {
        Accept: "application/json",
      },
    })
      .then((response) => {
        if (response.ok === true) {
          return response.json();
        }
      })
      .then((bolinhaDeMeuDeus) => {
        this.usuario = bolinhaDeMeuDeus;
      });
  },
  methods: {
    salvarUsuario() {
      fetch("http://191.235.105.128:8080/usuarios", {
        method: "POST",
        headers: {
          Accept: "application/json",
          "Content-Type": "application/json",
        },
        body: JSON.stringify(this.usuario),
      }).then((response) => {
        if (response.ok === true) {
          alert("Dados salvos com sucesso!");
        }
      });
    },
  },
};
</script>

<template>
    <div class="formulario">
      <vue-form
        class="formulario-listas"
        :state="formstate"
        @submit.prevent="onSubmit"
      >
        <validate class="formulario-item" tag="label">
          <span>Nombre: </span>
          <input
            type="text"
            v-model="model.name"
            required
            name="name"
          />
          <field-messages name="name" show="$touched">
            <div slot="required">El nombre es requerido</div>
          </field-messages>
        </validate>
  
        <validate class="formulario-item" tag="label">
          <span>Apellido: </span>
          <input
            type="text"
            v-model="model.apellido"
            required
            name="apellido"
          />
          <field-messages name="apellido" show="$touched">
            <div slot="required">El apellido es requerido</div>
          </field-messages>
        </validate>
  
        <validate class="formulario-item" tag="label">
          <span>Edad: </span>
          <input
            type="number"
            v-model="model.edad"
            required
            name="edad"
          />
          <field-messages name="edad" show="$touched">
            <div slot="required">La edad es requerida</div>
          </field-messages>
        </validate>
  
        <validate class="formulario-item" tag="label">
          <span>Email: </span>
          <input
            type="email"
            v-model="model.email"
            required
            name="email"
          />
          <field-messages name="email" show="$touched">
            <div slot="required">El email es requerido</div>
            <div slot="email">El email no es válido</div>
          </field-messages>
        </validate>
  
        <validate
          class="formulario-item"
          tag="label"
          :custom="{'check-password': checkPassword}"
        >
          <span>Contraseña: </span>
          <input
            type="password"
            v-model="model.password"
            name="password"
            required
          />
          <field-messages name="password" show="$touched">
            <div slot="required">La contraseña es requerida</div>
            <div slot="check-password">
              Debe contener al menos 8 caracteres, una mayúscula, una minúscula,
              un número y un carácter especial
            </div>
          </field-messages>
        </validate>
  
        <button type="submit">Enviar</button>
      </vue-form>
    </div>
  </template>
  
  <script>
  export default {
    name: "FormularioVue",
    data() {
      return {
        formstate: {},
        model: {
          name: "",
          apellido: "",
          email: "",
          edad: "",
          password: "",
        },
      };
    },
    methods: {
      onSubmit() {
        if (this.formstate.$valid) {
          this.$emit("emit-form", { ...this.model }); // Emitir evento con los datos del formulario
          this.clearForm();
          alert("Formulario enviado!");
        } else {
          alert("Si completas el formulario esto no pasa :D !");
        }
      },
      checkPassword(value) {
        return /^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[$@$!%*?&])[A-Za-z\d$@$!%*?&]{8,15}/.test(
          value
        );
      },
      clearForm() {
        this.model.name = "";
        this.model.apellido = "";
        this.model.email = "";
        this.model.edad = "";
        this.model.password = "";
        this.$refs.formstate.reset();
      },
    },
  };
  </script>
  
  <style>
  .formulario {
    padding: 10px;
    background-color: antiquewhite;
  }
  
  .formulario-item {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    padding-bottom: 10px;
  }
  
  .formulario-item input {
    border: none;
    border-radius: 5px;
    padding: 4px;
  }
  
  button {
    border: none;
    background-color: tomato;
    padding: 10px;
    border-radius: 5px;
    color: #fff;
  }
  </style>
  
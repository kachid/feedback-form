<template>
  <v-layout>
    <v-flex class="text-center">
      <v-card
        class="mx-auto"
        max-width="600"
      >
        <v-system-bar color="indigo darken-2"></v-system-bar>
        <v-toolbar>
          <v-toolbar-title>Feedback</v-toolbar-title>
        </v-toolbar>
        <v-form
          ref="form"
          v-model="valid"
          class="pa-5"
          :lazy-validation="lazy"
        >
          <v-text-field
            v-model="name"
            label="Имя"
            filled
          ></v-text-field>
          <v-text-field
            v-model="phone"
            v-mask="mask"
            :rules="phoneRules"
            hint="+7 (000) 000-00-00"
            label="Телефон"
            filled
            required
          ></v-text-field>
          <v-checkbox
            v-model="checkbox"
            :rules="[v => !!v || 'Вы должны согласиться, чтобы продолжить!']"
            label="Согласен на обработку персональных данных"
            color="teal"
            required
          ></v-checkbox>
          <v-btn
            :disabled="!valid"
            color="success"
            class="ma-4"
            @click="validate"
          >
            Отправить
          </v-btn>
        </v-form>
      </v-card>
    </v-flex>
  </v-layout>
</template>
<script>
import { mask } from 'vue-the-mask'

export default {
  directives: {
    mask
  },
  data: () => ({
    mask: '+7 (###) ###-##-##',
    valid: true,
    name: '',
    phone: '',
    phoneRules: [
      v => !!v || 'Номер телефона указать обязательно!'
    ],
    checkbox: true,
    lazy: false
  }),
  methods: {
    validate () {
      if (this.$refs.form.validate()) {
        this.snackbar = true
      }
    }
  }
}
</script>

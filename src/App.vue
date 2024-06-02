<template>
  <form @submit.prevent="submit">
    <v-container>
      <v-row class="d-flex flex-column">
        <v-col
        cols="12"
          md="4"
        >
        <v-text-field
          v-model="name.value.value"
          :counter="10"
          :error-messages="name.errorMessage.value"
          label="Name"
        ></v-text-field>
      </v-col>

      <v-col
        cols="12"
          md="4"
        >
        <v-text-field
          v-model="lastname.value.value"
          :counter="10"
          :error-messages="lastname.errorMessage.value"
          label="Last Name"
        ></v-text-field>
      </v-col>

      <v-col
      cols="12"
          md="4"
      ><v-text-field
          v-model="phone.value.value"
          :counter="7"
          :error-messages="phone.errorMessage.value"
          label="Phone"
        ></v-text-field></v-col>  
      

        <v-col
        cols="12"
          md="4"
        ><v-text-field
          v-model="email.value.value"
          :error-messages="email.errorMessage.value"
          label="E-mail"
        ></v-text-field></v-col>
        

        <v-col
        cols="12"
          md="4"
        ><v-text-field
          v-model="address.value.value"
          :error-messages="address.errorMessage.value"
          :items="items"
          label="Address"
        ></v-text-field></v-col>
        

        

        <v-col
        cols="12"
          md="4"
        >
        <v-btn
          class="me-4"
          type="submit"
        >
          submit
        </v-btn>
      </v-col>

      <v-col
      cols="12"
          md="4"
      ><v-btn @click="handleReset">
          clear
        </v-btn></v-col>  
      
      </v-row>  
  </v-container>
  </form>
</template>
<script setup>
  import { ref } from 'vue'
  import { useField, useForm } from 'vee-validate'

  const { handleSubmit, handleReset } = useForm({
    validationSchema: {
      name (value) {
        if (value?.length >= 2) return true

        return 'Name needs to be at least 2 characters.'
      },
      lastname (value) {
        if (value?.length >= 2) return true

        return 'Last Name needs to be at least 2 characters.'
      },

      phone (value) {
        if (value?.length > 9 && /[0-9-]+/.test(value)) return true

        return 'Phone number needs to be at least 9 digits.'
      },
      email (value) {
        if (/^[a-z.-]+@[a-z.-]+\.[a-z]+$/i.test(value)) return true

        return 'Must be a valid e-mail.'
      },
      address (value) {
        if (value?.length >= 5) return true

        return 'Adress needs to be at least 5 digits.'
      }
    },
  })
  const name = useField('name')
  const lastname = useField('lastname')
  const phone = useField('phone')
  const email = useField('email')
  const address = useField('address')
  

  

  const submit = handleSubmit(values => {
    alert(JSON.stringify(values, null, 2))
  })
</script>

    
  

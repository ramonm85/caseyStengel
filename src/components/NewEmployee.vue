<template>
   <div id="new-employee">
       <h3>New Choices</h3>
       <p style="color :red"> PLEASE MAKE SURE YOUR CHOICES ARE CORRECT THE FIRST TIME</p>
       <div class="row">
    <form @submit.prevent="saveEmployee" class="col s12">
      <div class="row">
        <div class="input-field col s12">
          <input type="text" v-model="peg" required>
          <label>PEG #</label>
        </div>
      </div>
      <div class="row">
        <div class="input-field col s12">
          <input type="text" v-model="name" required>
          <label>Name</label>
        </div>
      </div>
      <div class="row">
        <div class="input-field col s12">
          <input type="text" v-model="pass" required>
          <label>PASS</label>
        </div>
      </div>
      <div class="row">
        <div class="input-field col s12">
          <input type="text" v-model="position" required>
          <label>Position</label>
        </div>
      </div>
      <div class="row">
        <div class="input-field col s12">
          <input type="text" v-model="choices" required>
          <label>choices</label>
        </div>
      </div>
      <button type="submit" class="btn">Submit</button>
      <router-link to="/" class="btn grey">Cancel</router-link>
    </form>
  </div>
  </div>
</template>

<script>
import db from './firebaseInit'
export default {
    name: 'new-employee',
    data (){
        return {
          peg: null,
          name: null,
          pass: null,
          position: null,
          choices: null
        }
    },
     methods: {
        saveEmployee () {
          db.collection('Operators').add({
            peg: this.peg,
            name: this.name,
            pass: this.pass,
            position: this.position,
            choices: this.choices
          })
          .then(docRef => {
            console.log('Client added: ', docRef.id)
            this.$router.push('/')
          })
          .catch(error => {
            console.error('Error adding employee: ', error)
          })
        }
      }

}
</script>
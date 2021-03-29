<template>
    <v-card class="my-2">
<!--        <v-card-text primary-title>-->
<!--            <i>({{ message.id }})</i>-->
<!--            {{ message.text }}-->
<!--        </v-card-text>-->
        <v-card-actions>
          ({{ message.id }})
          <input type="text" v-model="message.text">
            <v-btn value="Edit" @click="edit" small flat round>Edit</v-btn>
          {{ message.vibor }}

            <v-btn @click="editCheck">{{message.vibor}}</v-btn>

            <v-btn @click="save">SAVE</v-btn>

            <v-btn icon @click="del" small>
            <v-icon>delete</v-icon>
          </v-btn>
        </v-card-actions>
    </v-card>
</template>

<script>
    import { mapActions } from 'vuex'
    import messages from "../../api/messages";

      export default {

        props: ['message', 'editMessage'],
        data() {
          return {
            text: '',
            id: '',
            vibor: this.message.vibor,
          }
        },
        methods: {
            ...mapActions(['removeMessageAction', 'addMessageAction', 'updateMessageAction']),

            edit() {
                this.editMessage(this.message)
            },
            del() {
                this.removeMessageAction(this.message)
            },
            save() {
              const message = {
                id: this.message.id,
                text: this.message.text,
                vibor: this.vibor
            }

            // if (this.id) {
              this.updateMessageAction(message)
            //}

            // else {
            //   this.addMessageAction(message)
            // }

            this.text = ''
            this.id = ''
            this.vibor = false

          },
          editCheck(){
            if(this.vibor == false){
              this.vibor = true
            }else{
              this.vibor = false
            }
            const message = {
              id: this.message.id,
              text: this.message.text,
              vibor: this.vibor
            }
            this.updateMessageAction(message)
          }
        }
    }
</script>

<style>

</style>

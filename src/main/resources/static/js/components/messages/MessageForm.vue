<template>
    <v-layout row>
        <v-text-field
                label="New message"
                placeholder="Write something"
                v-model="text"
        />

        <v-btn @click="save">Save</v-btn>
      <v-btn @click="editCheck">{{vibor}}</v-btn>
    </v-layout>
</template>

<script>
    import { mapActions } from 'vuex'

    export default {
        props: ['messageAttr'],
        data() {
            return {
                text: '',
                id: '',
                vibor: false,

            }
        },
        watch: {
            messageAttr(newVal, oldVal) {
                this.text = newVal.text
                this.id = newVal.id
                this.vibor = newVal.vibor
            }
        },
        methods: {
            ...mapActions(['addMessageAction', 'updateMessageAction']),
            save() {
                const message = {
                    id: this.id,
                    text: this.text,
                    vibor: this.vibor
                }

                if (this.id) {
                    this.updateMessageAction(message)
                } else {
                    this.addMessageAction(message)
                }

                this.text = ''
                this.id = ''
                this.vibor = false

            },
            editCheck(){
               // this.chek ? this.chek = true : this.chek = false
              if(this.vibor == false){
                this.vibor = true
              }else{
                this.vibor = false
              }
            }
        }
    }
</script>

<style>

</style>

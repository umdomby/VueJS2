<template>
    <div>
<!--        {{ message.text }}-->
        <span style="position: absolute; right: 0">
            <input type="button" value="Save" @click="save" />
<!--            <input type="button" value="Edit" @click="edit" />-->
            <input type="button" value="X" @click="del" />
        </span>

      <input type="text" v-model="message.text">
      <i>({{ message.id }})</i>
<!--            <input type="text"/>-->
<!--      {{textValue}}-->

    </div>
</template>

<script>

    function getIndex(list, id) {
      for (var i = 0; i < list.length; i++ ) {
        if (list[i].id === id) {
          return i
        }
      }

      return -1
    }

    export default {
        data(){
          return {
            text: '',
            id: ''
          }
        },
        components: {

        },
        props: ['message', 'editMessage', 'deleteMessage', 'messages'],
        methods: {
          edit() {
            // // this.editMessage(this.message)
            //
            // this.text = this.message.text
            // this.id = this.message.id
          },
          del() {
            this.deleteMessage(this.message)
          },
          save() {

            this.text = this.message.text
            this.id = this.message.id

            if (this.id) {

              const message = { text: this.text }
              this.$resource('/message{/id}').update({id: this.id}, message).then(result =>
                  result.json().then(data => {
                    const index = getIndex(this.messages, data.id)
                    this.messages.splice(index, 1, data)
                    this.text = ''
                    this.id = ''
                  })
              )
              // console.log(this.id)
            }
          }
        }
    }
</script>

<style>

</style>

<template>
  <div class="wrapper">
    <div class="wrapper-content">

      <section>
        <div class="container">
          <h1> {{ title }} </h1>

          <Message v-if="message" :message="message"/>

          <!-- new note -->
          <div class="new-note">
              <input type="text" v-model="note.title">
              <textarea name="" id="" cols="30" rows="10" v-model="note.descr"></textarea>
              <button @click="addNote">New note</button>
          </div>
          <!-- note list -->
          <div class="notes">
              <div class="note" v-for="(note, index) in notes" :key="index">
                  <div class="note-header">
                      <p> {{note.title}} </p>
                  </div>
                  <div class="note-body">
                      <p> {{note.descr}} </p>
                  </div>
                  <span> {{note.date}} </span>
              </div>
          </div>
        </div>
      </section>

    </div>
  </div>
</template>

<script>
import Message from './components/Message.vue'

export default {
  components: {
    Message
  },
  data() {
    return {
      title: 'Notes App',
      note: {
        title: '',
        descr: ''
      },
      message: null,
      notes: [
        {
          title: 'First note',
          descr: 'Description for first note',
          date: new Date(Date.now()).toLocaleString()
        },
        {
          title: 'Second note',
          descr: 'Description for second note',
          date: new Date(Date.now()).toLocaleString()
        },
        {
          title: 'Third note',
          descr: 'Description for third note',
          date: new Date(Date.now()).toLocaleString()
        }
      ]
    }
  },
  methods: {
    addNote() {
      let {title, descr} = this.note //ограничены областью видимости

      if (title === '') {
        this.message = `title can't be blanked!`
        return false
      }

      this.notes.push({
        title,
        descr,
        date: new Date(Date.now()).toLocaleString()
      })

      this.message = null 
      this.note.title = '' 
      this.note.descr = ''
    }
  }
}
</script>

<style>

</style>

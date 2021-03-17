<template>
  <div class="wrapper">
    <div class="wrapper-content">

      <section>
        <div class="container">

          <h1> {{ title }} </h1>

          <Message v-if="message" :message="message"/>

          <NewNote :note="note" @addNote="addNote"/>

          <Notes :notes="notes" @remove="removeNote"/>

        </div>
      </section>

    </div>
  </div>
</template>

<script>
import Message from './components/Message.vue'
import NewNote from './components/NewNote.vue'
import Notes from './components/Notes.vue'


export default {
  components: {
    Message, Notes, NewNote
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
    },
    removeNote(index) {
      this.notes.splice(index, 1)
    }
  }
}
</script>

<style>

</style>

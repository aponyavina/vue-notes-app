<template>
  <div class="wrapper">
    <div class="wrapper-content">

      <section>
        <div class="container">

          <h1 class="heading">Notes App</h1>

          <Message v-if="message" :message="message"/>

          <NewNote :note="note" @addNote="addNote"/>

          <div class="note-header" style="margin: 36px 0;">
            <h1> {{ title }} </h1>

            <Search 
            :value="search" 
            placeholder="Find your note"
            @search="search = $event"
            />

            <div class="icons">
              <svg :class="{active: grid}" @click="grid = true" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" ><rect x="3" y="3" width="7" height="7"></rect><rect x="14" y="3" width="7" height="7"></rect><rect x="14" y="14" width="7" height="7"></rect><rect x="3" y="14" width="7" height="7"></rect></svg>
              <svg :class="{active: !grid}" @click="grid = false" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><line x1="8" y1="6" x2="21" y2="6"></line><line x1="8" y1="12" x2="21" y2="12"></line><line x1="8" y1="18" x2="21" y2="18"></line><line x1="3" y1="6" x2="3" y2="6"></line><line x1="3" y1="12" x2="3" y2="12"></line><line x1="3" y1="18" x2="3" y2="18"></line></svg>
            </div>
          </div>

          <Notes 
          :notes="notesFilter" 
          @remove="removeNote"
          :grid="grid"
          />

        </div>
      </section>

    </div>
  </div>
</template>

<script>
import Message from './components/Message.vue'
import NewNote from './components/NewNote.vue'
import Notes from './components/Notes.vue'
import Search from './components/Search.vue'


export default {
  components: {
    Message, Notes, NewNote, Search
  },
  data() {
    return {
      title: 'Notes App',
      search: '',
      note: {
        title: '',
        descr: ''
      },
      message: null,
      grid: true,
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
  computed: {
    notesFilter() {
      let array = this.notes,
        search = this.search
        if (!search) return array
        // small
        search = search.trim().toLowerCase()
        // filter
        array = array.filter(item => {
          if (item.title.toLowerCase().indexOf(search) !== -1) {
            return item
          }
        })
        // error
        return array
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

<style scoped>
  .heading {
    font-size: 25px;
    font-weight: 500;
    text-align: center;
    color: #494ce8;
    margin-bottom: 20px;
  }


</style>

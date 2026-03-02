<script>
export default {
  name: "Main",
  data() {
    return {
      noteTitle: "",
      noteText: "",
            notes: JSON.parse(localStorage.getItem('my-notes') || '[]'),
      
    }
  },
  watch: {
    notes: {
      handler(newNotes) {
        localStorage.setItem('my-notes', JSON.stringify(newNotes));
      },
      deep: true 
    }
  },
  methods: {
    saveNote() {
      if (this.noteTitle.trim() ==='' || this.noteText.trim() === '') {

        return
      }
      this.notes.push({
        title: this.noteTitle,
        text: this.noteText
      })
    },
    addNote() {
      this.noteTitle = ""
      this.noteText = ""

    },
    showNote(note){
      this.noteTitle = note.title,
          this.noteText = note.text
    },
    deleteNote(index){
      this.notes.splice(index,1)
    }
  },
  computed: {
    isEmptyNote(){
      return this.noteTitle.trim() ===''
    }
  }


    }




</script>

<template>
  <main class="flex gap-6" >
    <div class="w-1/2">
      <div class="flex-col">
        <div class="flex justify-between mb-5">
      <h1 class="text-xl font-semibold text-emerald-200">New Note</h1>

      <div  class="flex flex-row gap-5">
        <button class="hover:text-black hover:bg-emerald-700/50 text-emerald-200 flex rounded-lg border gap-2 px-2 py-1 md:border-green-800 bg-emerald-800/20 text-sm items-center"
                  @click="addNote()"
        ><svg xmlns="http://www.w3.org/2000/svg" width="15" height="15" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class=""><path d="M5 12h14"/><path d="M12 5v14"/></svg>New</button>
        <button :class="{' hover:bg-emerald-800 cursor-pointer': !isEmptyNote,}"
                @click="saveNote()" class=" text-white flex  rounded-lg  gap-2 px-2 py-1 bg-emerald-600 items-center "
        ><svg  xmlns="http://www.w3.org/2000/svg" width="15" height="15" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class=""><path d="M15.2 3a2 2 0 0 1 1.4.6l3.8 3.8a2 2 0 0 1 .6 1.4V19a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2z"/>
          <path d="M17 21v-7a1 1 0 0 0-1-1H8a1 1 0 0 0-1 1v7"/>
          <path d="M7 3v4a1 1 0 0 0 1 1h7"/></svg>Save</button>
      </div>
        </div>
        <div  class="flex-col space-y-3">
         <input v-model="noteTitle"  type="text" class=" p-1 w-full rounded-lg border md:border-green-800 bg-emerald-900/40 border-emerald-700/50 text-emerald-100 placeholder:text-emerald-400/40" placeholder="Note title...">
           <textarea v-model="noteText" type="text" class="p-1 rounded-lg w-full min-h-[400px] border md:border-green-800 bg-emerald-900/40 border-emerald-700/50 text-emerald-100 placeholder:text-emerald-400/40 resize-none " placeholder="Start writing..."></textarea></div>

      </div>
    </div>
    <div class="w-1/2">
      <h1 class="text-xl font-semibold text-emerald-200 mb-6">Saved notes({{notes.length}})</h1>

      <div v-if="notes.length ===0"   class=" flex flex-col  pt-12">
        <h2 class="text-center  text-emerald-400/60">No saved notes yet.</h2>

        <h3 class="text-center  text-emerald-400/60">Create your first note to get started!</h3>
      </div>
      <div>
        <ul class="space-y-2">
          <li @click="showNote(note)" class="hover:bg-emerald-800 text-emerald-200 flex
           justify-between
           rounded-lg border gap-2 px-3 py-3 md:border-green-800 bg-emerald-800/20
            text-sm items-center" v-for="(note,index) in notes"  >
            <span>
            {{ note.title}}</span>
            <button @click="deleteNote(index)"  class="rounded-lg text-red-400/50 hover:bg-red-200/50 p-1 ">
              <svg xmlns="http://www.w3.org/2000/svg"
                         width="15"
                         height="15"
                         viewBox="0 0 24 24"
                         fill="none"
                         stroke="currentColor"
                         stroke-width="2"
                         stroke-linecap="round"
                         stroke-linejoin="round"
                         class="lucide lucide-trash2-icon lucide-trash-2"><path d="M10 11v6"/><path d="M14 11v6"/><path d="M19 6v14a2 2 0 0 1-2 2H7a2 2 0 0 1-2-2V6"/>
              <path d="M3 6h18"/><path d="M8 6V4a2 2 0 0 1 2-2h4a2 2 0 0 1 2 2v2"/></svg></button>
          </li>

        </ul>
      </div>

    </div>
  </main>

</template>

<style scoped>

</style>

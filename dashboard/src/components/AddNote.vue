<template>
    <div>
        <button @click="addNewNote" class="button-add">Add Note<i class="material-icons">add</i></button>
        <div class="notes-grid">
        <div v-for="(note, index) in notes" :key="index" class="sticky-note">
            <div class="note-header">
                <button @click="removeNote(index)" class="button-close" :style="{backgroundColor: note.important ? 'pink' : note.color}"><i class="material-icons" :style="{backgroundColor: note.important ? 'pink' : note.color}">close</i></button>
                <button @click="editNote(index)" class="button-edit" :style="{backgroundColor: note.important ? 'pink' : note.color}"><i class="material-icons" :style="{backgroundColor: note.important ? 'pink' : note.color}">edit</i></button>
                <button @click="toggleNoteImportance(index)" :style="{backgroundColor: note.important ? 'pink' : note.color}" :class="{ 'important-button': note.important }">{{ note.important ? 'Unmark Important' : 'Mark Important' }}</button>
            </div>
            <textarea 
            :disabled="!note.editing" v-model="note.content"  
            :style="{ width: note.width + 'px', backgroundColor: note.important ? 'pink' : note.color}" 
            ref="noteTextarea" 
            placeholder="Type your note"
            class="textarea"></textarea>
            <button @click="saveNote(index)" class="button-save" :style="{backgroundColor: note.important ? 'pink' : note.color}"><i class="material-icons" :style="{backgroundColor: note.important ? 'pink' : note.color}">save</i></button>
        </div>
    </div>
  </div>
</template>

<script>
export default {
    name:'AddNote',
  data() {
    return {
      notes: [],
      editing: true
    };
  },
  created() {
    const savedNotes = localStorage.getItem('stickyNotes');
    if (savedNotes) {
      this.notes = JSON.parse(savedNotes);
    }
  },
  methods: {
    addNewNote() {
      const colors = ['lightgreen'];
      const randomColor = colors[Math.floor(Math.random() * colors.length)]; 
      this.notes.push({
        content: '',
        width: 200,
        editing: true,
        color: randomColor,
        important:false
      });
      const lastIndex = this.notes.length - 1;
      this.$nextTick(() => {
        this.$refs.noteTextarea[lastIndex].focus(); 
      });
    },
    removeNote(index) {
      this.notes.splice(index, 1);
      this.removeFromLocalStorage(index); // Remove from localStorage
    },

    removeFromLocalStorage(index) {
    const notesInLocalStorage = JSON.parse(localStorage.getItem('stickyNotes'));

        if (notesInLocalStorage) {
        notesInLocalStorage.splice(index, 1);
        localStorage.setItem('stickyNotes', JSON.stringify(notesInLocalStorage));
        }
    },
    saveNote(index) {
      this.notes[index].editing = false;
      this.saveToLocalStorage();
    },
    saveToLocalStorage() {
      localStorage.setItem('stickyNotes', JSON.stringify(this.notes));
    },
    editNote(index) {
      this.notes[index].editing = !this.notes[index].editing;
    },
    toggleNoteImportance(index){
        this.notes[index].important = !this.notes[index].important;
        this.saveToLocalStorage();
    }
  }
};
</script>
<style scoped>
.button-add{
    position: -webkit-sticky;
    position: sticky;
    top: 10px;
    margin: 30px;
    display: inline-grid;
    align-items: center;
    justify-content: center;
    width: 150px;
    font-size: large;
    font-family: cursive;
    background-color: #70b1b9;
    color:white;
    box-shadow: 2px 3px 6px darkcyan;
}
.button-add i{
    background-color: #70b1b9;
}
i{
    font-size: 20px;
    font-weight: 600;
}
.important-button {
  background-color: pink;
}
button{
    box-shadow: 1px 1px grey;
    border: none;
    border-radius: 20px;
}
.notes-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  gap: 10px;
  margin: 0 5rem;
}

.sticky-note {
    display: inline-flex;
    flex-direction: column;
    justify-content: space-between;
    flex-wrap: wrap;
    align-items: center;
    padding: 5px;
    width:200px;
}

.note-header {
  display: flex;
  justify-content: space-between;
  margin-bottom: 5px;
}

textarea {
  width: 100%;
  height: 200px;
  font-family:cursive;
  font-size: 20px;
  border: none;
  border-radius: 5px;
  text-align: center;
  margin-bottom: 5px;
}
textarea:focus-visible{
    outline: 2px solid grey;
}
</style>
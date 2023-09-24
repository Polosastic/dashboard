<template>
    <div>
        <button @click="addNewNote" class="button-add">Add Note<i class="material-icons">add</i></button>
        <div class="notes-grid">
        <div v-for="(note, index) in notes" :key="index" class="sticky-note">
            <div class="note-header">
                <button @click="removeNote(index)" class="button-close" :style="{backgroundColor: note.color}"><i class="material-icons" :style="{backgroundColor: note.color}">close</i></button>
                <button @click="editNote(index)" class="button-edit" :style="{backgroundColor: note.color}"><i class="material-icons" :style="{backgroundColor: note.color}">edit</i></button>
            </div>
            <textarea 
            :disabled="!note.editing" v-model="note.content"  
            :style="{ width: note.width + 'px', backgroundColor: note.color}" 
            ref="noteTextarea" 
            placeholder="Type your note"
            class="textarea"></textarea>
            <button @click="saveNote(index)" class="button-save" :style="{backgroundColor: note.color}"><i class="material-icons" :style="{backgroundColor: note.color}">save</i></button>
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
      const colors = [ 'pink', 'lightskyblue', 'lightgreen'];
      const randomColor = colors[Math.floor(Math.random() * colors.length)]; 
      this.notes.push({
        content: '',
        width: 150,
        editing: true,
        color: randomColor
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
    }

  }
};
</script>
<style scoped>
.button-add{
    margin: 30px;
    display: inline-grid;
    align-items: center;
    justify-content: center;
    width: 125px;
    font-size: large;
    font-family: cursive;
    background-color: #9eabe7;
}
.button-add i{
    background-color: #9eabe7;
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
  margin: 0 4rem;
}

.sticky-note {
    display: inline-flex;
    background-color: yellow;
    flex-direction: column;
    justify-content: space-between;
    flex-wrap: wrap;
    align-items: center;
    padding:5px;
}

.note-header {
  display: flex;
  justify-content: space-between;
  margin-bottom: 5px;
  background-color: yellow; 
}

textarea {
  width: 100%;
  height: 200px;
  font-family:cursive;
  font-size: 20px;
  border: none;
  border-radius: 5px;
  text-align: center;
}
textarea:focus{
    outline: 2px solid grey;
}
</style>
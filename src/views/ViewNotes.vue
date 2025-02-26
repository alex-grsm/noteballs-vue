<template>
    <div class="notes">
        <div class="card has-background-primary-dark p-4">
            <div class="field">
                <div class="control">
                    <textarea
                        v-model="newNote"
                        class="textarea"
                        placeholder="Add a new note..."
                        ref="newNoteRef"
                    ></textarea>
                </div>
            </div>

            <div class="field is-grouped is-grouped-right">
                <div class="control">
                    <button
                        @click="addNote"
                        :disabled="!newNote"
                        class="button is-link has-background-primary">
                        Add New Note
                    </button>
                </div>
            </div>
        </div>

        <Note
            v-for="note in notes"
            :key="note.id"
            :note="note"
            @deleteClicked="deleteNote"
        />
    </div>
</template>

<script setup>
import { ref } from 'vue';
import { v4 as uuidv4 } from 'uuid';
import Note from '@/components/Notes/Note.vue';

const newNote = ref('');
const newNoteRef = ref(null);

const notes = ref([
    {
        id: 'id1',
        content: 'Lorem ipsum dolor sit, amet consectetur adipisicing elit. Error corrupti porro tempore, aliquid quod maxime aliquam veniam? Eveniet, debitis. Temporibus quos ea esse dolores debitis cumque, necessitatibus facere eos obcaecati.',
    },
    {
        id: 'id2',
        content: 'This is shorter note',
    },
]);

const addNote = () => {
    let id = uuidv4();

    let note = {
        id,
        content: newNote.value,
    };

    notes.value.unshift(note);
    newNote.value = '';
    newNoteRef.value.focus();
};

const deleteNote = (idToDelete) => {
    notes.value = notes.value.filter(note => note.id !== idToDelete);
}

</script>
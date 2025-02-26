<template>
    <div class="card">
        <header class="card-header">
            <p class="card-header-title">Component</p>
            <button class="card-header-icon" aria-label="more options">
                <span class="icon">
                    <i class="fas fa-angle-down" aria-hidden="true"></i>
                </span>
            </button>
        </header>
        <div class="card-content">
            <div class="content">
                {{ note.content }}
                <div class="has-text-right has-text-grey-light mt-2">
                    <small>{{ characterLength }}</small>
                </div>
            </div>
        </div>
        <footer class="card-footer">
            <a href="#" class="card-footer-item">Edit</a>
            <button
                @click.prevent="handleDeleteClick"
                class="card-footer-item">Delete
            </button>
        </footer>
    </div>
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps({
    note: {
        type: Object,
        required: true,
    },
});

const emit = defineEmits(['deleteClicked']);

const characterLength = computed(() => {
    let length = props.note.content.length;
    let description = length > 1 ? 'characters' : 'character';
    return `${length} ${description}`;
});

const handleDeleteClick = () => {
    emit('deleteClicked', props.note.id);
}
</script>
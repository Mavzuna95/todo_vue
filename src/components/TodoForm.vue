<template>
    <form
        class="sticky top-20 z-20 scroll-m-1 flex gap-2 border-t border-green-500 text-black bg-white py-4 justify-center pt-10"
        @submit.prevent="onSubmit">
        <input class=" w-4/5 rounded border-2 border-green-500 ps-2 text-sm " type="text" id="new-todo-input"
            name="new-todo" v-model="label"  autocomplete="off" />
        <button type="submit"
            class="text-green-500 enabled:hover:text-purple-400 border-2 border-green-500 hover:border-purple-500 rounded">
            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor"
                class="w-6 h-6">
                <path stroke-linecap="round" stroke-linejoin="round" d="M12 4.5v15m7.5-7.5h-15" />
            </svg>
        </button>
    </form>
</template>
<script>

export default {
    methods: {
        onSubmit() {
            if (this.label === "") {
                return alert('Заполните поля');
            }
            this.$emit('todo-added', this.label)
            this.label = ''

        },
        
    },
    data() {
        return {
            label: "",
        }
    },
};
</script>
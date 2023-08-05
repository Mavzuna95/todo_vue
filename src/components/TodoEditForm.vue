<template>
    <form class=" " @submit.prevent="onSubmit">
        <div class="flex justify-between w-full">
            <input :id="id" type="text" autocomplete="off" v-model.lazy.trim="newLabel"
                class="rounded border-2 border-green-500 " />

            <button type="button" class="border rounded-md px-3 mx-4 hover:bg-green-500 hover:text-white" @click="onCancel">
                Отмена
            </button>
            <button type="submit" class=" border rounded-md px-3  hover:bg-green-500 hover:text-white">
                Сохрaнить
            </button>
        </div>
    </form>
</template>
<script>
export default {
    props: {
        label: {
            type: String,
            required: true,
        },
        id: {
            type: String,
            required: true,
        },

    },
    data() {
        return {
            newLabel: this.label,
        };
    },
    methods: {
        onSubmit() {
            if (this.newLabel && this.newLabel !== this.label) {
                this.$emit("item-edited", this.newLabel);
            }
        },
        onCancel() {
            this.$emit("edit-cancelled");
        },
    },

};
</script>
<template>
    <div v-show="isFull">
        <h3>Выбран файл</h3>
        <div>
            {{selectedFile}}
        </div>
    <hr>
    </div>
</template>

<script>
export default {
    name: 'fsSelection',
    props: {
        selectedFile: {
            type: String,
            default: ''
        }
    },
    computed: {
        isFull() {
            return !(this.selectedFile ==='')
        }
    }
}
</script>

<style scoped>
</style>
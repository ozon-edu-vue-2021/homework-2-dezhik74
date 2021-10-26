<template>
    <button 
        @click="clickHandler" 
        class="file-link"
        :class="{ file__selected:isSelected }">
            <img :src="fileContent.type === 'file' ? fileImg : linkImg">
            {{fileContent.name}}
    </button>
</template>

<script>
import fileImg from '../assets/file_present_black_18dp.svg';
import linkImg from '../assets/link_black_18dp.svg';

export default {
    name: 'fsFile',
    props: {
        fileContent: {
            type: Object,
            default: () => {}
        },
        uniqueID : {
            type: Number,
            default: 0
        }
    },
    inject: ['selectedFileIDWrapper'],
    data () {
        return {
            fileImg: fileImg,
            linkImg: linkImg,
        }
    },
    computed: {
        isSelected: function (){
            return this.uniqueID === this.selectedFileIDWrapper.id
        }
    },
    methods: {
        clickHandler: function () {
            if (!this.isSelected) {
                this.$emit('select-file', this.fileContent.name, this.uniqueID);
            } else {
                this.$emit('unselect-file')
            }
        },
    }
}
</script>

<style scoped>
.file-link {
    cursor: pointer;
    border: 0;
    font: inherit;
    font-size: 16px;
    background-color: white;
    margin-bottom: 3px;
}

.file__selected {
    background-color: aqua;
}
</style>
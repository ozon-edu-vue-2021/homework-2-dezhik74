<template>
    <div 
        @click="$emit('select-file', fileContent.name)" 
        class="file-link">
            <img :src="fileContent.type === 'file' ? fileImg : linkImg">
            {{fileContent.name}}
    </div>
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
        }
    },
    data () {
        return {
            fileImg: fileImg,
            linkImg: linkImg
        }
    }
}
</script>

<style scoped>
.file-link {
    cursor: pointer;
}
</style>
<template>
    <div v-if="visible" >
        <span @click="clickHandler()" class="dir-name">
            <img :src="imgFolder" alt="">
            {{directoryContent.name}}
        </span>
        <div v-for='elem, i in directoryContent.contents' :key='`${elem.name}-${i}`'>
            <ul v-if='elem.type === "directory"'>
                <fs-directory
                    :directoryContent="elem" 
                    :visible="visibleChild"
                    v-on:select-file="selectFileHandler"
                />
            </ul>
            <ul v-else-if='(elem.type === "file" || elem.type === "link") && visibleChild'>
                <fs-file 
                    :fileContent="elem"
                    v-on:select-file="selectFileHandler"
                />
            </ul>
        </div>
    </div>
</template>

<script>

import fsFile from './fsFile.vue'
import imgFolder from '../assets/folder_black_18dp.svg'

export default {
    name: 'fsDirectory',
    components: {
        fsFile,
        'fs-directory': () => import ('./fsDirectory.vue')
        },
    props: {
        directoryContent: {
            type: Object,
            default: () => {}
        },
        visible: {
            type: Boolean,
            default: false
        }
    },
    data() {
        return {
            visibleChild: false,
            imgFolder: imgFolder,
        }
    },
    methods: {
        clickHandler: function () {
            this.visibleChild = ! this.visibleChild
        },
        selectFileHandler: function (path) {
            const result=this.directoryContent.name + '/' + path;
            this.$emit('select-file', result)
        }
    }

}
</script>

<style scoped>
li {
    list-style-type: none;
    margin-left: 15px;
    padding: 0;
}

ul {
    padding: 0;
    margin-left: 15px;
    margin-bottom: 0;
    margin-top: 0;
}

.dir-name {
    cursor: pointer;
}

</style>
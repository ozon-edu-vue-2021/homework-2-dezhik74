<template>
    <div>
        <button @click="clickHandler()" class="directory-name">
            <img :src="imgFolder" alt="">
            {{directoryContent.name}}
        </button>
        <div v-if="visibleChild">
            <ul class="directory-content">
                <div v-for='elem, i in directoryContent.contents' :key='`${elem.name}-${i}`'>
                    <fs-directory
                        v-if='elem.type === "directory"'
                        :directoryContent="elem" 
                        :visible="visibleChild"
                        v-on:select-file="selectFileHandler"
                        v-on:unselect-file="unselectHandler"
                    />
                    <fs-file v-else-if='(elem.type === "file" || elem.type === "link") && visibleChild'
                        :fileContent="elem"
                        v-on:unselect-file="unselectHandler"
                        v-on:select-file="selectFileHandler"
                    />
                </div>
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
        selectFileHandler: function (path, fileComponent) {
            const result=this.directoryContent.name + '/' + path;
            this.$emit('select-file', result, fileComponent)
        },
        unselectHandler: function () {
            console.log('DIR - unselect')
            this.$emit('unselect-file')
        },
    }

}
</script>

<style scoped>

.directory-content {
    padding: 0;
    margin-left: 15px;
    margin-bottom: 0px;
    margin-top: 0px;
}

.directory-name {
    cursor: pointer;
    border: 0;
    font: inherit;
    font-size: 16px;
    background-color: white;
    margin-bottom: 3px;
    /* padding: 0; */
}

.directory-name:active {
    border:0;

}

</style>
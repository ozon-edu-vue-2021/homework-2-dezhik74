<template>
    <div >
        <ul v-if='subSystem.type === "directory"'>
            {{subSystem.type}} + {{subSystem.name}}
            <fs-item 
                v-for='dir,i in subSystem.contents' 
                :key="`${dir.name}-${i}`"
                :subSystem="dir"
            />
        </ul>
        <li v-else-if='subSystem.type === "file"'>
            {{subSystem.type}} + {{subSystem.name}}
        </li>
        <li v-else-if='subSystem.type === "link"'>
            {{subSystem.type}} + {{subSystem.name}}
        </li>    
    </div>
</template>
<script>
export default {
    name: "fsItem",
    props: {
        subSystem: {
            type: Object,
            default: () => {}
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
}

</style>
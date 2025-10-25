<script>
    export default { 
        // Add code in appropriate places
        data() {
            return {
                items: ['keyboard', 'mouse', 'iPhone', 'macbook', 'adapter'],
                added: "",
            }
            
        },
    methods: {
        add: function(item) {
            this.items.push(item);
            this.added = ""
        }
    }
    }
</script>

<template>

    <h2>Shopping Cart</h2>
    <!-- TODO: Add Code Here -->
        <ul>
            <li v-for="(item,idx) of items">
                {{ item }}
                <button @click="items.splice(idx,1)">Delete!</button>
            </li>
        </ul>

        <input type="text" v-model="added">
        <button @click="add(added)">
            Add!
        </button>
   
</template>

<template>
    <div>
        <!-- <label for="owner-input">Enter owner's name  </label>
        <input id="owner-input" type="text" placeholder="June" v-model="owner"> -->
        <h1>Tasks to do</h1>
        <p class="subheading">List owner:
            <span v-if="editMode" class="owner">
                <input width="50" type="text" placeholder="June" v-model="owner">
                <button @click="editMode = !editMode">Ok</button>
            </span>
            <span v-else>
                <span class="owner">{{owner}}</span>
                <button @click="editMode = !editMode">Edit</button>
            </span>
        </p>
    </div>
</template>

<script lang="ts">

import { Vue, Component } from 'vue-property-decorator'

@Component
export default class Header extends Vue {
    owner = 'June';
    editMode = false;
}

</script>

<style lang="scss">

.subheading {
    font-size: 20px;
}

.owner {
    font-weight: 600;
    margin-right: 0.5rem;
}

#owner-input {
    margin-left: 1rem;
}

</style>

<template>
    <div>
        <h1>Tasks to do</h1>
        <p class="subheading">List owner:
            <span v-if="editMode" class="owner">
                <input class= "owner input" width="50" type="text" placeholder="June" v-model="owner" @keyup.enter="editMode = !editMode; updateOwner()">
                <button @click="editMode = !editMode; updateOwner()">Ok</button>
            </span>
            <span v-else>
                <span class="owner">{{owner}}</span>
                <button @click="editMode = !editMode">Edit</button>
            </span>
        </p>
    </div>
</template>

<script lang="ts">

import { Vue, Component, Prop } from 'vue-property-decorator'

@Component
export default class Header extends Vue {
  @Prop() owner!: string
  editMode = false;

  updateOwner () {
    this.$root.$emit('updateOwner', this.owner)
  }
}

</script>

<style lang="scss">

.subheading {
  font-size: 20px;
}

.input {
  width: 100px;
}

.owner {
  font-weight: 600;
  margin-right: 0.5rem;
}

#owner-input {
  margin-left: 1rem;
}

</style>

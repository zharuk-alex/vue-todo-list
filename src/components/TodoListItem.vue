<template>
  <v-list-item
    :value="task"
    class="py-1"
    active-class="deep-purple--text text--accent-4"
  >
    <template v-slot:default="{ active }">
      <v-list-item-action>
        <v-checkbox
          :input-value="active"
          color="deep-purple accent-4"
        ></v-checkbox>
      </v-list-item-action>
      <v-list-item-content>
        <v-list-item-title
          :class="{ 'text-decoration-line-through': active }"
          v-text="task.task"
        ></v-list-item-title>
      </v-list-item-content>
      <v-scale-transition>
        <v-list-item-action v-show="hover">
          <v-icon
            color="error"
            @click.stop="$emit('click-delete')"
            style="cursor: pointer"
          >
            mdi-delete-forever
          </v-icon>
        </v-list-item-action>
      </v-scale-transition>
    </template>
  </v-list-item>
</template>

<script>
  export default {
    props: {
      task: {
        type: Object,
      },
      hover: {
        type: Boolean,
        default: false,
      },
    },
  };
</script>

<style></style>

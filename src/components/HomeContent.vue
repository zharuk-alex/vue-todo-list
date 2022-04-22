<template>
  <default-layout>
    <template #header-top-left>
      <div class="day">{{ day }}</div>
      <div class="month">{{ month }}</div>
    </template>
    <template #header-top-right>
      <v-chip class="ma-2" small>Tasks {{ tasks.length }}</v-chip>
      <v-chip class="ma-2" small color="success">Done {{ doned }}</v-chip>
    </template>
    <template #header-sub>
      <v-text-field
        v-model="newTask"
        class="input-field-task ma-0 pa-0"
        prepend-inner-icon="mdi-plus"
        placeholder="Type your task and Press enter"
        hide-details
        @click:prepend-inner="addTask()"
        @keyup.enter="addTask()"
      >
      </v-text-field>
    </template>

    <template #content>
      <v-list class="text-left">
        <v-list-item-group v-model="tasksmodel" multiple>
          <template v-for="(task, index) in tasks">
            <v-hover :key="`item-${index}`" v-slot="{ hover }">
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
                  <v-list-item-action v-show="hover">
                    <v-icon
                      color="error"
                      @click.stop="removeTask(task.task)"
                      style="cursor: pointer"
                    >
                      mdi-delete-forever
                    </v-icon>
                  </v-list-item-action>
                </template>
              </v-list-item>
            </v-hover>
          </template>
        </v-list-item-group>
      </v-list>
    </template>
  </default-layout>
</template>

<script>
import faker from "@faker-js/faker";
import DefaultLayout from "@/layouts/default-layout.vue";
import moment from "moment";
export default {
  name: "HomeContent",
  components: {
    DefaultLayout,
  },
  data: () => ({
    newTask: "",
    tasks: [],
  }),
  computed: {
    tasksmodel: {
      get() {
        return this.tasks.filter((t) => (t.done ? t.task : false));
      },
      set(val) {
        this.tasks = this.tasks.map((task) => {
          let v_exist = val.find((v) => v.id == task.id);
          task.done = !!v_exist;
          return task;
        });
        return val;
      },
    },
    doned() {
      return Object.values(this.tasksmodel).length;
    },
    day() {
      return moment().format("dddd") + ", " + moment().format("Do");
    },
    month() {
      return moment().format("MMMM");
    },
    doneTasks() {
      return this.tasks.filter((t) => t.done).length;
    },
  },
  mounted() {
    this.tasks = Array.from({ length: 6 }, () => ({
      id: faker.datatype.number(),
      created_at: new Date(),
      task: faker.lorem.lines(1),
      done: faker.datatype.boolean(),
    }));
  },
  methods: {
    addTask() {
      if (this.newTask.length) {
        this.tasks.push({
          created_at: new Date(),
          task: this.newTask,
          done: false,
        });
        this.newTask = "";
      }
    },
    removeTask(val) {
      this.tasks = this.tasks.filter((t) => t.task !== val);
      this.tasksmodel = this.tasksmodel.filter((t) => t !== val);
    },
  },
};
</script>
<style lang="scss">
</style>

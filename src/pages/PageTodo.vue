<template>
  <q-page padding>
    <div class="absolute-center">
      <h5 v-show="elementVisible">
        Hey! Click the button and create Your first task!
        <q-btn icon="arrow_downward" flat />
      </h5>
    </div>
    <q-list v-if="Object.keys(tasks).length" bordered separator>
      <Task v-for="(task, key) in tasks" :task="task" :key="key" :id="key" />
    </q-list>
    <div class="absolute-bottom text-center q-mb-lg">
      <q-btn
        @click="showAddTask = true"
        round
        dense
        color="secondary"
        size="24px"
        icon="add"
      />
    </div>
    <q-dialog v-model="showAddTask">
      <AddTask />
    </q-dialog>
  </q-page>
</template>

<script>
import { mapGetters } from "vuex";
import Task from "../components/Tasks/Task";
import AddTask from "../components/Modals/AddTask";

export default {
  name: "PageTodo",
  data() {
    return {
      showAddTask: false,
      elementVisible: true
    };
  },
  computed: {
    ...mapGetters("tasks", ["tasks"])
  },

  created() {
    setTimeout(() => (this.elementVisible = false), 5000);
  },

  components: {
    Task,
    AddTask
  }
};
</script>

<template>
  <q-item
    @click="updateTask({ id: id, updates: { completed: !task.completed } })"
    clickable
    v-ripple
    rounded
    :input-style="{ backgroundColor: 'green' }"
  >
    <q-item-section side top>
      <q-checkbox v-model="task.completed" />
    </q-item-section>
    <q-item-section>
      <q-item-label :class="{ 'text-strikethrough': task.completed }">{{
        task.name
      }}</q-item-label>
    </q-item-section>

    <q-item-section side>
      <div class="row">
        <div class="column justify-center">
          <q-icon name="event" size="18px" class="q-mr-xs"></q-icon>
        </div>
        <div class="column">
          <q-item-label caption>{{ task.taskDate }}</q-item-label>
          <small>
            <q-item-label class="row justify-end" caption>{{
              task.taskTime
            }}</q-item-label>
          </small>
        </div>
      </div>
    </q-item-section>
    <q-item-section side>
      <div class="row">
        <q-btn
          @click.stop="showEditTask = true"
          push
          color="black"
          round
          icon="edit"
        />
        <q-btn
          @click.stop="promptDeleteTask(id)"
          push
          color="black"
          round
          icon="delete"
        />
      </div>
    </q-item-section>
    <q-dialog v-model="showEditTask">
      <EditTask :task="task" :id="id"  />
    </q-dialog>
  </q-item>
</template>

<script>
import { mapActions } from "vuex";
import EditTask from "../Modals/EditTask";

export default {
  props: ["task", "id"],
  data() {
    return {
      showEditTask: false
    };
  },
  components: {
    EditTask
  },
  methods: {
    ...mapActions("tasks", ["updateTask", "deleteTask"]),
    promptDeleteTask(id) {
      this.$q
        .dialog({
          title: "Delete task?",
          message: "Do u want to really delete task?",
          cancel: true,
          persistent: true
        })
        .onOk(() => {
          this.deleteTask(id);
        });
    }
  }
};
</script>

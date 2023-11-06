<template>
  <transition name="modal">
    <div v-if="showModal" class="modal-mask">
      <div class="modal-container">
        <div>
          <h4>Редактировать</h4>
        </div>
        <div class="model-body">
          <div class="headers">
            <span>ID: </span>
            <span>Название:</span>
            <span>Цена:</span>
            <span>Дата:</span>
          </div>
          <div>
            <input v-model="newProject.row_id">
            <input v-model="newProject.title">
            <input v-model="newProject.price">
            <input v-model="newProject.deadline">
          </div>
        </div>
        <div class="buttons">
          <span>Сохранить</span>
          <span @click="$emit('close')">Отменить</span>
        </div>
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  data() {
    return {
      newProject: []
    }
  },
  props: {
    showModal: Boolean,
    editedProject: Object,
  },
  beforeUpdate() {
    this.newProject = Object.assign({}, this.editedProject);
  },
}
</script>

<style lang="scss">
$colorSave: rgb(0, 189, 0);
$colorCancel: rgb(255, 0, 0);

.model-body {
  display: flex;
  input {
    margin-bottom: 17px;
  }
}

.headers {
  display: flex;
  flex-direction: column;
  align-items: flex-start;

  span {
    margin-bottom: 20px;
  }
}

.buttons {
  display: flex;
  justify-content: center;
  span {
    border: 1px solid black;
    border-radius: 5px;
    padding: 5px 10px;
    color: black;
    cursor: pointer;
    margin-right: 10px;

    &:first-child {
      background-color: $colorSave;
    }
    &:last-child {
      background-color: $colorCancel;
    }

    &:hover {
      opacity: 0.7;
    }
  }
}
.modal-mask {
  position: fixed;
  z-index: 9998;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  transition: opacity 0.3s ease;
}

.modal-container {
  width: 300px;
  margin: auto;
  padding: 20px 30px;
  background-color: #fff;
  border-radius: 2px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
  transition: all 0.3s ease;
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
}

.modal-body {
  margin: 20px 0;
}

.modal-enter-from {
  opacity: 0;
}

.modal-leave-to {
  opacity: 0;
}

.modal-enter-from .modal-container,
.modal-leave-to .modal-container {
  -webkit-transform: scale(1.1);
  transform: scale(1.1);
}
</style>
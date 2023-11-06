<template>
  <div class="container">
    <h1>Проекты</h1>
    <table class="table">
      <thead>
          <tr>
            <td>ID</td>
            <td>Название</td>
            <td>Цена</td>
            <td>Дата</td>
          </tr>
      </thead>
      <tbody>
        <tr v-for="item in projects" :key="item.row_id">
          <td>{{ item.row_id }}</td>
          <td>{{ item.title }}</td>
          <td>{{ item.price }}</td>
          <td>{{ new Date(item.deadline).toLocaleDateString() }}</td>
          <td>
            <div class="icons">
              <img 
                @click="more(item.row_id)" src="../../public/open.svg" alt="open"
              >
              <img 
                @click="edit(item)" src="../../public/edit.svg" alt="edit"
              >
              <img 
                @click="showDeleteDialog(item.row_id)" src="../../public/delete.svg" alt="delete"
              >
            </div>
          </td>
        </tr>
      </tbody>
        <tfoot>
          <tr>
            <td>Страница: 1</td>
          </tr>
        </tfoot>
      </table>
      <div class="btn">
        <button>press</button>
      </div>
      <project-dialog 
        :showModal="showModal"
        :editedProject="selectedItem"
        @close="showModal = false"
      />
      <yes-or-no 
        :showModal="showDelete"
        :row_id="wantToDelete"
        @close="showDelete = false"
        @delete="deleteRow"
      />
  </div>
</template>

<script>
import ProjectDialog from './dialogs/ProjectDialog.vue';
import YesOrNo from './dialogs/YesOrNo.vue';

export default {
  name: 'MainPage',
  data() {
    return {
      showModal: false,
      showDelete: false,
      wantToDelete: 0,
      selectedItem: [],
      count: this.projects.length,
      money: 0,
    }
  },
  components: {
    'project-dialog': ProjectDialog,
    'yes-or-no': YesOrNo,
  },
  props: {
    projects: Array
  },
  updated() {
    this.count = this.projects.length;
    this.getSumOfProjects();
  },
  methods: {
    getSumOfProjects() {
      let money = 0;
      for (let item in this.projects) {
        money += this.projects[item].price;
      }
      this.money = money;
    },
    more(id) {
      console.log(id);
    },
    edit(item) {
      console.log(item);
      this.selectedItem = item;
      this.showModal = true;
    },
    showDeleteDialog(row_id) {
      this.wantToDelete = row_id;
      this.showDelete = true;
    },
    deleteRow() {
      fetch(`http://localhost:8000/main/delete/${this.wantToDelete}`, {
        method: "DELETE"
      })
        .then(this.wantToDelete = 0)
        .then(this.showDelete = false);
    },
    updateRow() {
      fetch(`http://localhost:8000/main/update/${this.wantToDelete}`, {
        method: "PUT"
      })
        .then(this.wantToDelete = 0)
        .then(this.showDelete = false);
    }
  }
}
</script>

<style lang="scss">
.btn {
  margin-top: 20px;
  display: flex;
  justify-content: flex-end;

  button {
    border: 1px solid black;
    padding: 10px 30px;
    background-color: #2f00ff;
    color: #fff;
    text-transform: uppercase;
    cursor: pointer;

    &:hover {
      background-color: #1e00a3;
    }
  }
}
.icons {
  display: flex;
  justify-content: flex-end;

  img {
    width: 20px;
    margin-right: 10px;

    &:hover {
      cursor: pointer;
    }
  }
}
.container {
  max-width: 1500px;
  margin: auto;
}
.table {
	width: 100%;
	border: 5px solid #fff;
	border-collapse: collapse; 
	outline: 1px solid #000;
	font-size: 15px;


  td {
    width: 20%;
    padding: 7px;
    border-top: 3px solid #fff;
    border-bottom: 3px solid #fff;
    font-size: 15px;
  }
  tbody {
    tr {
      &:nth-child(even) {
        background: #f8f8f8!important;
      }
    }
  }
}
</style>
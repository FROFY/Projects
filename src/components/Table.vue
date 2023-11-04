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
              <tr v-for="item in projects" :key="item.id">
                  <td>{{ item.id }}</td>
                  <td>{{ item.name }}</td>
                  <td>{{ item.age }}</td>
                  <td>{{ new Date().toLocaleDateString() }}</td>
                  <td>
                      <div class="icons">
                          <img 
                            src="../../public/open.svg" alt="open"
                          >
                          <img 
                            @click="edit(item)" src="../../public/edit.svg" alt="edit"
                          >
                          <img 
                            @click="deleteRow(item.id)" src="../../public/delete.svg" alt="delete"
                          >
                      </div>
                  </td>
              </tr>
          </tbody>
      </table>
      <project-dialog 
        :showModal="showModal"
        :editedProject="selectedItem"
        @close="showModal = false"
      />
      <yes-or-no 
        :showModal="showDelete"
        :row_id="wantToDelete"
        @close="showDelete = false"
      />
  </div>
</template>

<script>
import ProjectDialog from './ProjectDialog.vue';
import YesOrNo from './YesOrNo.vue';

export default {
  name: 'MainPage',
  data() {
    return {
      showModal: false,
      showDelete: false,
      wantToDelete: 0,
      selectedItem: [],
    }
  },
  components: {
    'project-dialog': ProjectDialog,
    'yes-or-no': YesOrNo,
  },
  props: {
    projects: Object
  },
  methods: {
    // more(id) {
    //   console.log(id);
    // },
    edit(item) {
      console.log(item);
      this.selectedItem = item;
      this.showModal = true;
    },
    deleteRow(row_id) {
      this.wantToDelete = row_id;
      this.showDelete = true;
    },
  }
}
</script>

<style lang="scss">
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

  th {
    font-weight: bold;
    padding: 7px;
    background: #ffd300;
    text-align: left;
    font-size: 15px;
    border-top: 3px solid #fff;
    border-bottom: 3px solid #ffd300;
  }
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
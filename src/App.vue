<template>
  <div id="app">
    <div class="container">
      <div class="card">
        <p class="title mb-15">Todo List</p>
        <div class="todo">
          <div class="add flex between">
            
            <input class="input-add mb-15" type="text" name="todo" id="todo" v-model="newList" >
            
            <button class="btn-add" @click="insertTodo" >追加</button>
          </div>
          <div class="list flex between mb-5" v-for="item in todoLists" :key="item.id">
            <input class="input-update"  type="text" v-model="item.todo"> 
            <div>
            <button class="btn-update" @click="updateList(item.id, item.todo)">更新</button>
            <button class="btn-delete" @click="deleteList(item.id)">削除</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      newList: "",
      todoLists: [],
    };
  },
  
  methods: {
    async getTodo() {
      const resData = await axios.get("https://safe-depths-13271.herokuapp.com/api/test");
      this.todoLists = resData.data.data;
    },

    async insertTodo() {
      const sendData = {
        todo: this.newList
      }
     await axios.post("https://safe-depths-13271.herokuapp.com/api/test", sendData);
     await this.getTodo();
     this.newList= null
    },
    async updateList(id, todo) {  
      const sendData = {
         todo:todo
      };
      await axios.put("https://safe-depths-13271.herokuapp.com/api/test" + id, sendData);
      await this.getTodo();
    },
    async deleteList(id) {
      await axios.delete("https://safe-depths-13271.herokuapp.com/api/test" + id);
      await this.getTodo();
    },
  },
  created() {
    this.getTodo();
  },
};
</script>



<style scoped>
.container {
  background-color: #2d197c;
  height: 100vh;
  width: 100vw;
  position: relative;
}
.card {
  background-color: #fff;
  width: 50vw;
  padding: 30px;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  border-radius: 10px;
}
.title {
  font-weight: bold;
  font-size: 24px;
}
.between {
  justify-content: space-between;
}
.flex {
  display: flex;
}
.input-add {
  width: 80%;
  padding: 5px;
  border-radius: 5px;
  border: 1px solid #ccc;
  appearance: none;
  font-size: 14px;
  outline: none;
}
.mb-5 {
  margin-bottom: 5px;
}
.mb-15 {
  margin-bottom: 15px;
}
.btn-add {
    text-align: left;
    border: 2px solid #dc70fa;
    font-size: 12px;
    color: #dc70fa;
    background-color: #fff;
    font-weight: bold;
    padding: 8px 16px;
    border-radius: 5px;
    cursor: pointer;
    transition: 0.4s;
    outline: none;
}

.input-update {
  width: 30%;
  padding: 5px;
  border-radius: 5px;
  border: 1px solid #ccc;
  appearance: none;
  font-size: 14px;
  outline: none;
}
.btn-update {
  text-align: left;
  border: 2px solid #fa9770;
  font-size: 12px;
  color: #fa9770;
  background-color: #fff;
  font-weight: bold;
  padding: 8px 16px;
  border-radius: 5px;
  cursor: pointer;
  transition: 0.4s;
  outline: none;
}
.btn-delete {
  text-align: left;
  border: 2px solid #71fadc;
  font-size: 12px;
  color: #71fadc;
  background-color: #fff;
  font-weight: bold;
  padding: 8px 16px;
  border-radius: 5px;
  cursor: pointer;
  transition: 0.4s;
  outline: none;
}
</style>
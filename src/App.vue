<template>
  <div class="container mt-5">
    <div class="row text-center">
      <div class="col-12">
        <h3>To Do List with Vue.js</h3>
        <hr>
      </div>
    </div>
    <div class="row mt-2 text-center">
      <div class="col-12">
        <label for="exampleInputEmail1">Add a item</label>
        <input type="email" v-model="itemInput" placeholder="Add a item" class="form-control mx-auto"
          id="exampleInputEmail1" aria-describedby="emailHelp">
        <button type="button" :disabled="disableBtn" @click="addItem" class="btn btnAdd mt-2">Add</button>
        <button type="button" :disabled="editBtnClick" @click="addEditItem" class="btn btnEdit mt-2">Edit</button>
        <button type="button" @click="deleteAll" class="btn btn-danger mt-2">Delete All</button>
      </div>
    </div>   
       <div class="row mt-5">
      <div class="col-12">
        <ul class="list-group mx-auto">
          <transition-group name="fade" mode="out-in">
             <li class="list-group-item" v-for="(item,index) in itemList" v-bind:key="item">
            {{item}}
            <span class="deleteItem float-right"><i class="far fa-edit mr-2" @click="editItem(index)">
            </i><i class="fas fa-times" @click="deleteItem(index)"></i></span>
            </li>   
          </transition-group>                     
        </ul>

      </div>
    </div>  
  </div>
</template>

<script>
  export default {
    data() {
      return {
        itemList: [],
        itemInput: "",
        itemIndex : null,
        editBtnClick : true
      }
    },
    methods: {
      addItem() {
        this.itemList.push(this.itemInput);
        this.itemInput ="";
      },
      deleteItem(index) {
        if (confirm("Are you sure ?")) {
          this.itemList.splice(index, 1);
        }
      },
      deleteAll(){
        if (confirm("Are you sure ?")) {
          this.itemList = []
        }
      },
      editItem(index){
        this.itemInput = this.itemList[index];
        this.itemIndex = index;
        this.editBtnClick = false;
      },
       addEditItem(){
        this.itemList[this.itemIndex] = this.itemInput;
        this.itemInput = "";
        this.editBtnClick = true
      }
    
    },
    computed : {
      disableBtn(){
        if(this.itemInput.length > 0){
          return false;
        } else {
          return true;
        }
      }
    }
     
  }

</script>

<style>
  body {
    background-color: #f2f6f5;
  }
  h3 {
    color: #63707e;
  }
  .form-control {
    width: 40%;
  }
  .btn {
    width: 150px;
    color:white;
  }
  .btnAdd {
    background-color:#204051;
  }
  .btnEdit {
    background-color: #b0a160;
  }
  .list-group {
    width: 60%;
  }
  .list-group-item {
    background-color: #63707e;
    color: #f2f6f5;
  }
  .deleteItem {
    cursor: pointer;
  }
  .fade-enter {
    opacity: 0;
  }
  .fade-enter-active {
    transition: opacity .3s;
  }
  .fade-leave {
    opacity:1
  }
  .fade-leave-active {
    transition: opacity .3s;
    opacity: 0;
  }
  .fade-move {
    transition: opacity .3s;
  }


 
</style>

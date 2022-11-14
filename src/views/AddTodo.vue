<template>
  <div class="container">
    <div class="row">
      <div class="col p-3">
        <h2>Nuevo Todo</h2>
      </div>
    </div>
    <div class="row">
      <div class="col">
        <div class="form-group">
          <label htmlFor="todo"> Nombre:</label>
          <input type="text" class="form-control" v-model="state.todoitemlocal.todo" />
        </div>
        <div class="form-group">
            <label htmlFor="desc">Desc :</label>
            <textarea class="form-control" rows="3" id="desc" v-model="state.todoitemlocal.desc"></textarea>  
        </div>
        <div class="form-group">
            <button type="button" class="btn btn-primary m-1" @click="addTodo">Add</button>
            <button type="button" class="btn btn-primary m-1" @click="cancel">Cancel</button>
        </div>
      </div>
    </div>
  </div> 
</template>

<script>
import Constant from '../Constant';
import { reactive } from 'vue'
import { useStore } from 'vuex'
import { useRouter } from 'vue-router';

export default {
    setup() {
        const store = useStore();
        const router = useRouter();

        const state = reactive({ 
            todoitemlocal : { no:"", todo:"", desc:"", done:false } 
        });

        const addTodo = () => {
          if (state.todoitemlocal.todo.trim().length >= 2) {
            store.dispatch(Constant.ADD_TODO, { todoitem : state.todoitemlocal })
            router.push({ name:"todoList" });
          } else {
            alert('Nombre obligatorio');
          }
        }
        const cancel = () => {
            router.push({ name:"todoList"});
        }

        return { state, addTodo, cancel }
    }
}
</script>

<style>

</style>
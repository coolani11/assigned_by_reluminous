<template>
    <main>
      <h1>Task Board</h1>
      <p>Create a list of tasks</p>
  
      <div class="create-new">
        <input 
          type="text" 
          v-model="newTask" 
          placeholder="Add a new task" 
          @keypress.enter="addTask" />
        <button @click="addTask">Add</button>
      </div>
  
      <div class="tasks">
        <Task
          v-for="(task, i) in $store.state.tasks"
          :key="i"
          :task="task" />
      </div>
      <div>
        <v-btn color="rgb(214, 47, 47)" @click="logout">Logout</v-btn>
    </div>
    </main>

    
  </template>
  
  <script>
  export default {
    data (){
      return {
        newTask: ''
      }
    },
    methods: {
      addTask () {
        if (this.newTask) {
          this.$store.commit('ADD_TASK', this.newTask);
          this.newTask = '';
        }
      },
      async logout() {
      await this.$fire.auth.signOut();
      this.$router.replace("/");
    },
    }
  }

  
  </script>

  <style scoped>
* {
	margin: 0;
	padding: 0;
	box-sizing: border-box;
	font-family: 'Fira sans', sans-serif;
}



main {
	width: 100%;
	height: 100vh;
	display: flex;
	flex-direction: column;
	align-items: center;
	padding-top: 2rem;
}

main h1 {
	font-size: 2.5rem;
	text-transform: capitalize;
	margin-bottom: 0.5rem;
}

main h1 ~ p {
	margin-bottom: 2rem;
}

main .create-new {
	display: flex;
	justify-content: center;
	align-items: center;
	max-width: 480px;
}

main .create-new input {
	appearance: none;
	border: none;
	outline: none;
	border-bottom: 1px solid #FFF;
	background-color: transparent;
	color: #000000;
	font-size: 1.5rem;
	padding-top: 0.5rem;
	padding-bottom: 0.5rem;
	margin: 0;
	transition: 0.4s;
}

main .create-new input:focus {
	border-bottom-color: rgb(47, 214, 111);
}

main .create-new button {
	appearance: none;
	border: none;
	outline: none;
	background-color: rgb(47, 214, 111);
	text-transform: uppercase;
	font-weight: bold;
	color: #000;
	font-size: 1.5rem;
	padding: 0.5rem 1rem;
	border-radius: 0.5rem;
	margin-left: 0.5rem;
	cursor: pointer;
}

main .tasks {
	width: 100%;
	max-width: 480px;
	margin-top: 2rem;
}

main .tasks .task {
	display: flex;
	align-items: center;
	justify-content: space-between;
	background-color: #51C2E2;
	padding: 1rem;
	border-radius: 0.5rem;
	margin-bottom: 1rem;
}

main .tasks .task .buttons {
	min-width: fit-content;
}

main .tasks .task button {
	appearance: none;
	border: none;
	outline: none;
	background-color: rgb(47, 214, 111);
	text-transform: uppercase;
	font-weight: bold;
	color: #000;
	font-size: 0.875rem;
	padding: 0.5rem 1rem;
	border-radius: 0.5rem;
	margin-left: 0.5rem;
	cursor: pointer;
}

main .tasks .task button.delete {
	background-color: crimson;
	color: #EEE;
}

.tasks .task.is-complete {
	opacity: 0.7;
}

.tasks .task.is-complete .content {
	text-decoration: line-through;
}
</style>
  
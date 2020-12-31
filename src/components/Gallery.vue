<template>
  <div id="add">
    <h1>Add a image:</h1>
    <div>
      <h5>Enter url:</h5>
      <input type="text" id="url_input" placeholder="Enter url ..." autocomplete="off">
      <button @click="add_img(url)">Add</button>
    </div>
  </div>
  <div id="gallery">
    <div v-for="path in paths" :key="path" class="card">
      <img @click="pop_up" :src="path">
      <div class="footer">
        <h4>Image</h4>
        <a @click="remove_img(path)"><img id="trash-bin" src="data:image/svg+xml;base64,PHN2ZyBpZD0iQ2FwYV8xIiBlbmFibGUtYmFja2dyb3VuZD0ibmV3IDAgMCA0OTcgNDk3IiBoZWlnaHQ9IjUxMiIgdmlld0JveD0iMCAwIDQ5NyA0OTciIHdpZHRoPSI1MTIiIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyI+PGc+PHBhdGggZD0ibTMwNS43MzEgNjcuNTA1Yy0xLjI4NC0xOC4xMzktMTYuNDUyLTMyLjUwNS0zNC45MTItMzIuNTA1aC00Ni44MDNjLTE4LjQ2IDAtMzMuNjI4IDE0LjM2Ni0zNC45MTIgMzIuNTA1bC0xNy4zNDkgMTAtMTcuNzU0LTEwYzEuNzk4LTM3LjU4OSAzMi40NDYtNjcuNTA1IDY5Ljk5LTY3LjUwNWg0Ni44NTJjMzcuNTQ0IDAgNjguMTkyIDI5LjkxNiA2OS45OSA2Ny41MDVsLTE3LjQxOSAxMHoiIGZpbGw9IiNhMjlhYTUiLz48cGF0aCBkPSJtMTU3Ljg1IDQ3LjVoMzkuMzhjLTQuNjIgNS40OS03LjU5IDEyLjQyLTguMTMgMjBsLTE3LjM0IDEwLTE3Ljc2LTkuOTljLjMzLTYuOTggMS42Ni0xMy43IDMuODUtMjAuMDF6IiBmaWxsPSIjNzY2ZDc4Ii8+PHBhdGggZD0ibTM0MC44MyA2Ny41MS0xNy40MiAxMC0xNy42OC0xMC4wMWMtLjU0LTcuNTgtMy41LTE0LjUxLTguMTItMjBoMzkuMzdjMi4xOSA2LjMxIDMuNTIgMTMuMDMgMy44NSAyMC4wMXoiIGZpbGw9IiM3NjZkNzgiLz48cGF0aCBkPSJtMzQxLjU2MiA0OTdoLTE4Ni4xMjRjLTMxLjQ2OSAwLTU3LjYxOS0yNC4xMjctNTkuOTc5LTU1LjM0bC0yMy40NTktMjk2LjI5OSAxNzUuNDE4LTIzLjc3NiAxNzcuNTgyIDIzLjc3Ni0yMy40NTggMjk2LjI5OWMtMi4zNiAzMS4yMTMtMjguNTEgNTUuMzQtNTkuOTggNTUuMzR6IiBmaWxsPSIjYTI5YWE1Ii8+PHBhdGggZD0ibTQyNSAxNDUuMzYtMS41NiAxOS42OGgtMzQ5Ljg4bC0xLjU2LTE5LjY4IDE3NS40Mi0yMy43N3oiIGZpbGw9IiNhMjlhYTUiLz48cGF0aCBkPSJtNDI1IDE0NS4zNi0xNzcuNTgtMjMuNzctMTYzLjE5MyAyMi4xMTMtMTIuNTU2LTEuNjI5IDIzLjc4OSAyOTkuNTg2YzIuMzYgMzEuMjEgMjguNTEgNTUuMzQgNTkuOTggNTUuMzRoMjVjLTMxLjQ3IDAtNTcuNjItMjQuMTMtNTkuOTgtNTUuMzRsLTIwLjE5My0yNTUuMDQyYy0uOTIxLTExLjYzMiA4LjI3LTIxLjU3OSAxOS45MzgtMjEuNTc5aDMwMy4yMzV6IiBmaWxsPSIjNzY2ZDc4Ii8+PHBhdGggZD0ibTQ0My40NDUgMTQ1LjA0MmgtMzg5Ljg5Yy01LjUwNiAwLTkuOTctNC40NjQtOS45Ny05Ljk3di0uMTU2YzAtMzcuMjMgMzAuMTgxLTY3LjQxMiA2Ny40MTItNjcuNDEyaDI3NS4wMDdjMzcuMjMgMCA2Ny40MTIgMzAuMTgxIDY3LjQxMiA2Ny40MTJ2LjE1NmMtLjAwMSA1LjUwNy00LjQ2NSA5Ljk3LTkuOTcxIDkuOTd6IiBmaWxsPSIjYTI5YWE1Ii8+PGcgZmlsbD0iIzc2NmQ3OCI+PHBhdGggZD0ibTczLjU5IDEzNC45MnYuMTVjMCA1LjUxIDQuNDYgOS45NyA5Ljk2IDkuOTdoLTMwYy01LjUgMC05Ljk2LTQuNDYtOS45Ni05Ljk3di0uMTVjMC0zNy4yMyAzMC4xOC02Ny40MSA2Ny40MS02Ny40MWgzMGMtMzcuMjMgMC02Ny40MSAzMC4xOC02Ny40MSA2Ny40MXoiLz48cGF0aCBkPSJtMjQ4LjUgNDQyLjk4NmMtMTAuMDEyIDAtMTguMTI4LTguMTE2LTE4LjEyOC0xOC4xMjh2LTIwNy4zNTRjMC0xMC4wMTIgOC4xMTYtMTguMTI4IDE4LjEyOC0xOC4xMjhzMTguMTI4IDguMTE2IDE4LjEyOCAxOC4xMjh2MjA3LjM1NGMwIDEwLjAxMi04LjExNiAxOC4xMjgtMTguMTI4IDE4LjEyOHoiLz48cGF0aCBkPSJtMzM0Ljc3NyA0NDIuOTg3Yy0uNDgxIDAtLjk2Ni0uMDE5LTEuNDUzLS4wNTgtOS45OC0uNzkyLTE3LjQzLTkuNTI1LTE2LjYzNy0xOS41MDVsMTYuNDUzLTIwNy4zNTRjLjc5Mi05Ljk4IDkuNTItMTcuNDMxIDE5LjUwNS0xNi42MzcgOS45OC43OTIgMTcuNDMgOS41MjUgMTYuNjM3IDE5LjUwNWwtMTYuNDUzIDIwNy4zNTRjLS43NTQgOS40OTItOC42OTEgMTYuNjk1LTE4LjA1MiAxNi42OTV6Ii8+PHBhdGggZD0ibTE2Mi4yMjMgNDQyLjk4N2MtOS4zNjIgMC0xNy4yOTktNy4yMDItMTguMDUyLTE2LjY5NWwtMTYuNDUzLTIwNy4zNTRjLS43OTItOS45OCA2LjY1Ny0xOC43MTMgMTYuNjM3LTE5LjUwNSA5Ljk3OC0uODA1IDE4LjcxMyA2LjY1NiAxOS41MDUgMTYuNjM3bDE2LjQ1MyAyMDcuMzU0Yy43OTIgOS45OC02LjY1NyAxOC43MTMtMTYuNjM3IDE5LjUwNS0uNDg3LjA0LS45NzIuMDU4LTEuNDUzLjA1OHoiLz48L2c+PC9nPjwvc3ZnPg==" /></a>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Gallery',
  data() {
    return {
      paths: JSON.parse(localStorage.getItem("paths")) || []
    }
  },
  methods: {
    pop_up () {
      console.log("Clicked")
    },
    add_img () {
      let url = document.getElementById("url_input").value 
      this.paths.push(url)
      localStorage.setItem("paths", JSON.stringify(this.paths))
    },
    remove_img (path) {
      let index = this.paths.indexOf(path)
      this.paths.splice(index, 1)
      localStorage.setItem("paths", JSON.stringify(this.paths))
    }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto+Slab:wght@400;600;700&display=swap');
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: 'Roboto Slab';
    color: #fff;
  }
  img {
    width: 250px;
    height: 150px;
    margin: 5px;
    display: flex;
    justify-content: center;
    margin-right: 5px !important;
  }
  #gallery {
    margin-left: 105px;
    display: grid;
    grid-template-columns: 1fr 1fr 1fr 1fr;
    grid-gap: 5px;
    margin-top: 60px;
  }
  #add {
    margin-left: 100px;
    display: block;
  }
  input,button {
    display: block;
    margin: 5px;
  }
  h3,h4,h5 {
    margin-left: 5px;
  }
  body {
  background: #1e1f26 !important;
  min-width: 100%;
  min-height: 100%;
}
input,button {
  display: block;
  margin: 5px;
}
h1 {
  margin-left: 5px;
}
button {
  width: 100px;
  height: 40px;
  border: 1px solid transparent;
  border-radius: 5px;
  background: #444857;
  font-weight: bold;
  cursor: pointer;
}
button:active,button:focus,input:active,input:focus {
  outline: none !important;
  border: 1px solid transparent;
}
input {
  background: #444857;
  border: 1px solid transparent;
  border-radius: 5px;
  height: 35px;
  padding: 5px;
  width: 250px;
}
input:checked {
  background: #444857;
  color: #fff;
}
input:-internal-autofill-selected {
  background: #444857 !important;
  color: #fff !important;
}
input::placeholder {
  margin: 3px;
  font-size: 14px;
  font-weight: bold;
}
#trash-bin{
  width: 24px;
  height: 24px;
  cursor: pointer;
}
h4 {
  margin-left: 5px;
  margin-top: 4px;
}
#add div {
  margin-top: 15px;
}
.card {
  border: 1px solid #444857;
  width: 260px;
  background:  #444857;
  border-radius: 4px;
}
.footer {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  border: none;
}
</style>

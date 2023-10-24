<template>
  <div class="container">
    <section class="container__add-note-box">
      <h2>Welcome to Note App</h2>
      <p>Created by Reza <span>(Nuxt 3)</span></p>
      <input
        type="text"
        class="container__add-note-box__input"
        placeholder="Enter Your New Note"
        ref="noteInput"
        v-model="noteText"
        @keypress.enter="addNote"
      />
      <div class="container__add-note-box__color-container">
        <span
          class="container__add-note-box__color-container__color"
          style="--clr: #fff"
        >
        </span>
        <span
          class="container__add-note-box__color-container__color"
          style="--clr: #eee"
        >
        </span>
        <span
          class="container__add-note-box__color-container__color"
          style="--clr: #1abc9c"
        >
        </span>
        <span
          class="container__add-note-box__color-container__color"
          style="--clr: #55efc4"
        >
        </span>
        <span
          class="container__add-note-box__color-container__color"
          style="--clr: #81ecec"
        >
        </span>
        <span
          class="container__add-note-box__color-container__color"
          style="--clr: #00cec9"
        >
        </span>
        <span
          class="container__add-note-box__color-container__color"
          style="--clr: #f1c40f"
        >
        </span>
        <span
          class="container__add-note-box__color-container__color"
          style="--clr: #ff7675"
        >
        </span>
        <span
          class="container__add-note-box__color-container__color"
          style="--clr: #fd79a8"
        >
        </span>
        <span
          class="container__add-note-box__color-container__color"
          style="--clr: #ffeaa7"
        >
        </span>
      </div>
      <div class="container__add-note-box__btn-container">
        <button
          class="container__add-note-box__btn-container__btn container__add-note-box__btn-container__add-btn"
          ref="addNoteBtn"
          @click="addNote"
        >
          <svg
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 24 24"
            stroke-width="1.5"
            stroke="currentColor"
            class="w-6 h-6"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              d="M12 4.5v15m7.5-7.5h-15"
            />
          </svg>
        </button>
        <button
          class="container__add-note-box__btn-container__btn container__add-note-box__btn-container__delete-btn"
          ref="deleteNoteBtn"
        >
          <svg
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 24 24"
            stroke-width="1.5"
            stroke="currentColor"
            class="w-6 h-6"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              d="M14.74 9l-.346 9m-4.788 0L9.26 9m9.968-3.21c.342.052.682.107 1.022.166m-1.022-.165L18.16 19.673a2.25 2.25 0 01-2.244 2.077H8.084a2.25 2.25 0 01-2.244-2.077L4.772 5.79m14.456 0a48.108 48.108 0 00-3.478-.397m-12 .562c.34-.059.68-.114 1.022-.165m0 0a48.11 48.11 0 013.478-.397m7.5 0v-.916c0-1.18-.91-2.164-2.09-2.201a51.964 51.964 0 00-3.32 0c-1.18.037-2.09 1.022-2.09 2.201v.916m7.5 0a48.667 48.667 0 00-7.5 0"
            />
          </svg>
        </button>
      </div>
    </section>
    <section class="container__note-container">
      <div
        class="container__note-container__note-card"
        v-for="note in noteArray"
        :style="'background-color:' + note.bg"
        @click="deleteNote([note.id], $event)"
      >
        <p class="container__note-container__note-card__text">
          {{ note.text }}
        </p>
      </div>
    </section>
  </div>
</template>

<script setup>
let noteText = ref("");
let noteBg = ref("#fff");
let noteArray = ref([]);
const noteInput = ref(null);
const addNoteBtn = ref(null);
const deleteNoteBtn = ref(null);

function addNote() {
  noteArray.value.push({
    id: noteArray.value.length + 1,
    text: noteText.value,
    bg: noteBg.value,
  });
  updateLocalStorage();
  reset();
}

function deleteNote(props, event) {
  removeNote(props[0]);
}

function reset() {
  noteText.value = "";
  noteBg.value = "#fff";
}

function removeNote(id) {
  noteArray.value = noteArray.value.filter((note) => note.id !== id);
  updateLocalStorage();
}

function updateLocalStorage() {
  localStorage.setItem("notesList", JSON.stringify(noteArray.value));
}

onMounted(() => {
  noteArray.value = JSON.parse(localStorage.getItem("notesList")) || [];
  const colorList = document.querySelectorAll(
    ".container__add-note-box__color-container__color"
  );
  colorList.forEach((color) => {
    color.addEventListener("click", (e) => {
      noteBg.value = e.target.style.getPropertyValue("--clr");
    });
  });

  deleteNoteBtn.value.addEventListener("click", () => reset());
});
</script>

<style>
.container {
  width: 100vw;
  height: 85vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  row-gap: 50px;
}

.container__add-note-box {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  row-gap: 10px;
}

.container__add-note-box p span {
  color: #44bd32;
  font-weight: 700;
}

.container__add-note-box__input {
  all: unset;
  width: clamp(250px, 400px, 400px);
  padding: 10px;
  border: 1px solid #0000008e;
  border-radius: 5px;
  box-shadow: 0 2px 15px #0000004d;
  font-size: 1.2rem;
  background-color: v-bind(noteBg);
  transition: background-color 0.2s;
}

.container__add-note-box__color-container {
  margin-top: 10px;
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 5px;
}

.container__add-note-box__color-container__color {
  width: 30px;
  height: 30px;
  border-radius: 50%;
  background: var(--clr);
  box-shadow: 0 0 10px #00000049;
  cursor: pointer;
}

.container__note-container {
  width: clamp(280px, 80%, 900px);
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  gap: 20px;
}

.container__note-container__note-card {
  height: 80px;
  display: flex;
  box-shadow: 0 0 10px #00000049;
  padding: 10px;
  border-radius: 8px;
  cursor: pointer;
  border: 1px solid #00000062;
}

.container__note-container__note-card__text {
  font-size: 1.2rem;
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.container__add-note-box__btn-container {
  margin-top: 10px;
  width: clamp(250px, 400px, 400px);
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 10px;
}
.container__add-note-box__btn-container__btn {
  all: unset;
  width: 100px;
  padding: 10px;
  border: 2px solid #74b9ff;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 5px;
  color: #74b9ff;
  cursor: pointer;
  transition: 0.2s;
}

.container__add-note-box__btn-container__btn:hover {
  background-color: #74b9ff;
  color: #fff;
}

.container__add-note-box__btn-container__delete-btn {
  border-color: #d63031;
  color: #d63031;
}

.container__add-note-box__btn-container__delete-btn:hover {
  background-color: #d63031;
  color: #fff;
}

.container__add-note-box__btn-container__btn svg {
  width: 30px;
}
</style>

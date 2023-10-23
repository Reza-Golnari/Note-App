<template>
  <div class="container">
    <section class="container__add-note-box">
      <h2>Welcome to Note App</h2>
      <p>Created by Reza <span>(Nuxt 3)</span></p>
      <input
        type="text"
        class="container__add-note-box__input"
        placeholder="Enter Your New Note"
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
          style="--clr: #16a085"
        >
        </span>
        <span
          class="container__add-note-box__color-container__color"
          style="--clr: #2ecc71"
        >
        </span>
        <span
          class="container__add-note-box__color-container__color"
          style="--clr: #27ae60"
        >
        </span>
        <span
          class="container__add-note-box__color-container__color"
          style="--clr: #f1c40f"
        >
        </span>
        <span
          class="container__add-note-box__color-container__color"
          style="--clr: #e74c3c"
        >
        </span>
        <span
          class="container__add-note-box__color-container__color"
          style="--clr: #3498db"
        >
        </span>
        <span
          class="container__add-note-box__color-container__color"
          style="--clr: #2980b9"
        >
        </span>
      </div>
    </section>
    <section class="container__note-container">
      <div class="container__note-container__note-card">
        <p class="container__note-container__note-card__text">test note</p>
      </div>
      <div class="container__note-container__note-card">
        <p class="container__note-container__note-card__text">test note</p>
      </div>
      <div class="container__note-container__note-card">
        <p class="container__note-container__note-card__text">test note</p>
      </div>
      <div class="container__note-container__note-card">
        <p class="container__note-container__note-card__text">test note</p>
      </div>
      <div class="container__note-container__note-card">
        <p class="container__note-container__note-card__text">test note</p>
      </div>
      <div class="container__note-container__note-card">
        <p class="container__note-container__note-card__text">test note</p>
      </div>
      <div class="container__note-container__note-card">
        <p class="container__note-container__note-card__text">test note</p>
      </div>
    </section>
  </div>
</template>

<script setup></script>

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
}

.container__note-container__note-card__text {
  font-size: 1.2rem;
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>

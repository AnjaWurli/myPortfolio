<template>
  <div class="pw-check_container">
    <div class="pw-check_body">
      <h1 class="pw-check_h1">Password Check</h1>
      <form class="pw-check_form">
        <input
          data-cy="input1"
          :type="passwordType[0].inputType"
          v-model="word1"
          @keyup="checkPassword"
          class="pw-check_input"
        />
        <input
          data-cy="input2"
          :type="passwordType[0].inputType"
          v-model="word2"
          @keyup="checkPassword"
          class="pw-check_input"
        />
        <button
          data-cy="button"
          @click.prevent="togglePassword"
          class="pw-check_button"
        >
          {{ passwordType[0].buttonText }}
        </button>
      </form>
      <section class="pw-check_section">
        <p v-for="check of checks" :key="check.id" class="pw-check_p">
          {{ check.description }}
          <span :data-cy="check.id" :id="check.id"> {{ check.check }}</span>
        </p>
      </section>
    </div>
  </div>
</template>

<script>
import {
  equalFn,
  longFn,
  numFn,
  specFn,
  lowFn,
  upFn,
} from "../assets/passwordCheck/checkWord.js";

export default {
  data() {
    return {
      word1: "",
      word2: "",
      passwordType: [
        { inputType: "password", buttonText: "Show Passwords" },
        { inputType: "text", buttonText: "Hide Passwords" },
      ],
      wrong: "❌",
      right: "✅",
      checks: [
        { description: "passwords are equal", id: "equal", check: "❌" },
        { description: "lower case letters", id: "low", check: "❌" },
        { description: "upper case letters", id: "up", check: "❌" },
        { description: "contains numbers", id: "num", check: "❌" },
        { description: "special characters", id: "spec", check: "❌" },
        { description: "min. 10 characters", id: "long", check: "❌" },
      ],
    };
  },
  methods: {
    togglePassword() {
      this.passwordType.reverse();
    },
    checkPassword() {
      console.log(this.word1, this.word2);
      if (equalFn(this.word1, this.word2)) {
        this.checks[0].check = this.right;

        const checkObj = this.checks;
        const right = this.right;

        const toCheck = (x, y) => {
          if (x) {
            return (checkObj[y].check = right);
          }
        };

        toCheck(longFn(this.word1), 5);

        for (let letter of this.word1) {
          toCheck(numFn(letter), 3);
          toCheck(specFn(letter), 4);
          toCheck(lowFn(letter), 1);
          toCheck(upFn(letter), 2);
        }
      } else {
        this.checks.forEach((check) => (check.check = this.wrong));
      }
    },
  },
};
</script>

<style>
.pw-check_container {
  container-type: inline-size;
}
.pw-check_body {
  font-size: 23px;
  margin: 0;
  background-color: lightsalmon;
  font-family: "Open Sans", sans-serif;
  height: 85vh;
}

.pw-check_h1 {
  font-family: "Lobster", cursive;
  font-size: 3rem;
  color: white;
  filter: drop-shadow(black 3px 3px);
  text-align: center;
  margin: 0;
  padding: 2rem;
}

.pw-check_p {
  margin: 0;
}
.pw-check_section,
.pw-check_form {
  display: grid;
  justify-items: center;
  gap: 0.5rem;
  margin: 2rem;
}

.pw-check_form {
  padding-inline: 10%;
}

.pw-check_form > * {
  font-family: "Open Sans", sans-serif;
  border: 3px solid black;
  border-radius: 4px;
  width: 100%;
}

.pw-check_input {
  font-size: 1.7rem;
  text-align: center;
}
.pw-check_button {
  font-size: 1.7rem;
  background-color: black;
  color: white;
  cursor: pointer;
  width: 102%;
}

@container (min-width: 550px) {
  .pw-check_form {
    padding-inline: 20%;
  }
  .pw-check_body {
    font-size: 27px;
  }
}

@container (min-width: 750px) {
  .pw-check_body {
    display: grid;
    grid-template-columns: 1fr max-content;
    grid-template-rows: 30vh max-content;
    justify-content: center;
    align-items: center;
  }
  .pw-check_h1 {
    grid-column: span 2;
  }

  .pw-check_form {
    padding: 0;
  }
  .pw-check_input {
    max-width: 30rem;
  }
  .pw-check_button {
    max-width: 30.5rem;
  }
}
</style>

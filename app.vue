<template>
  <div class="body">
    <div id="ring">
      <h1 id="rounds">Round {{ rounds }}</h1>
      <div id="fight">
        <div
          v-for="fighter in players"
          :key="fighter.value.id"
          class="fighters"
          id="robot"
        >
          <div id="fighterHeads">
            <Icon :name="fighter.value.id" size="4rem"></Icon>
            <p id="points">Points: {{ fighter.value.points }}</p>
          </div>
          <Icon :name="fighter.value.selection" size="10rem"></Icon>
        </div>
      </div>
      <div id="playButtons">
        <button
          v-for="option in selection"
          :key="option"
          @click="chooseArtilary(option)"
        >
          <Icon :name="option" size="3rem"></Icon>
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
console.log("Fight!");

let robot = ref({
  id: "twemoji:robot",
  selection: "twemoji:raised-fist",
  points: 0,
});
let player = ref({
  id: "twemoji:adult",
  selection: "twemoji:raised-fist",
  points: 0,
});

let players = computed(() => {
  console.log("COMPUTED ROBOT: ", robot.value);
  console.log("COMPUTED PLAYER: ", player.value);
  return [robot, player];
});

// let players = ref([robot, player]);

const selection = ref([
  "twemoji:raised-fist",
  "twemoji:leftwards-hand",
  "twemoji:victory-hand",
]);

let playerSelection = ref(null);
let computerSelection = ref(null);
let rounds = ref(5);

const getComputerChoice = () => {
  const randomIndex = Math.floor(Math.random() * selection.value.length);
  return selection.value[randomIndex];
};

const playRound = (playerSelection, robotSelection) => {
  if (
    playerSelection === "twemoji:raised-fist" &&
    robotSelection === "twemoji:victory-hand"
  ) {
    player.value.selection = playerSelection;
    robot.value.selection = robotSelection;
    console.log(Number(player.value.points) + 1);
    player.value.points = Number(player.value.points) + 1;
    console.log("POINTS kumele iukba iAdd'ille apha: " + player.value.points);
    console.log(player.value);

    console.log(
      `You win! ${player.value.selection} beats ${robot.value.selection}`
    );
  } else if (
    player.value.selection === "twemoji:leftwards-hand" &&
    robot.value.selection === "twemoji:raised-fist"
  ) {
    player.value.selection = playerSelection;
    robot.value.selection = robotSelection;
    player.value.points = player.value.points + 1;
    console.log("POINTS kumele iukba iAdd'ille apha: " + player.value.points);
    console.log(player.value);

    console.log(
      `You win! ${player.value.selection} beats ${robot.value.selection}`
    );
  } else if (
    player.value.selection === "twemoji:victory-hand" &&
    robot.value.selection === "twemoji:raised-fist"
  ) {
    player.value.selection = playerSelection;
    robot.value.selection = robotSelection;
    player.value.points = player.value.points + 1;
    console.log("POINTS kumele iukba iAdd'ille apha: " + player.value.points);
    console.log(player.value);

    console.log(
      `You win! ${player.value.selection} beats ${robot.value.selection}`
    );
  }
  if (
    robot.value.selection === "twemoji:raised-fist" &&
    player.value.selection === "twemoji:victory-hand"
  ) {
    player.value.selection = playerSelection;
    robot.value.selection = robotSelection;
    robot.value.points = robot.value.points + 1;
    console.log(
      `You lose! ${robot.value.selection} beats ${player.value.selection}`
    );
  } else if (
    robot.value.selection === "twemoji:leftwards-hand" &&
    player.value.selection === "twemoji:raised-fist"
  ) {
    player.value.selection = playerSelection;
    robot.value.selection = robotSelection;
    robot.value.points = robot.value.points + 1;
    console.log(
      `You lose! ${robot.value.selection} beats ${player.value.selection}`
    );
  } else if (
    robot.value.selection === "twemoji:victory-hand" &&
    player.value.selection === "twemoji:raised-fist"
  ) {
    player.value.selection = playerSelection;
    robot.value.selection = robotSelection;
    robot.value.points = robot.value.points + 1;
    console.log(
      `You lose! ${robot.value.selection} beats ${player.value.selection}`
    );
  } else if (robot.value.selection === player.value.selection) {
    player.value.selection = playerSelection;
    robot.value.selection = robotSelection;
    console.log(`Draw!`);
  }
  if (rounds.value > 0) {
    rounds.value -= 1;
  } else {
    if (player.value.points > robot.value.points) {
      console.log("YOU HAVE WON THE MATCH");
    } else if (player.value.points < robot.value.points) {
      console.log("YOU HAVE LOST THE MATCH");
    } else {
      console.log("THE MATCH IS A DRAW");
    }
  }
};

const validateUserInput = () => {
  let playerInput = null;

  while (true) {
    // playerInput = prompt("twemoji:raised-fist, twemoji:leftwards-hand, twemoji:victory-hand?").toLowerCase();
    playerInput = "twemoji:raised-fist";

    if (
      playerInput != "twemoji:raised-fist" &&
      playerInput != "twemoji:leftwards-hand" &&
      playerInput != "twemoji:victory-hand"
    ) {
      // alert("Incorrect input. Enter either ['twemoji:raised-fist', 'twemoji:leftwards-hand' or 'twemoji:victory-hand']");
    } else {
      return playerInput;
    }
  }
};

const chooseArtilary = (chosenArtilery) => {
  computerSelection.value = getComputerChoice();
  console.log(
    "Computer[in cooseArtilary Function] chice: " + computerSelection.value
  );
  console.log("you selected Chosen Artilery: " + chosenArtilery);
  playRound(chosenArtilery, computerSelection.value);
  console.log(players.value);
};
</script>

<style>
.body {
  /* border: 1px solid red; */
  height: 100vh;
  background-image: url("assets/images/51ibDFf58kL._AC_SL1000_.jpg");
  background-size: cover;
  background-repeat: no-repeat;
  background-attachment: fixed;
  background-position: center;
  position: relative;
  display: flex;
  justify-content: space-around;
  align-items: center;
}

#ring {
  width: 90%;
  height: 90%;
  border: 1px solid red;
  display: flex;
  justify-content: space-around;
  align-items: center;
  flex-direction: column;
  /* padding: 5%; */
  /* background-color: rgb(252, 243, 231); */
}

#fight {
  /* height: 350px;
  width: 650px; */
  display: flex;
  justify-content: space-around;
  align-items: center;
  border: 1px solid teal;
  /* padding: 2%; */
  /* gap: 50%; */
}

.fighters {
  display: flex;
  border: 1px solid rgb(0, 102, 255);
  align-items: center;
  flex-direction: column;
  gap: 2rem;
}

.fighters > * {
  border: solid 2px white;
}

#fighterHeads {
}

#rounds {
  font-family: "GameSlash";
  font-size: 2.5rem;
}

#points {
  font-family: "Digital";
  /* font-size: 1.5rem; */
}
</style>

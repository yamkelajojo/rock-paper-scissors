<template>
  <div>
    <NuxtWelcome />
  </div>
</template>

<script setup>
import { ref } from 'vue';

const selection = ref(["rock", "paper", "scissors"])

const getComputerChoice = () =>{
  const randomIndex = Math.floor(Math.random() * selection.value.length);
  return selection.value[randomIndex];
}

const playRound = (playerSelection, computerSelection) => {
    if (playerSelection == "rock" && computerSelection == "scissors"){
      console.log(`You win! ${playerSelection} beats ${computerSelection}`)
    }
    else if (playerSelection == "paper" && computerSelection == "rock"){
      console.log(`You win! ${playerSelection} beats ${computerSelection}`) 
    }
    else if (playerSelection == "scissors" && computerSelection == "rock"){
      console.log(`You win! ${playerSelection} beats ${computerSelection}`) 
    }
    if (computerSelection == "rock" && playerSelection == "scissors"){
      console.log(`You lose! ${computerSelection} beats ${playerSelection}`)
    }
    else if (computerSelection == "paper" && playerSelection == "rock"){
      console.log(`You lose! ${computerSelection} beats ${playerSelection}`)
    }
    else if (computerSelection == "scissors" && playerSelection == "rock"){
      console.log(`You lose! ${computerSelection} beats ${playerSelection}`) 
    }
    else{
      console.log(`Draw!`)
    }
  }


// const validateUserInput= () => {
//   let validInput = false

//   while(validInput){
//     let playerSelection = prompt("Rock, Paper, Scissors?").toLowerCase();
    
//   }
// }


let rounds = 5 
while(rounds != 0){
  let computerSelection = getComputerChoice();
  // let playerSelection = prompt("Rock, Paper, Scissors?").toLowerCase();
  let playerSelection = 'rock'
  console.log(computerSelection)
  playRound(playerSelection, computerSelection);
  --rounds
}
</script>

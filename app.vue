<template>
  <div>
    <NuxtWelcome />
  </div>
</template>

<script setup>
import { ref } from 'vue';

const selection = ref(["rock", "paper", "scissors"])
let playerSelection = ref(null)

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
    else if (computerSelection == playerSelection){
      console.log(`Draw!`)
    }
  }


const validateUserInput= () => {
  let playerInput = null

  while(true){
    playerInput = prompt("Rock, Paper, Scissors?").toLowerCase();
    
    if(playerInput != "rock" && playerInput != "paper" && playerInput != "scissors"){
      alert("Incorrect input. Enter either ['Rock', 'Paper' or 'Scissors']")
    }
    else{
      return playerInput
    }
  }
  // console.log("Dojo")
}

let rounds = 2
while(rounds != 0){
  let computerSelection = getComputerChoice();
  console.log("Computer : " + computerSelection)
  playerSelection.value = validateUserInput()
  console.log("playerSelection : " + playerSelection.value)
  playRound(playerSelection.value, computerSelection);
  rounds = rounds - 1
}
</script>

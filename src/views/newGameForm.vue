<template>
    <div class="container">
         <v-text-field
            placeholder="player1"
            label="Name"
            clearable
            filled
          ></v-text-field>
          <v-text-field
            placeholder="player2"
            label="Name"
            clearable
            filled
          ></v-text-field>
          <v-btn to="/lobby"> Back to Lobby </v-btn>
          <v-btn v-on:click="createGame()"> Start Game </v-btn>
         </div>
</template>

<script>
export default {
    name : 'newGame',

    methods : {
        createGame() {
        let ws = new WebSocket("ws://localhost:9000/games/websocket")
        ws.onopen = e => {
            ws.send(JSON.stringify({_type : "createGame", player1 : "test1", player2 : "test2"}))
        };
        ws.onmessage = e => {
            ws.close()
        }
        }
    }
}
</script>

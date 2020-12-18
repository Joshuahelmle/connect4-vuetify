<template>
<div class="lobby">
  <h1>Lobby</h1>
    <div class="container">
   
    <p>There are currently no open Games, be the first to start playing!</p><br>
        <a href="/games/new">Start new Game</a>
     
        <p>
            These are the currently active games, join one if you want!<br>
            You can also create a <a href="/games/new">new</a> one.
        </p>
        <ul>
            <li v-for="game in games" :key="game.id">{{game.player1}} vs {{game.player2}}</li>
        </ul>  
    </div>
</div>
</template>

<script>
export default {
    name : 'Lobby',
    data()  {
        return {
            games : []
        }

    },
    created: function () {
       this.getGames();
    },
    methods : {
        getGames() {
            let ws = new WebSocket("ws://localhost:9000/games/websocket")
            ws.onopen = e => {
                ws.send(JSON.stringify({_type : "getGames"}))
            };
            ws.onmessage = e => {
                let msg = JSON.parse(e.data)
                if(msg.games){
                    this.games = JSON.parse(e.data).games
                    ws.close()
                }
                
            }
            
        }
    }
}
</script>

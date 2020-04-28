<template>
  <div>
    <div v-if="howtoPlay">
      <div class="descriptionTitle">How to Play</div>
      <div class="description">
        <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Ducimus fugiat vitae placeat, architecto quisquam facilis. Labore atque, nostrum quas recusandae, beatae quisquam inventore dolore officiis illo neque enim voluptate. Molestiae?</p>
      </div>
    </div>
    <div class="gameTable">
      <table>
        <tr>
          <td @click="write(0,0)">{{tableGame[0][0]}}</td>
          <td @click="write(0,1)">{{tableGame[0][1]}}</td>
          <td @click="write(0,2)">{{tableGame[0][2]}}</td>
        </tr>
        <tr>
          <td @click="write(1,0)">{{tableGame[1][0]}}</td>
          <td @click="write(1,1)">{{tableGame[1][1]}}</td>
          <td @click="write(1,2)">{{tableGame[1][2]}}</td>
        </tr>
        <tr>
          <td @click="write(2,0)" class="borderClear">{{tableGame[2][0]}}</td>
          <td @click="write(2,1)" class="borderClear">{{tableGame[2][1]}}</td>
          <td @click="write(2,2)" class="borderClear">{{tableGame[2][2]}}</td>
        </tr>
      </table>
      <div>
          <div v-if="gameFinish"  class="heartBeat finishGame">{{won}}
            <button @click="refrestGame" class="tryAgainButton">Try Again</button>
          </div>
         
      </div>
      <div class="button">
        <button v-if="howtoPlay" @click="playGame">Start</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      howtoPlay: true,
      tableGame: [
        ["X", "O", "X"],
        ["O", "X", "X"],
        ["O", "X", "O"]
      ],
      count: 0,
      gameFinish: false,
      won:"",
      draw:0
    };
  },
  methods: {
    playGame() {
      this.howtoPlay = false;
      this.tableGame = [
        ["", "", ""],
        ["", "", ""],
        ["", "", ""]
      ];
    },
    write(x, y) {
      if (this.gameFinish == false && this.tableGame[x][y] === "") {
        this.tableGame[x][y] = "X";
        this.$forceUpdate();
        this.count++;
        if (this.count < 5) {
          this.enemy();
        }
        
      }

      
      this.draw++;


      if (this.controlX()) {
        this.gameFinish = true;
        this.won = "Tebrikler oyunu X Kazandı";
      }
      if (this.controlO()) {
        this.gameFinish = true;
        this.won="Tebrikler oyunu O Kazandı";
      }

      
      if(this.draw >5 && this.gameFinish == false){
        this.won="Oyun Berabere";
        this.gameFinish = true;
      }

    },

    refrestGame(){
         location.reload();
    },

    enemy() {
      let x = Math.floor(Math.random() * 3);
      let y = Math.floor(Math.random() * 3);
      while (this.tableGame[x][y] !== "") {
        x = Math.floor(Math.random() * 3);
        y = Math.floor(Math.random() * 3);
      }
      this.tableGame[x][y] = "O";
      this.$forceUpdate();
    },

    controlX() {
      if (
        this.tableGame[0][0] === "X" &&
        this.tableGame[0][1] === "X" &&
        this.tableGame[0][2] === "X"
      ) {
        return true;
      } else if (
        this.tableGame[1][0] === "X" &&
        this.tableGame[1][1] === "X" &&
        this.tableGame[1][2] === "X"
      ) {
        return true;
      } else if (
        this.tableGame[2][0] === "X" &&
        this.tableGame[2][1] === "X" &&
        this.tableGame[2][2] === "X"
      ) {
        return true;
      } else if (
        this.tableGame[0][0] === "X" &&
        this.tableGame[1][0] === "X" &&
        this.tableGame[2][0] === "X"
      ) {
        return true;
      } else if (
        this.tableGame[0][1] === "X" &&
        this.tableGame[1][1] === "X" &&
        this.tableGame[2][1] === "X"
      ) {
        return true;
      } else if (
        this.tableGame[0][2] === "X" &&
        this.tableGame[1][2] === "X" &&
        this.tableGame[2][2] === "X"
      ) {
        return true;
      } else if (
      /* Çarpraz Kuralları */
        this.tableGame[0][0] === "X" &&
        this.tableGame[1][1] === "X" &&
        this.tableGame[2][2] === "X"
      ) {
        return true;
      } else if (
        this.tableGame[2][0] === "X" &&
        this.tableGame[1][1] === "X" &&
        this.tableGame[0][2] === "X"
      ) {
        return true;
      }
    },
    controlO() {
      if (
        this.tableGame[0][0] === "O" &&
        this.tableGame[0][1] === "O" &&
        this.tableGame[0][2] === "O"
      ) {
        return true;
      } else if (
        this.tableGame[1][0] === "O" &&
        this.tableGame[1][1] === "O" &&
        this.tableGame[1][2] === "O"
      ) {
        return true;
      } else if (
        this.tableGame[2][0] === "O" &&
        this.tableGame[2][1] === "O" &&
        this.tableGame[2][2] === "O"
      ) {
        return true;
      } else if (
        this.tableGame[0][0] === "O" &&
        this.tableGame[1][0] === "O" &&
        this.tableGame[2][0] === "O"
      ) {
        return true;
      } else if (
        this.tableGame[0][1] === "O" &&
        this.tableGame[1][1] === "O" &&
        this.tableGame[2][1] === "O"
      ) {
        return true;
      } else if (
        this.tableGame[0][2] === "O" &&
        this.tableGame[1][2] === "O" &&
        this.tableGame[2][2] === "O"
      ) {
        return true;
      } else if (
      /* Çarpraz Kuralları */
        this.tableGame[0][0] === "O" &&
        this.tableGame[1][1] === "O" &&
        this.tableGame[2][2] === "O"
      ) {
        return true;
      } else if (
        this.tableGame[2][0] === "O" &&
        this.tableGame[1][1] === "O" &&
        this.tableGame[0][2] === "O"
      ) {
        return true;
      }
    }
  }
};
</script>

<style scoped>

.heartBeat {
  animation-duration: 1s;

}



.descriptionTitle {
  text-align: center;
  font-size: 24px;
  margin: 10px 0;
  padding-top: 15px;
  color: #05668d;
  font-family: "Candara";
  letter-spacing: 5px;
  font-weight: bold;
}

.description {
  text-align: center;
  width: 400px;
  margin: 0 auto;
}
.description p {
  color: #313131;
  line-height: 32px;
  font-family: Candara;
}

.gameTable {
  width: 100%;
  height: auto;
  padding: 20px 0;
}

.gameTable table {
  text-align: center;
  margin: 0 auto;
}

.gameTable td {
  padding: 20px;
  font-size: 24px;
  border-left: 1px solid #d2d2d2;
  border-bottom: 1px solid #d2d2d2;
  transition: 500ms;
  font-family: Arial, Helvetica, sans-serif;
}
.gameTable td:hover {
  background: #f2f2f2;
}

.gameTable td:nth-child(1) {
  border-left: 0;
}
td.borderClear {
  border-bottom: 0;
}

.button {
  width: 100%;
  height: auto;
  margin: 20px auto;
  text-align: center;
}

.button button {
  padding: 13px 20px;
  background: #003049;
  color: #fff;
  font-weight: 700;
  border: 1px solid #eee;
  border-radius: 5px;
  outline: none;
  transition: 600ms;
  margin: 20px 0;
}
.button button:hover {
  background: #565a5c;
  padding: 13px 60px;
}

.finishGame{
  width:100%;
  background:#3f197c;
  text-align:center;
  color:#fff;
  box-shadow:2px 0px 8px #333;
  padding:20px 0;
  font-size: 24px;
  letter-spacing: 10px;
  margin-top:100px;
}
.tryAgainButton{
  width:115px;
  height:45px;
  background:#fff;
  border:1px solid #fff;
  color: #333;
  border-radius:10px 0 10px 0;
  font-weight:bold;
  display: block;
  margin:30px auto;
  margin-bottom:0px;
  outline: none;
}
.tryAgainButton:hover{
  background:#003049;
  transition:1s;
  border:0;
  color:#fff;
}
</style>
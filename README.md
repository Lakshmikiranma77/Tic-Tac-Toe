<div class='flex-container'>
  <div class='border'>
    <div class='selBorder'>
      <div class="selection">
        <h2 class="color">Select</h2>
        <button type="button" class="xs select" value="xs">  </button>
        <button type="button" class="os select" value="os">  </button>
      </div>
    </div>
    <div>
      <h1 class="title">Tic Tac Toe</h1>
    </div>
    <div class='box-row'>
      <button type="button" class="square a" value="a">  </button>
      <button type="button" class="square b" value="b">  </button>
      <button type="button" class="square c" value="c">  </button>
    </div>
    <div class='box-row'>
      <button type="button" class="square d" value="d">  </button>
      <button type="button" class="square e" value="e">  </button>
      <button type="button" class="square f" value="f">  </button>
    </div>
    <div class='box-row'>
      <button type="button" class="square g" value="g">  </button>
      <button type="button" class="square h" value="h">  </button>
      <button type="button" class="square i" value="i">  </button>
    </div>
    <button class="refresh" type="button" value="Refresh Page" onClick="window.location.href=window.location.href">Start Over</button>
    <div>
      <p class="dispWinner"></p>
    </div>
  </div>
</div>


html,
body {
  height: 100%;
}
body {
  margin: 0;
}
.flex-container {
  height: 100%;
  padding: 0;
  margin: 0;
  display: flex;
  align-items: center;
  justify-content: center;
}

.border {
  width: 165px;
  margin-top: -40px;
}

.box-row {
  display: flex;
  flex-direction: row;
}

h2 {
  margin: 2px;
}

button {
  height: 50px;
  width: 50px;
  margin-right: 4px;
  margin-bottom: 4px;
  border: 2px solid black;
  background-color: white;
}

.refresh {
  height: 40px;
  width: 158px;
  margin-right: 2px;
  border: 2px solid black;
  background-color: white;
  font-weight: bold;
}

.xs {
  background-color: red;
}

.os {
  background-color: blue;
}

.title {
  width: 158px;
  background-color: white;
  font-weight: bold;
  margin: -1px;
}

.dispWinner {
  width: 158px;
  height: 10px;
  background-color: white;
  font-weight: bold;
  text-align: center;
}

.selBorder {
  height: 100px;
}

.selection {
  margin: 5px;
  margin-left: -2px;
  text-align: center;
  border: solid black;
}

$(document).ready(function() {
  const winner = [/[a,b,c]/g, /[d,e,f]/g, /[g,h,i]/g, /[a,d,g]/g, /[b,e,h]/g, /[c,f,i]/g, /[a,e,i]/g, /[g,e,c]/g];
  let board = ["a",'b','c','d','e', 'f', 'g', 'h', 'i']
  let Player1 = {'name': 'Player 1', 'board' : '', 'class' : 'xs'}
  let Player2 = {'name': 'Player 2', 'board' : '', 'class' : 'os'}
  let currentPlayer = Player1
  let game = "Playing"

  function winCheck(moves, name) {
    const winner = [/[a,b,c]/g, /[d,e,f]/g, /[g,h,i]/g, /[a,d,g]/g, /[b,e,h]/g, /[c,f,i]/g, /[a,e,i]/g, /[g,e,c]/g];
    winner.forEach((x) => {
      won = moves.match(x)
      if(won !== null){
        if(won.length == 3){
          game = "Finished"
        }
      }
    })
  }

  function compMove(board) {
      let move = board[Math.floor(Math.random() * board.length)]
      var $button = $(`.${move}`);
      $button.addClass(currentPlayer.class)
      currentPlayer.board += $button.val()
      winCheck(currentPlayer.board, currentPlayer.name)
      if(game == "Finished") {
        $(".dispWinner").text(`You lost!`)
      }
      var index = board.indexOf($button.val());
      if (index > -1) {
        board.splice(index, 1);
      }
  }

  $(".square").click(function(){
    var $button = $(this);
    $button.addClass(currentPlayer.class)
    currentPlayer.board += $button.val()
    winCheck(currentPlayer.board, currentPlayer.name)
    console.log(board.length)
    if(game == "Finished") {
      $(".dispWinner").text(`You won!!`);

    } else if (board.length == 1){
        $(".dispWinner").text(`Its a draw!`)
    } else {
       var index = board.indexOf($button.val());
    if (index > -1) {
      board.splice(index, 1);
    }
    currentPlayer = Player2
    compMove(board)
    currentPlayer = Player1
    }
  })
  
  $('.select').click(function(){
    var $selector = $(this);
    if($selector.val() == 'xs'){
      Player1.class = 'xs';
      Player2.class = 'os'
    } else {
      Player1.class = 'os';
      Player2.class = 'xs'
    }
    $('.selection').fadeToggle(1000);
  });
})


var quicklist = ['TRUTH', 'TWIST', 'TOPAZ', 'TRICK', 'TRACK', 'TRIPS', 'TWINS', 'TRUCK', 'TRUST', 'TELLS', 'TARTS', 'THINK', 'TROPE', 'TIPSY'];
var input = document.getElementById('guess');
var button = document.getElementById('button');
var guess;

// change css class
var changeClass = function(cng, old, newClass){
  cng.className = cng.className.replace(old, newClass);
}

// game loop
  var gameloop = function(){
    // pick a word
    var rand = quicklist[Math.floor(Math.random() * quicklist.length)];
    var hasDuplicates = (/([a-zA-Z]).*?\1/).test(rand);
    console.log(rand);
    var pressn = 1;
  
  function getAllIndexes(arr, val) {
    var indexes = [], i;
    for(i = 0; i < arr.length; i++)
        if (arr[i] === val)
            indexes.push(i);
    return indexes;
  }
  
  // still undecided about this first letter being colored in or not
  //changeClass(document.getElementById("row1").firstElementChild, 'default', 'correct');
  // give first letter
  document.getElementById("row1").firstElementChild.innerHTML=rand[0];
  
  //guess event
  input.onkeypress = function(event) {
    if (event.key == "Enter" || event.keyCode == 13) {
      document.getElementById('smallMsg').innerHTML = "Green = correct letter, Yellow = wrong place";
      guess = input.value.toUpperCase();
      
      var current = "row" + pressn;
      // current row
      var childDivs = document.getElementById(current).getElementsByTagName('div');
      var c = 0; // correct count
      
      // right numer of letters?
      if(guess.length !== 5){
        document.getElementById('smallMsg').innerHTML = "Guesses must be 5 letters!";
        if(pressn===5){
          end("Sorry, you lost.");
        }
        pressn++;
        document.getElementById(current).firstElementChild.innerHTML=rand[0];
        return;
      }

      // check for correctness
      for( i=0; i<childDivs.length; i++ ) {
        childDivs[i].innerHTML = guess[i];
        
        // if letter match
        if(guess[i] == rand[i]){
          changeClass(childDivs[i], 'default', 'correct');
          // childDivs[i].innerHTML = rand[i];
          c++;

        } //wrong place?
        else if(rand.indexOf(guess[i])!=-1){
          if(hasDuplicates === false && childDivs[rand.indexOf(guess[i])].className != "square correct"){
            changeClass(childDivs[i], 'default', 'wrongplace');
          }//if
          else if(hasDuplicates === true){
            var ind = getAllIndexes(rand, guess[i]);
        
            if (ind.length > 1){
              for (var j=0; j<ind.length;j++){
                if(childDivs[ind[j]].className != "square correct" && childDivs[i].className != "square wrongplace"){
                  changeClass(childDivs[i], 'default', 'wrongplace');
                } //if
              }//for
            }//if
            else if (childDivs[rand.indexOf(guess[i])].className != "square correct"){
              changeClass(childDivs[i], 'default', 'wrongplace');
            }//else if
          } //else if
        } // else if
        
        input.value = ""; // clear input box
        
        if(c===5) {
          end("Congrats, you won!");
        } //if
        else if (pressn === 5){
          end("Sorry, you lost.");
        } //else if
      } //for
      pressn++; // number of guesses
    } //if keyenter
  } //input 
} //gameloop

// endgame
var end = function(msg){
  document.getElementById('msgBox').innerHTML=msg;
  changeClass(button, "invisible", "visible");
  document.getElementById('guess').readOnly = true;
}

// reset
var playagain = function(){
  document.getElementById('msgBox').innerHTML="Guess the Word!";
  document.getElementById('guess').readOnly = false;
  changeClass(button, "visible", "invisible");
  
  // clean boxes
  for(var i=1;i<6;i++){
    var resets = document.getElementById('row'+i).getElementsByTagName('div');
    for(var j=0;j<5;j++){
      resets[j].innerHTML="";
      if(resets[j].className == "square correct" || resets[j].className == "square wrongplace"){
        changeClass(resets[j], "correct", "default");
        changeClass(resets[j], "wrongplace", "default");
      }
    }
  }
  // restart the loop
  gameloop();
};

gameloop();

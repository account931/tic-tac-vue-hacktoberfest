<template>
    <div class="col-sm-12 col-xs-12 game-div">
    
        <!-- Time counter, how many seconds left till start of new game (happens when someone wins and user clicked "Start a new game") -->
        <div class="timer"> {{ this.$store.state.counterTime }}</div>
        <!-- End Time counter, how many seconds left till start of new game (happens when someone wins and user clicked "Start a new game") -->

        


        <!--------- Draw the game Field from sub-component './sub_components/gameField.vue' ------------> 
        <!-- Passing "vertical, horizontal, gameHits" as props to child sub-component --> 
        <draw-game-field  :verticalX  = "this.$store.state.vertical" 
                          :horizontalX= "this.$store.state.horizontal"        
                          :gameHitsX  = "this.$store.state.gameHits" 
                          @myEventX = "mainUserClick"/> <!-- pass this Parent's component method "mainUserClick" to child compon -->
        <!--------- End Draw the game Field from sub-component './sub_components/gameField.vue' --------> 
    
    
    
        {{ /* BELOW IS a commented build game logic, now reassigned to 'sub_components/gameField.vue'  */ }} 
        {{ /* If u wish to reinstate it, cut off 'draw-game-field' above(optional) + decomment all lines with starting text 'WORKING LINES COMMENTED HERE(before sub_comp deploy)', i.e code following this text  */ }}
        <!-- <h3> Original (TicTacStart_1.vue) table </h3> -->
        
        <!--------- Build game field REASSIGNED to sub-component <draw-game-field --------->
        <!-- Build game field based on array gameHits[], iterate over array, substitute for drawGameField() -->
        <!-- WORKING LINES COMMENTED HERE(before sub_comp deploy) --> <!--  <table class='tableX' id='gameTable'> -->
        
        
            <!-- building horizontal -->
            <!-- WORKING LINES COMMENTED HERE(before sub_comp deploy) --> <!-- <tr v-for="(item, index) in horizontal" :key="index"> -->
        
                <!-- building vertcial -->
                <!-- Uses fu**ing Vue iterator, instead of simple i++--> 

                <!-- WORKING LINES COMMENTED HERE(before sub_comp deploy) --> <!-- <template v-for="(item2, index2) in vertical"> -->  <!-- uses template to use v-loop without html tag -->
                    <!-- Build empty td cell, used for building IF this iterator is undefined in gameHits[] -->            
                    <!-- WORKING LINES COMMENTED HERE(before sub_comp deploy) -->  <!-- <td :key="index2" v-if="booksGet[index * horizontal + index2] == undefined " class="game-cell" :id="index * horizontal + index2"  @click="mainUserClick(index * horizontal + index2)"> -->
                        <!-- Nul => {{index * horizontal + index2}} -->
                        <!-- {{index * horizontal + index2}} --> <!-- fu**ing iterator-->
                        <!-- {{item2}} -->                    
                    <!-- WORKING LINES COMMENTED HERE(before sub_comp deploy) -->  <!-- </td> -->
            
                    <!-- Build taken td cell ("0" of "X"), used for building IF this iterator is defined in gameHits[] as ("0" of "X") -->            
                    <!-- WORKING LINES COMMENTED HERE(before sub_comp deploy) -->  <!--<td :key="index2" v-if="booksGet[index * horizontal + index2] != undefined " class="game-cell" :id="index * horizontal + index2"> -->   <!-- if array el is not undefined, dispplay it's value -->
                    <!-- WORKING LINES COMMENTED HERE(before sub_comp deploy) -->  <!--  {{ booksGet[index * horizontal + index2 ] }} --> 
                        <!-- {{index * horizontal + index3}} --> <!-- fu**ing iterator-->
                    <!-- WORKING LINES COMMENTED HERE(before sub_comp deploy) -->  <!-- </td> -->
            
                <!-- WORKING LINES COMMENTED HERE(before sub_comp deploy) -->   <!-- </template> -->
            
            <!-- WORKING LINES COMMENTED HERE(before sub_comp deploy) -->  <!-- </tr> -->
            <!-- iterate over array -->
        
       <!-- WORKING LINES COMMENTED HERE(before sub_comp deploy) -->  <!-- </table> -->
      
     
        
       
       
    </div>
</template>




<script>
//import function from other external file
import {computedAnswerFile} from './sub_functions/computedAnswer.js';  //name in {} i.e 'computedAnswerFile' must be cooherent to name in "export const computedAnswerFile" in '/sub_functions/computedAnswer.js'

//using other sub-component, in this case a component to draw the game Field
import drawGameField from './sub_components/gameField.vue';  //import file from same level folder
	     
//import Swal from 'sweetalert2'; //simple sweetalert2 not working in Vue, have to use vue-sweetalert2
//start import Vue-sweetalert2 ---------
import Vue from 'vue'
import VueSweetalert2 from 'vue-sweetalert2';
// If you don't need the styles, do not connect
import 'sweetalert2/dist/sweetalert2.min.css';
Vue.use(VueSweetalert2);
//end import Vue-sweetalert2 --------

export default {
  name: 'TicTacStart_1',
  
  //using other sub-component, e.g sub-component to draw game field
  components: {
      'draw-game-field': drawGameField 
  },
  
  
  data () {
    return {
      msg      : 'Welcome to Tic tac on Vue Vuex',
	  //has gone to Vuex store
	  /*
      maxSize  : 9, 
      gameHits : new Array(9), //array contains users hits, both user and bot, i.e [x, x, 0, x, x....]
      winCombination: [ [0, 1, 2], [3, 4, 5], [6, 7, 8], [0, 3, 6], [1, 4, 7], [2, 5, 8], [0, 4, 8], [2, 4, 6 ] ], //win combinations: horiz, vertical, diagonal
      
      horizontal : 3, //value to build game field (table)
      vertical   : 3,
	  idIterator : 0,
      counterTime: '', //used to counting sec till new game will start
      userCanPlay: true, // flag if it is user's turn to play, to prevent user's multiple clicking without his turn
      */
    }
  },
  
  computed: {
        booksGet () { //to ensure reactivity
            return this.gameHits;
        },

              
    },
  
  methods: {
              
           /*
            |--------------------------------------------------------------------------
            | When User Clicks cell, User "X"
            |--------------------------------------------------------------------------
            |
            |
            */
            mainUserClick(item) { 
            
                //if it is not user's turn to play, stop it
                if(!this.$store.state.userCanPlay){
                   return false;
                }
                
				
                //below next line was reassigned to Vuex (+2 lines below)
                //this.gameHits.splice(item, 1, "x"); //2 Mega Fixes: 1.to ensure reactivity should use this approach to change array, not this.gameHits[item] = "x"  2. Use splice this way => this.gameHits.splice(item, 1, "x"); //(what array el index to start with, delete 1, new value)

                //trigger Vuex mutation to update Vuex array gameHits[]
                this.$store.dispatch('updateVuexGameHitsX', item); //working example how to change Vuex store from child component  


                //below line was reassigned to Vuex (+2 lines below)
                //this.userCanPlay = false; //user can not play unless a bot makes a turn, changed to true in computedAnswer 
                
				//trigger Vuex mutation to update Vuex boolean userCanPlay
                this.$store.dispatch('updateUserCanPlay', false); //working example how to change Vuex store from child component  


                console.log(this.$store.state.gameHits);
                
                
                if(this.checkGame() == true){
			       return false; //to prevent computedAnswer fire if the winner is present
		        } 
                
		        //this.computedAnswer(); //reassigned to external file, see next line 
                computedAnswerFile.computedAnswer(this); //Call the function from external file (/sub_functions/computedAnswer.js). Must pass this or it will crash (e.g it needs this to use this.gameHits, etc)

            },
            
            
            
            
            
            
	        /*
            |--------------------------------------------------------------------------
            | AnnounceWinner subfunction (used in checkGame(). 
	        | Uses isConfirm for better UI (after the user/bot win, user clicks OK in swal and gamefield doesn't vanish immetiately, so user can see the results)
            |--------------------------------------------------------------------------
            |
            |
            */
	        AnnounceWinner(winnerText){
		        let timeDelay = 1800;
                                
                //VUE Sweet alert 2, ordinary sweetAlert does not work in Vue,  have to use vue-sweetalert2
                this.$swal.fire({  //or this.$swal  or Vue.swal
                    html:true, 
                    title: winnerText,
                    text: "You won't be able to revert this!",
                    icon: 'success',
                    showCancelButton: true,
                    confirmButtonColor: '#3085d6',
                    cancelButtonColor: '#d33',
                    confirmButtonText: 'Good, start new game!',
                    cancelButtonText: "No, cancel it!",
					keydownListenerCapture: false, //ignore esc button to close the pop
					allowOutsideClick: false       //don't allow outside click to close the pop-up
                }).then((result) => {
                    if (result.isConfirmed) {
                        
                        this.timeLeftToStartLeft(timeDelay);
                        
			            //reset the game field, i.e start new game
			            setTimeout(() => {
						    
							
							
                            //below next line was reassigned to Vuex (+2 lines below)
                            //this.gameHits = new Array(this.maxSize); //clear the array //new Array(this.maxSize);

                            //trigger Vuex mutation to update Vuex array gameHits[]
                            this.$store.dispatch('resetVuexGameHits'); //working example how to change Vuex store from child component  



                            this.clearRedCells();
			                //drawGameField(true); //redraw new game field
		                }, timeDelay); 
			    
                    }
                }); 

	        },
	
    
    
    
    
    
            //subfunction, used in AnnounceWinner(), counts second till new game start (happens when someone won & user clicked "Start new game")
            timeLeftToStartLeft(timeX){
                
				//below next line was reassigned to Vuex (+2 lines below)
				//this.counterTime = timeX;

				//trigger Vuex mutation to set Vuex var counterTime
                this.$store.dispatch('setVuexCounterTime', timeX);
					
                //counts time-- with setInterval 
                let timerId = setInterval(() => {
				
					
					//below next line was reassigned to Vuex (+2 lines below)
                    //this.counterTime = this.counterTime - 5;
					
                    //trigger Vuex mutation to update Vuex var counterTime
                    this.$store.dispatch('updateVuexCounterTime', 5); //working example how to change Vuex store from child component  
			
			
                    
                    //stop counting if goes < 0
                    if(this.$store.state.counterTime <= 0){
                        clearInterval(timerId);
					   

                        //below next line was reassigned to Vuex (+2 lines below)
					    //this.counterTime = ''; //get time vanish

				        //trigger Vuex mutation to set Vuex var counterTime
                        this.$store.dispatch('setVuexCounterTime', '');
				
                    }
		        }, 1);
                
                // stop setInterval anyway in timeX arg (in case prev counting did not reach 0). Working
                /* setTimeout(() => { 
                    clearInterval(timerId);
                    this.$store.state.counterTime = ''; //get time vanish                    
                 }, timeX);   */              
                
            },
            
            
            //subfunction, used in drawRedLine() and checkGame()
	        //gets the index of winning combination sub-array of array winCombination, i.e return 2 
            getWinningArrayNumber(){
		
		        for(let i = 0; i < this.$store.state.gameHits.length; i++){           //this.gameHits.length;
			        for(let j = 0; j < this.$store.state.winCombination.length; j++){ //this.winCombination.length
				        for(let n = 0; n < this.$store.state.winCombination[j].length; n++){
					        let temp1 = this.$store.state.winCombination[j][n];
					        let temp2 = this.$store.state.winCombination[j][n+1];
					        let temp3 = this.$store.state.winCombination[j][n+2];
					        if(this.$store.state.gameHits[temp1] == this.$store.state.gameHits[temp2] && this.$store.state.gameHits[temp1] == this.$store.state.gameHits[temp3] && this.$store.state.gameHits[temp2] == this.$store.state.gameHits[temp3] && this.$store.state.gameHits[temp1] != undefined){
					            //alert(j);
						        return j;
					        } 
				        }
		            }
	            }
		
            },
    
    
    
            /*
            |--------------------------------------------------------------------------
            | drawRedLine for winner combination
            |--------------------------------------------------------------------------
            |
            |
            */
	        drawRedLine(){
		        //alert("draw line");
		
                let result = this.getWinningArrayNumber(); //gets the index of winning combination sub-array of array winCombination, i.e return 2 
		        //alert("result winCombination: " + result);
		
                /*
		        setTimeout(() => { //Mega Fix, otherwise without this delay, if Bot wins, it colorRow() first and then as specified in computedAnswer() redrasw game field with delay erasing colored cells
			       colorRow(winCombination[result][0], winCombination[result][1], winCombination[result][2]);	//Fix
		        }, 1200);
                */
                
                this.colorRow(this.$store.state.winCombination[result][0], this.$store.state.winCombination[result][1], this.$store.state.winCombination[result][2]);	//Fix

            },
            
            
            //subfunction, used in drawRedLine()
	        colorRow(cell1, cell2, cell3){ 
	            document.getElementById(cell1).classList.add("redCell");
                document.getElementById(cell2).className += " redCell";
                document.getElementById(cell3).className += " redCell";

	        },
	
    
    
            //subfunction, used in AnnounceWinner(), on starting new game, reset red winning cells
            clearRedCells(){
                for(let i = 0; i < document.getElementsByClassName('game-cell').length; i++ ){
                    document.getElementsByClassName('game-cell')[i].classList.remove("redCell");
                }
            },
            
            
            
            
            
           /*
            |--------------------------------------------------------------------------
            | Check winner based on array gameHits[] and array winCombination[]
            |--------------------------------------------------------------------------
            |
            |
            */
            checkGame() {
                //variant 2, more short elegant variant ---------------
		        let winnerText;
	            let result = this.getWinningArrayNumber(); //gets the index of winning combination sub-array of array winCombination, i.e return 2 
                //alert(result);
                
                
                if(result == null){  //no winning match was found
		            //alert("null, i.e no winning match so far");
			
			        //check while no win match if it an even situation
			
		            //check if Players are even
		            let checkFlag = false;
		            for (var i = 0, l = this.$store.state.gameHits.length; i < l; i++) { //this.gameHits.length
                        if (typeof(this.$store.state.gameHits[i]) =='undefined') { //checks if any array element is undefined, meaning the gane is not finished yet
                            checkFlag = true;
			                break;
                        } 
                    }; 
		            
		            if(checkFlag == false ){ //true if finds no undefined element
		                //alert("even");
			            this.AnnounceWinner("So close. You are even");
						
						//below line was reassigned to Vuex (+2 lines below)
                        //this.userCanPlay = true; //enable user's turn to play
						
						//trigger Vuex mutation to update Vuex boolean userCanPlay
                        this.$store.dispatch('updateUserCanPlay', true); //working example how to change Vuex store from child component  

                        return true;	//stop		
		            }
			        
			        return false;
		        }
		
		
		
		        //Goes here only if winning combination is found. Detect who wins "X" or "0"
		        let t = this.$store.state.winCombination[result][0]; //gets value of just one first cell (or other 2 must be tha same value)
		        if(this.$store.state.gameHits[t] == "x"){
			        //alert("X won");
			        winnerText = "Winner is  <i> You </i> !!! You <i>  won </i>!!!!";
					
					
                //below line was reassigned to Vuex (+2 lines below)
                //this.userCanPlay = true; //enable user's turn to play   
				
				//trigger Vuex mutation to update Vuex boolean userCanPlay
                this.$store.dispatch('updateUserCanPlay', true); //working example how to change Vuex store from child component  



                    
		        } else {
				
			        //alert("0 won");
			        winnerText = "Screw you. Bot won. Winner is <i> Bot</i> !!! ";
		        }
		        this.drawRedLine(); //draw red line for winning cell combination
                this.AnnounceWinner(winnerText);
		        return true;
		        // End variant 2, more short elegant variant ---------------
            
                
            
            },
            
            
            
            
            
            
           /*
            |--------------------------------------------------------------------------
            | computedAnswer
            |--------------------------------------------------------------------------
            |
            |
            */
            //has gone/reassigned/transfered to /sub_functions/computedAnswer.js
            /*computedAnswer() {
                
                let delayTime = 300; //delay time
                
                //AI goes fisrt before random number assignment (if conditions are met) ------------
                //(only several combinations are programmed, feel free to add more)
                
                //Section when Bot tries to prevent the user to win by using counter-measures (prevent user from completing full "x" combination)
                //if first horizont line == [x, x, undefined]
		        if (this.gameHits[0] == "x" && this.gameHits[1] == "x" && this.gameHits[2] == undefined) {
		            this.AI_engage_subfunction(2, "0");   //arrayIndex, cellValue(always "0")
			        return true;
		        }
		        alert(88);
		        //if first horizont line == [undefined, x, x]
		        if (this.gameHits[1] == "x" && this.gameHits[2] == "x" && this.gameHits[0] == undefined) {
		            this.AI_engage_subfunction(0, "0");  //arrayIndex, cellValue(always "0")
                    return true;			
		        }
		
		        //if 2nd horizont line == [x, x, undefined]
		        if (this.gameHits[3] == "x" && this.gameHits[4] == "x" && this.gameHits[5] == undefined) {
		           this.AI_engage_subfunction(5, "0");  //arrayIndex, cellValue(always "0") 
			       return true;
		        }
                
                //Section when Bot tries to win by completing full "0" combination
                //if 1st horizont line == [0, 0, undefined]
		        if (this.gameHits[0] == "0" && this.gameHits[1] == "0" && this.gameHits[2] == undefined) {
		           this.AI_engage_subfunction(2, "0");  //arrayIndex, cellValue(always "0") 
			       return true;
		        }
                //End AI goes fisrt before random number assignment (if conditions are met) ------------
                
                
                
                
                //Random variant with do while
		        let numberRandom;
		        do {
			        numberRandom = this.getRandomInt(0, this.maxSize-1);
                    //alert("numberRandom " + numberRandom);
		        } while(
			        this.gameHits[numberRandom] != undefined	//check if random number array elem has not been taken 
		        )
                
                
                //Bot answers, setTimeout for bot answer to appear with light delay
                setTimeout(() => { 
                    
                    //Insert "0" to gameHits[] 
		            //gameHits[numberRandom] = "0";
                    this.gameHits.splice(numberRandom, 1, "0"); //2 Mega Fixes: 1.to ensure reactivity should use this approach to change array, not this.gameHits[item] = "x"  2. Use splice this way => this.gameHits.splice(item, 1, "x"); //(what array el index to start with, delete 1, new value)
                    
                    this.userCanPlay = true; //enable user's turn to play
                    
                    if(this.checkGame() == true){
			           return false; //to prevent computedAnswer fire if the winner is present
		            }
                                    
                }, delayTime);                
                
            }, */
            
            
            
            
            
            
            
	        //generate random number for bot player
	        getRandomInt(min, max) {
                min = Math.ceil(min);
                max = Math.floor(max);
                return Math.floor(Math.random() * (max - min + 1)) + min;
            },
            
            
            
	    /*
        |--------------------------------------------------------------------------
        | Subfunction, Used in computedAnswer(
        |--------------------------------------------------------------------------
        |
        |
        */
	    AI_engage_subfunction(arrayIndex, cellValue){
		
		    let delayTime = 100; //delay time 
		
            //write down the bot answer '0'
		    //this.gameHits[arrayIndex] = cellValue; //gameHits[2] = "0";	adds to specified array index (array gameHits) new value
	        
			
            
			
			
			 
            //below next line was reassigned to Vuex (+2 lines below)
            //this.gameHits.splice(arrayIndex, 1, cellValue); //2 Mega Fixes: 1.to ensure reactivity should use this approach to change array, not this.gameHits[item] = "x"  2. Use splice this way => this.gameHits.splice(item, 1, "x"); //(what array el index to start with, delete 1, new value)

            //trigger Vuex mutation to update Vuex array gameHits[]
            this.$store.dispatch('updateVuexGameHits0', arrayIndex); //working example how to change Vuex store from child component  
			

			  
			//below line was reassigned to Vuex (+2 lines below)
            //this.userCanPlay = true; //enable user's turn to play
	
			//trigger Vuex mutation to update Vuex boolean userCanPlay
            this.$store.dispatch('updateUserCanPlay', true); //working example how to change Vuex store from child component  




			
	        //flash message
	        //$(".my-hidden"). show();
	        //$(".my-hidden"). fadeOut(3400);	
		
		    //Vue_Sweet alert 2 Toast -----
            let Toast = this.$swal.mixin({
                toast: true,
                position: 'top-end',
                showConfirmButton: false,
                timer: 3000,
                timerProgressBar: true,
                didOpen: (toast) => {
                    toast.addEventListener('mouseenter', this.$swal.stopTimer)   //anemdments for Vue SweetAlerts
                    toast.addEventListener('mouseleave', this.$swal.resumeTimer) //anemdments for Vue SweetAlerts
                }
            })

            //Fire the toast
            Toast.fire({
                icon: 'success',
                title: 'AI was engaged!!!'
            }); 
	        //End Vue_Sweet alert 2 Toast ----
            
            
		
			//below next line was reassigned to Vuex (+2 lines below)
            //this.counterTime = "Attention, AI was engaged!!!!"; //

		    //trigger Vuex mutation to set Vuex var counterTime
            this.$store.dispatch('setVuexCounterTime', "Attention, AI was engaged!!!!");
			
			
			setTimeout(() => {
				
			    //below next line was reassigned to Vuex (+2 lines below)
                //this.counterTime = ""; //force the text to disappear

		        //trigger Vuex mutation to set Vuex var counterTime
                this.$store.dispatch('setVuexCounterTime', "");
		    }, 600);
            
            
	        //computed answer with delay
	        /* setTimeout(() => {
			    drawGameField(false); //renew with no animation
		    }, delayTime); */
            
		    this.checkGame();
	        //return true;
	    }
	
	

    },
               
               
               
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

table {
    width: 100%;
    border:0;
    border-collapse:collapse;
}

td {
    /*padding: 15px;*/
	height: 4em; width: 2em;
    text-align: center;
    border:1px gray solid;
    border-collapse:collapse;
	transition: background-color 2s ease-out 100ms;
}

.tableX td:hover{background-color: yellow;}

.redCell {background-color: red;} /* for winning line */

.timer{height:1.5em; color:red; font-size: 1.4em;}
.game-div{margin-bottom: 10em;}

</style>

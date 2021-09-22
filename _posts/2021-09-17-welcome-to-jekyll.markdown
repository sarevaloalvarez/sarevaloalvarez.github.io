---
layout: post
title:  "Welcome to Steve's site using Jekyll!"
date:   2021-09-17 18:01:43 +0000
categories: jekyll update
---

<html>
    <head>
       <title>Game Of Pig</title>
       <style>
           canvas{
            border: 2px dashed black;
           }
       </style>
       
         
    </head> 
    <body>
        <script>
            class Player{
                constructor(name,points=0){
                    this.name=name;
                    this.points=points;
                    this.rpoints=0;
                }

                add(points){
                 this.points+=points;
                }
                subtract(){
                    this.points-=this.rpoints;
                    this.rpoints=0;
                }
                turnPoints(rpoints){
                    this.rpoints+=rpoints;
                }

                zero(){
                    this.points=0;
                }
            }
            var rollcnt=0;
            var turns=1;
            var highestScore=0;
            var sumScore=0;
            var mostRolls=0;
            var sumRolls=0;
            var player1= new Player('user ');
            var player2= new Player('computer');
            var players=[];
            players.push(player1);
            players.push(player2);
        </script>
        <h1>The Game of Pig</h1>
        <h2>Game Rules</h2>
        <h3>The object: to be the first to score 100 points or more.</h3>
        <h3>How to play: Players take turns rolling two dice and following these rules:</h3>
        <p>On a turn, a player may roll the dice as many times as he or she wants, keeping a running total of the sums that come up. When the player stops rolling, he or she records the total and adds it to the scores from previous rounds.
            But, if a 1 comes up on one of the dice before the player decides to stop rolling, the player scores 0 for that round and it's the next player's turn.
            Even worse, if a 1 comes up on both dice, not only does the turn end, but the player's entire accumulated total returns to 0.</p>   
        <p id="showTurn"></p>
        <p id="endMessage"></p>
        <input type="button" value='Roll Dice' onclick='playTurn();sumRolls++'>
        <input type="button" value="End Turn" onclick='compTurn()'>
        <canvas id='myCanvas' width='450px' height='450px'></canvas>
        <script>
            function playTurn(){ 
                    rollcnt++; 
                    players[1].rpoints=0;
                    var dice=roll();//dice has 3 indices first 2 for roll and 3rd for the sum
                    if (dice[2]==2){
                        players[0].zero();
                        rollcnt=0;
                        setTimeout(compTurn,1000);
                    }
                        else if(dice[0]==1 || dice[1]==1){
                            players[0].subtract();
                            rollcnt=0;
                            setTimeout(compTurn,1000);
                        }   
                            else {
                            players[0].add(dice[2]);
                            sumScore+=players[0].rpoints;
                            players[0].turnPoints(dice[2]);
                            }
                    if(players[0].rpoints>highestScore){
                        highestScore=players[0].rpoints;
                    }
                    
                    if(rollcnt>mostRolls){
                        mostRolls=rollcnt;
                    }
                    draw(dice);
                    importantText(0);
                    
            }
            function compTurn(){
                turns++;
                players[0].rpoints=0;
                document.getElementById("showTurn").innerText=players[1].name+"'s turn";
                var randRolls=Math.floor(Math.random()*10);
                for(var compRolls=0;compRolls<randRolls;compRolls++){
                    var dice=roll();//dice has 3 indices first 2 for roll and 3rd for the sum
                    setTimeout(draw,1000,dice);
                    if (dice[2]==2){
                            players[1].zero();
                            sumRolls+=compRolls;
                            compRolls=100;
                            importantText(0);
                    }
                            else if(dice[0]==1 || dice[1]==1){
                                players[1].subtract();
                                sumRolls+=compRolls;
                                compRolls=100;
                                importantText(0);
                            }   
                                else {
                                    players[1].add(dice[2]);
                                    sumScore+=players[1].rpoints;
                                    players[1].turnPoints(dice[2]);
                                }
                    if(compRolls>mostRolls){
                        mostRolls=comRolls;
                    }
                }
                if(players[1].rpoints>highestScore){
                    highestScore=players[1].rpoints;
                }
                if (compRolls<100){
                    sumRolls+=compRolls;
                }
                turns++;
                importantText(1);
                
            }
            function importantText(p){
                if(players[p].points>=100){
                        document.getElementById("showTurn").innerText=players[p].name+" has won! ";
                        document.getElementById('endMessage').innerText=highestScore+" was the highest round score. "+(sumScore/turns)+" was the average score. "+mostRolls+" was the most rolls in a turn. "+(sumRolls/turns)+" was the average rolls in a turn.";
                    }
                    else{
                        document.getElementById("showTurn").innerText=players[p].name+"'s turn";
                    }
            }
           function draw(dice){
                var canvas= document.getElementById('myCanvas');
                var ctx=canvas.getContext('2d');
                ctx.beginPath();
                ctx.clearRect(0,0,500,500);
                ctx.rect(35,35,200,200);
                ctx.rect(135,245,200,200);
                ctx.stroke();
                ctx.translate(135,135);
                drawFace(ctx,dice[0]);
                ctx.translate(100,210);
                drawFace(ctx,dice[1]);
                ctx.fillText(players[0].name+": "+players[0].points,65,-305);
                ctx.fillText(players[1].name+": "+players[1].points,65,-325);
                ctx.translate(-235,-345);
                ctx.closePath();
           }
           function drawFace(ctx,die){
                ctx.beginPath();
                switch(die){
                    case 5:
                        ctx.arc(-60,60,20,0,2*Math.PI);
                        ctx.moveTo(60,-60);
                        ctx.arc(60,-60,20,0,2*Math.PI);
                        ctx.moveTo(60,60);
                    case 3:
                        ctx.arc(60,60,20,0,2*Math.PI);
                        ctx.moveTo(-60,-60);
                        ctx.arc(-60,-60,20,0,2*Math.PI);
                        ctx.moveTo(0,0);
                    
                    case 1:
                        ctx.arc(0,0,20,0,2*Math.PI);
                        ctx.fill();
                        ctx.stroke();
                        break;
                    case 6:
                        ctx.arc(-60,0,20,0,2*Math.PI);
                        ctx.moveTo(60,0);
                        ctx.arc(60,0,20,0,2*Math.PI);
                        ctx.moveTo(-60,60);
                    case 4:
                        ctx.arc(-60,60,20,0,2*Math.PI);
                        ctx.moveTo(60,-60);
                        ctx.arc(60,-60,20,0,2*Math.PI);
                        ctx.moveTo(60,60); 
                    case 2:
                        ctx.arc(60,60,20,0,2*Math.PI);
                        ctx.moveTo(-60,-60);
                        ctx.arc(-60,-60,20,0,2*Math.PI);
                        ctx.fill();
                        ctx.stroke();
                    }
                    
           }
            function roll(){
                var dice=[];
                for(var i=0;i<2;i++){
                    var rand=Math.floor(Math.random()*6)+1;
                    dice.push(rand);
                }
                dice.push(dice[0]+dice[1]);
                return dice;
            }
            
        </script>
    </body>
</html>

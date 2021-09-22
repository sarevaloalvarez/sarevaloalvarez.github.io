---
layout: post
title:  "Roll some dice while you're here!"
date:   2021-09-17 18:01:43 +0000
categories: jekyll update
---

<html>
    <head>
       <title>Roll the Dice </title>
       <style>
           canvas{
            border: 2px dashed black;
           }
       </style>
       
         
    </head> 
    <body>
    
        <h1>Dice Roll</h1>
       
        <input type="button" value='Roll Dice' onclick='playTurn();'>
     
        <canvas id='myCanvas' width='450px' height='450px'></canvas>
        <script>
            function playTurn(){ 
                    var dice=roll();
                    draw(dice);
       
                    
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

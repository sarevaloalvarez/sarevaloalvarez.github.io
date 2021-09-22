---
layout: post
title:  "Welcome to Steve's site using Jekyll!"
date:   2021-09-17 18:01:43 +0000
categories: jekyll update
---
<!DOCTYPE html>
<html>
    <head>
        <title>Warehouse Scene</title>
        <style>
            canvas{
                border: 1px solid black;
            }
        </style>
    </head>
    <body onload='initialize()'>
        <canvas id='Cutscene' width='1024px' height='500 px'></canvas> 
    </body>
    <script>
        var canvas,ctx;
        var bgrd=new Image();
        bgrd.src='AcmeWarehouse.png';
        var bgrdX;
        var cat= new Image();
        cat.src='cat_ar_base.png';
        var robot=new Image();
        robot.src='robosheet.png';
        var monster=new Image();
        monster.src='monster.png';
        var catX,catY,catFrameX,catFrameY,catFrameW,catFrameH;
        var robotX,robotY,robotFrameX,robotFrameY,robotFrameW,robotFrameH;
        var monsterX,monsterY,monsterFrameX,monsterFrameY,monsterFrameW,monsterFrameH;
        var robotFrameCount;
        var catFrameCount;
        var monsterFrameCount;
        var timing;
        function initialize(){
            canvas=document.getElementById('Cutscene');
            ctx=canvas.getContext('2d');
            bgrdX=10;
            catX=20;catY=372;catFrameX=0;catFrameY=3;catFrameW=64;catFrameH=64;
            catFrameCount=8;
            robotX=1924;robotY=372;robotFrameX=0;robotFrameY=0;robotFrameW=55; robotFrameH=88;
            robotFrameCount=3;
            monsterX=-100;monsterY=-100;monsterFrameX=0; monsterFrameY=1;monsterFrameW=64;monsterFrameH=64;
            monsterFrameCount=4;
            timing=0;

            update();
           
        }
        function update(){
            timing++;
            console.log(timing);
            //0-5 sec
            if(timing<300){
                if(timing%6==0){
                    catFrameX++;
                    bgrdX+=4;
                    robotX-=4;
                }
               
            }
            //5-9 sec
            if(timing>300 && timing<540){ 
                catFrameY=1;
                if(timing%6==0){
                   
                    catFrameX++;
                    
                }
                
            }
            //9-15 sec
            if(timing>540 && timing<900){
                catFrameY=3;
                if(timing%6==0){
                    
                    catFrameX++;
                    bgrdX+=14;
                    robotX-=14;
                    catX+=5;
                }
            }
            //15-17 sec
            if(timing>900 && timing<1020){
                if(timing%6==0){
                    catX+=7;
                    catFrameX++;
                }
            }
            //17-21 sec
            if(timing > 1020 && timing<1260){
                catFrameY=1;
                if(timing%6==0){

                    catFrameX++;
                }
            }
            //21-29 sec
            if (timing>1260 && timing<1740){
                catFrameY=3;
                if(timing%6==0){

                    catFrameX++;
                    catX+=5;
                }
            }
            //29-30 sec
            if(timing>1740 && timing<1800){
                catFrameY=1;
                if(timing%6==0){
                    catFrameX++;
                }
            }
            if(timing==1800){
                catFrameCount=4;
                catFrameX=3;
            }
            //30-30.4 sec
            if (timing>1800 && timing<1824){
                
                catFrameY=0;
                if(timing%6==0){
                    catFrameX--;
                }
            }
            //30.4-33.6 sec
            if (timing >1824 && timing<2016){
                //text
            }
            //33.6-34 sec
            if(timing>2016 && timing<2040){
                if(timing%6==0){
                    catFrameX++;
                }
            }
            if(timing==2040){
                catFrameCount=10;
                catFrameY=5;
                catFrameX=0;
            }
            //34-35 sec
            if(timing>2040 && timing<2100){

                
                if(timing%6==0){
                    catFrameX++;
                    catX-=6;
                }
                switch (catFrameX){
                    case 0:
                    case 1:
                    case 2:
                    case 3:
                    catY-=2;break;
                    case 4:
                    catY-=1;break;
                    case 5: 
                    catY+=1;break;
                    case 6:
                    case 7:
                    case 8:
                    case 9:
                    catY+=2;
                }
            }
            if (timing==2100){
                catFrameCount=8;
                catFrameY=1;
                robotFrameY=1;
                catFrameX=0;
            }
            //35-45 sec
            if (timing>2100 && timing<2700){
                if(timing%8==0){
                    catFrameX++;
                    robotFrameX++;
                }
            }
            if(timing==2700){
                catFrameY=3;
                robotFrameY=2;
                monsterX=0;
                monsterY=372;
            }
            //45-50 sec
            
            if(timing>2700 && timing<3000){
                if(timing%6==0){
                    catFrameX++
                    catX+=8;
                    robotFrameX++;
                    robotX-=8;
                    monsterFrameX++;
                    monsterX+=5;
                    
                }
            }
            if(timing==3000){
                robotFrameY=3;
                robotFrameCount=6;
            }
            //50-51.8 sec
            if(timing>3000 && timing<3108){
                if(timing%6==0){
                    robotFrameX++;
                    monsterFrameX++;
                    monsterX+=5;
                }
            }
            if(timing==3108){
                robotFrameY=1;
                robotFrameCount=3;
                monsterFrameY=3;
                monsterFrameCount=7;
                monsterFrameX=0;
            }
            //51.8-52.5 sec
            if(timing>3108 && timing<3150){
                if(timing%6==0){
                    robotFrameX++;
                    monsterFrameX++
                }
            }
            if(timing==3150){
                monsterX=-100;
                monsterY=-100;
            }
            //52.5-60 sec
            if(timing>3150 && timing<3600){
                if(timing%6==0)
                    robotFrameX++;
            }
            if(catFrameX==catFrameCount)
                catFrameX=0;
            if (robotFrameX==robotFrameCount)
                robotFrameX=0;
            if (monsterFrameX==monsterFrameCount)
                monsterFrameX=0;
            draw();
            requestAnimationFrame(update);
        }
        function draw(){
            ctx.clearRect(0,0,canvas.width,canvas.height);
             ctx.drawImage(bgrd,bgrdX,10,2048,500,0,0,2048,500);
             ctx.drawImage(robot,robotFrameX*robotFrameW,robotFrameY*robotFrameH,robotFrameW,robotFrameH,robotX,robotY,robotFrameW+12,robotFrameH+20);
             ctx.drawImage(cat,catFrameX*catFrameW,catFrameY*catFrameH,catFrameW,catFrameH,catX,catY,128,128);
             if(timing>300 && timing<540){
                 ctx.rect(0,0,canvas.width,100);
                 ctx.fillStyle='black';
                 ctx.fill();
                 ctx.drawImage(cat,0,0,catFrameW,catFrameH,-20,-20,128,128);
                 ctx.fillStyle='white';
                 ctx.font = "30px Comic Sans MS";
                 ctx.fillText("Woah, What's That?",150,50);
             }
             if(timing>900 && timing<1020){
                ctx.rect(0,0,canvas.width,100);
                ctx.fillStyle='black';
                ctx.fill();
                ctx.drawImage(cat,0,0,catFrameW,catFrameH,-20,-20,128,128);
                ctx.fillStyle='white';
                ctx.font = "30px Comic Sans MS";
                ctx.fillText("It looks like a robot.",150,50);
             }
             if(timing >= 1020 && timing<1260){
                ctx.rect(0,0,canvas.width,100);
                ctx.fillStyle='black';
                ctx.fill();
                ctx.drawImage(cat,0,0,catFrameW,catFrameH,-20,-20,128,128);
                ctx.fillStyle='white';
                ctx.font = "30px Comic Sans MS";
                ctx.fillText("I think I can get it to work.",150,50);
             }
             if(timing >1824 && timing<2016){
                ctx.rect(0,0,canvas.width,100);
                ctx.fillStyle='black';
                ctx.fill();
                ctx.drawImage(robot,0,0,robotFrameW,robotFrameH,0,0,96,96);
                ctx.fillStyle='white';
                ctx.font = "30px Comic Sans MS";
                ctx.fillText("*CLINK*  *CLUNK*  *CLINK*",150,50);
             }
             //2100-2700
             if (timing>2100 && timing<=2220){
                ctx.rect(0,0,canvas.width,100);
                ctx.fillStyle='black';
                ctx.fill();
                ctx.drawImage(robot,0,0,robotFrameW,robotFrameH,0,0,96,96);
                ctx.fillStyle='white';
                ctx.font = "30px Comic Sans MS";
                ctx.fillText("POWER ON",150,50);   
             }
             if (timing>2220 && timing<=2340){
                ctx.rect(0,0,canvas.width,100);
                ctx.fillStyle='black';
                ctx.fill();
                ctx.drawImage(cat,0,0,catFrameW,catFrameH,-20,-20,128,128);
                ctx.fillStyle='white';
                ctx.font = "30px Comic Sans MS";
                ctx.fillText("How long have you been here?",150,50);
             }
             if (timing>2340 && timing<=2460){
                ctx.rect(0,0,canvas.width,100);
                ctx.fillStyle='black';
                ctx.fill();
                ctx.drawImage(robot,0,0,robotFrameW,robotFrameH,0,0,96,96);
                ctx.fillStyle='white';
                ctx.font = "30px Comic Sans MS";
                ctx.fillText("I've been left deactiviated for around 15 years",150,50);
             }
             if (timing>2460 && timing<=2580){
                ctx.rect(0,0,canvas.width,100);
                ctx.fillStyle='black';
                ctx.fill();
                ctx.drawImage(robot,0,0,robotFrameW,robotFrameH,0,0,96,96);
                ctx.fillStyle='white';
                ctx.font = "30px Comic Sans MS";
                ctx.fillText("My creator must have left me here to rust",150,50);
             }
             if (timing>2580 && timing<=2700){
                ctx.rect(0,0,canvas.width,100);
                ctx.fillStyle='black';
                ctx.fill();
                ctx.drawImage(cat,0,0,catFrameW,catFrameH,-20,-20,128,128);
                ctx.fillStyle='white';
                ctx.font = "30px Comic Sans MS";
                ctx.fillText("15 years is about how long this mess has been going on.",150,50);
             }
             if (timing>2700 && timing<=3000){
                ctx.rect(0,0,canvas.width,100);
                ctx.fillStyle='black';
                ctx.fill();
                ctx.drawImage(cat,0,0,catFrameW,catFrameH,-20,-20,128,128);
                ctx.fillStyle='white';
                ctx.font = "30px Comic Sans MS";
                ctx.fillText("OH NO! THERES TOO MANY!! RUN!!!",150,50);
             }
             //3150-3600
             if (timing>=3150 && timing<=3300){
                ctx.rect(0,0,canvas.width,100);
                ctx.fillStyle='black';
                ctx.fill();
                ctx.drawImage(robot,0,0,robotFrameW,robotFrameH,0,0,96,96);
                ctx.fillStyle='white';
                ctx.font = "30px Comic Sans MS";
                ctx.fillText("I'm well aware of how long this chaos has been going on",150,50);
             }
             if (timing>3300 && timing<=3600){
                ctx.rect(0,0,canvas.width,100);
                ctx.fillStyle='black';
                ctx.fill();
                ctx.drawImage(robot,0,0,robotFrameW,robotFrameH,0,0,96,96);
                ctx.fillStyle='white';
                ctx.font = "30px Comic Sans MS";
                ctx.fillText("My creator started it and I need your help to stop it",150,50);
             }
             for(var i=0;i<3;i++){
                ctx.drawImage(monster,monsterFrameX*monsterFrameW,monsterFrameY*monsterFrameH,monsterFrameW,monsterFrameH,monsterX-i*64,monsterY, 96,96);
             }
        }
    </script>
</html>

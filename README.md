# Ping-Pong-Game-
Python is used to build this program . 
Turtle module is used in this code . 
This game is a multiplayer game . 
The two players A and B have to use their keyboard buttons and slide their paddle and prevent the leaving of ball.  

import turtle  

wn = turtle.Screen() 
wn.title("Pong by @dhruv_trehan_17") 
wn.bgcolor("black")                  
wn.setup(width=800 , height=600)     
wn.tracer(0)                        
#Score
score_a = 0                          
score_b = 0                         

Paddle A : Command to make paddle A 

1.turtle is a module name and Turtle is a class name . Small t denotes the name of the class and capital T denotes the name of the class. 
2.Each command is used to decide the shape and structure of Paddle A.
3.paddle_a is a object through which various commands are running in turtle.

paddle_a = turtle.Turtle()          
paddle_a.speed(0)                    
paddle_a.shape("square")             
paddle_a.color("white")             
paddle_a.shapesize(stretch_wid= 5 , stretch_len = 0.5) 
paddle_a.penup()                     
paddle_a.goto(-350,0)                


Paddle B

1.turtle is a module name and Turtle is a class name . Small t denotes the name of the class and capital T denotes the name of the class. 
2.Each command is used to decide the shape and structure of Paddle B.
3.paddle_b is a object through which various commands are running in turtle.


paddle_b = turtle.Turtle()         
paddle_b.speed(0)                   
paddle_b.shape("square")            
paddle_b.color("white")          
paddle_b.shapesize(stretch_wid=5 , stretch_len = 0.5)   
paddle_b.penup()                                        
paddle_b.goto(350,0)                                   


Code telling all about ball which is used in the slide of program 

ball = turtle.Turtle()
ball.speed(-1)
ball.shape("circle")
ball.color("white")
ball.penup()
ball.goto(0,0)

ball.dx = 2
ball.dy = -2

Pen which is used to write headline at the top of the turtle screen

pen = turtle.Turtle()
pen.speed(0)
pen.color("white")
pen.penup()
pen.hideturtle()
pen.goto(0,260)
pen.write("Player A: 0 Player B: 0 ".format(score_a , score_b), align = "center" ,  font=("Arial" ,  24 , "normal"))

Function which is used to slide paddle A and paddle B


def paddle_a_up():
    
    y = paddle_a.ycor()
    y +=20
    paddle_a.sety(y)

def paddle_a_down():

    y = paddle_a.ycor()
    y -=20
    paddle_a.sety(y)

def paddle_b_up():
    
    y = paddle_b.ycor()
    y +=20
    paddle_b.sety(y)

def paddle_b_down():
    
    y = paddle_b.ycor()
    y -=20
    paddle_b.sety(y)

Keyboard binding is done through these command . Various command are function on the basis of click done by the user.

1.wn.listen() is a command which is used to draw relation between keyboard and various keys. 

wn.listen()                          
wn.onkeypress(paddle_a_up,"w")       
wn.onkeypress(paddle_a_down,"s")   
wn.onkeypress(paddle_b_up,"Up")      
wn.onkeypress(paddle_b_down,"Down")  

This is a main game loop

while True:
    wn.update()
    
    #move the ball
    
    ball.setx(ball.xcor() + ball.dx)
    ball.sety(ball.ycor() + ball.dy)

    #Border checking

    if ball.ycor() > 290:
        ball.sety(290)
        ball.dy *= -1

    if ball.ycor() < -290:
        ball.sety(-290)
        ball.dy *= -1

    if ball.xcor() > 390:
        ball.goto(0,0)
        ball.dx *= -1
        score_a +=1
        pen.clear()
        pen.write("Player A: {} Player B: {} ".format(score_a , score_b), align = "center" ,  font=("Arial" ,  24 , "normal"))


    if ball.xcor() < -390: //
        ball.goto(0,0)
        ball.dx *= -1
        score_b +=1
        pen.clear()
        pen.write("Player A: {} Player B: {} ".format(score_a, score_b), align="center", font=("Arial", 24, "normal"))


 Paddle and ball collision
 
 In this part of the code we have focused on collision between the ball and paddle and returning back of the ball to the centre after colllision

    if (ball.xcor() > 340 and ball.xcor() < 350 )and (ball.ycor() < paddle_b.ycor() + 40 and ball.ycor() > paddle_b.ycor() -40):
        ball.setx(340)
        ball.dx *=-1

    if (ball.xcor() < -340 and ball.xcor() >  -350 ) and (ball.ycor() < paddle_a.ycor () + 40 and ball.ycor() > paddle_a.ycor() -40):
        ball.setx(-340)
        ball.dx *=-1

Printing the game results
    
    if (flag == 0):
         pen.goto(0,0)
         pen.write("Game over" , align="center" , font=("Arial", 72 ,"normal"))
         if (score_a > score_b):
             pen.goto(0,-110)
             pen.write("Player A Wins" , align ="center" , font = ("Arial" , 24 , "normal"))
         else:
             pen.goto(0, -110)
             pen.write("Player B Wins", align="center", font=("Arial", 24, "normal"))
     wn.exitonclick() 
   

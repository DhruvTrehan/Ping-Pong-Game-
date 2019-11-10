# Ping-Pong-Game-
Python is used to build this program . 
Turtle module is used in this code . 
This game is a multiplayer game . 
The two players A and B have to use their keyboard buttons and slide their paddle and prevent the leaving of ball.  

import turtle #Command to import turtle in Python 

wn = turtle.Screen()                 #Setting wn as a object to be used in calling turtle commands 
wn.title("Pong by @dhruv_trehan_17") #Setting the tittle on the turtle screen
wn.bgcolor("black")                  #Setting background color in Turtle Screen
wn.setup(width=800 , height=600)     #Setting the width of the screen
wn.tracer(0)                         #Help in the tracing the execution of the program

#Score
score_a = 0                          # Variable assigned to check the score of A 
score_b = 0                          # Variable assigned to check the score of B

#paddle A

paddle_a = turtle.Turtle()           #turtle is module name and Turtle is a class name . Small 't' denotes a module name and capital 'T' denotes a class name.
paddle_a.speed(0)                    #Setting the speed of a 
paddle_a.shape("square")             # The shape of paddle a  is sqaure
paddle_a.color("white")              #The color of paddle a is white 
paddle_a.shapesize(stretch_wid= 5 , stretch_len = 0.5)   #The size of paddle A 
paddle_a.penup()                    #penup command is used to move the turttle without any line on screen 
paddle_a.goto(-350,0)               #Move the paddle from centre to (-350 , 0) position 


#paddle B

paddle_b = turtle.Turtle()          #turtle is module name and Turtle is a class name . Small 't' denotes a module name and capital 'T' denotes a class name.
paddle_b.speed(0)                   #Setting the speed of paddle b
paddle_b.shape("square")            #Shape of paddle b
paddle_b.color("white")             #color of paddle b 
paddle_b.shapesize(stretch_wid=5 , stretch_len = 0.5)  #size of paddle b 
paddle_b.penup()                                       #moving the turtle after lifting up the turtle 
paddle_b.goto(350,0)                                   #moving the paddle from centre to (350 , 0 ) position


#Code telling all about ball which is used in the slide of program 

ball = turtle.Turtle()
ball.speed(-1)
ball.shape("circle")
ball.color("white")
ball.penup()
ball.goto(0,0)

ball.dx = 2
ball.dy = -2

#pen which is used to write headline at the top of the turtle screen

pen = turtle.Turtle()
pen.speed(0)
pen.color("white")
pen.penup()
pen.hideturtle()
pen.goto(0,260)
pen.write("Player A: 0 Player B: 0 ".format(score_a , score_b), align = "center" ,  font=("Arial" ,  24 , "normal"))

#Function which is used to slide paddle A and paddle B


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

#Keyboard binding

wn.listen()                          #command to automate the keyboard commands
wn.onkeypress(paddle_a_up,"w")       #w is command to let paddle a be up 
wn.onkeypress(paddle_a_down,"s")     #s is used to slide paddle a down
wn.onkeypress(paddle_b_up,"Up")      #Up arrow key is used to slide paddle  b up
wn.onkeypress(paddle_b_down,"Down")  #down arrow key is used to slide paddle b down 


#This is a main game loop

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


    # paddle and ball collision
    #In this part of the code we have focused on collision between the ball and paddle and returning back of the ball to the centre after colllision

    if (ball.xcor() > 340 and ball.xcor() < 350 )and (ball.ycor() < paddle_b.ycor() + 40 and ball.ycor() > paddle_b.ycor() -40):
        ball.setx(340)
        ball.dx *=-1

    if (ball.xcor() < -340 and ball.xcor() >  -350 ) and (ball.ycor() < paddle_a.ycor () + 40 and ball.ycor() > paddle_a.ycor() -40):
        ball.setx(-340)
        ball.dx *=-1

   #Printing the game results
    
    if (flag == 0):
         pen.goto(0,0)
         pen.write("Game over" , align="center" , font=("Arial", 72 ,"normal"))
         if (score_a > score_b):
             pen.goto(0,-110)
             pen.write("Player A Wins" , align ="center" , font = ("Arial" , 24 , "normal"))
         else:
             pen.goto(0, -110)
             pen.write("Player B Wins", align="center", font=("Arial", 24, "normal"))
     wn.exitonclick() #For screen to exit you need to click 
   

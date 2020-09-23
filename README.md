<div align="center">

## A Basic Game


</div>

### Description

This is a tutorial for anyone who wants to start learning how to program games in Java. I have written it so it can be easy for anyone but it is rather long. If you would like to see this tutorial in its two sections rather than one page please check out my website <a href="http://www.jcroucher.com">www.jcroucher.com</a>
 
### More Info
 


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[John Croucher](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/john-croucher.md)
**Level**          |Beginner
**User Rating**    |4.7 (202 globes from 43 users)
**Compatibility**  |Java \(JDK 1\.2\)
**Category**       |[Games](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/games__2-72.md)
**World**          |[Java](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/java.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/john-croucher-a-basic-game__2-3270/archive/master.zip)





### Source Code

<CENTER></FONT>
<H1><font color="#0000CD">Java Game Tutorial - Part 1 </Font></H1>
</Center>
<font color="#000000" face="Comic Sans MS" size="2">
<BR>In this and following tutorials you will learn about Applets, Threads, Graphics and a few other things. By the end of this tutorial you should have the skills to make basic games in Java. For this tutorial you will be making a simple ‘space invaders’ type game.
<BR>
<BR>I assume that you have basic knowledge of Java as I wont be going into the basic details of how some things work.
<BR>
<BR>First we will be starting by creating an applet and drawing a circle to the applet area.
<BR>
<BR>1.	Create a file called ‘Game.java’.
<BR>2.	Open the file.
<BR>
<BR>The next step is to import the necessary packages. For now we will only be requiring 2 packages:
</FONT><font color="#0000CD" face="Comic Sans MS" size="2">
<BR>     import java.applet.*;
<BR>     import java.awt.*;
<BR>
</Font><font color="#000000" face="Comic Sans MS" size="2">
<BR>Now that the importing has been taken care of we will need to set up the Java applet by the following:
<BR>
</FONT><font color="#0000CD" face="Comic Sans MS" size="2">
<BR>     public class Game extends Applet implements Runnable
<BR>     {
<BR>     }
<BR>
</Font><font color="#000000" face="Comic Sans MS" size="2">
<BR>This basically gives access to the Applet class and the ‘Runnable’ makes it so we can implement threads.
<BR>
<BR>The variables come next as we wish to make these ones global:
<BR>
</FONT><font color="#0000CD" face="Comic Sans MS" size="2">
<BR>     Thread gameThread;
<BR>     int width=400, height=400, MAX=1;
<BR>     int currentX[] = new int[MAX];
<BR>     int currentY[] = new int[MAX];
<BR>
</Font><font color="#000000" face="Comic Sans MS" size="2">
<BR>I have decided to use arrays for the X and Y cords now because they will be used at a later stage. It makes it easier to set it up now rather than changing it later.
<BR>Next comes the methods. I have included methods that are currently not used at this stage but they are used later.
<BR>
<BR>Start() is used for starting a new thread for the class.
<BR>
</FONT><font color="#0000CD" face="Comic Sans MS" size="2">
<BR>     public void start()
<BR>     {
<BR>          Thread gameThread = new Thread(this);
<BR>          gameThread.start();
<BR>     }
<BR>
<BR>
</Font><font color="#000000" face="Comic Sans MS" size="2">
<BR>init() is used for setting the initial values
<BR>
</FONT><font color="#0000CD" face="Comic Sans MS" size="2">
<BR>     public void init()
<BR>     {
<BR>          currentX[0]=0;
<BR>          currentY[0]=0;
<BR>     }
<BR>
</Font><font color="#000000" face="Comic Sans MS" size="2">
<BR>run() is the main method we will use later. It is initialised after a new thread is started.
<BR>
</FONT><font color="#0000CD" face="Comic Sans MS" size="2">
<BR>     public void run()
<BR>     {
<BR>     }
<BR>
<BR>
</Font><font color="#000000" face="Comic Sans MS" size="2">
<BR>paint() calls update().
<BR>
</FONT><font color="#0000CD" face="Comic Sans MS" size="2">
<BR>     public void paint(Graphics g)
<BR>     {
<BR>          update(g);
<BR>     }
<BR>
</Font><font color="#000000" face="Comic Sans MS" size="2">
<BR>update () is where all the actual drawing is done.
<BR>
</FONT><font color="#0000CD" face="Comic Sans MS" size="2">
<BR>     public void update(Graphics g)
<BR>     {
<BR>          Graphics2D g2 = (Graphics2D)g;
<BR>
<BR>          // Set the background color.
<BR>          g2.setBackground(Color.black);
<BR>
<BR>          // Clear the applet.
<BR>          g2.clearRect(0, 0, width, height);
<BR>
<BR>          // Set the drawing color to green.
<BR>          g2.setColor(Color.green);
<BR>
<BR>          //(X pos, Y pos, Width, Height)
<BR>          g2.fillOval(currentX[0], currentY[0], 20,20);
<BR>     }
<BR>
<BR>
</Font><font color="#000000" face="Comic Sans MS" size="2">
<BR>* Note this is an applet which means you must run it from a HTML file. The HTML code to run this applet is as follows and I will use the same code throughout this series of tutorials.
<BR>
</FONT><font color="#0000CD" face="Comic Sans MS" size="2">
<BR><APPLET
<BR>     CODE      = "Game.class"
<BR>     NAME      = "Game Tutorial"
<BR>     WIDTH    = 400
<BR>     HEIGHT   = 400
<BR>     ALIGN      = middle
<BR>?>
<BR></APPLET>
<BR>
</Font><font color="#000000" face="Comic Sans MS" size="2">
<BR>As you will see if you compile and run this applet it will draw a green circle on a black background. This is pretty simple and pretty boring but it sets the basis up for doing things later. At this stage you do not even need the Thread but I thought I would put it in now to make it more easy later.
<BR>
<BR>Now I will go into something more interesting but still rather useless. We will now make the circle bounce around the screen.
<BR>
<BR>In this version I have added more global variables:
<BR>
</FONT><font color="#0000CD" face="Comic Sans MS" size="2">
<BR>     int speed=10; // Speed at which we will move the objects
<BR>
<BR>     // Which direction to move the object
<BR>     int directionX[] = new int[MAX];
<BR>     int directionY[] = new int[MAX];
<BR>
<BR>
</Font><font color="#000000" face="Comic Sans MS" size="2">
<BR>These variables are used for making sure the applet doesn’t go psycho fast on very fast computers and also to make sure it doesn’t run to slow on slow computers.
<BR>
</FONT><font color="#0000CD" face="Comic Sans MS" size="2">
<BR>     long start=0;
<BR>     long tick_end_time;
<BR>     long tick_duration;
<BR>     long sleep_duration;
<BR>
<BR>     static final int MIN_SLEEP_TIME = 10;
<BR>     static final int MAX_FPS = 20;
<BR>     static final int MAX_MS_PER_FRAME = 1000 / MAX_FPS;
<BR>
<BR>     float fps=0;
<BR>
<BR>
</Font><font color="#000000" face="Comic Sans MS" size="2">
<BR>Only two functions are modified in this version. The first modification is a simple one. All it does is sets the value in directionX[0] to 1 which means that it will travel to the left first, and directionY[0] to 0 which means it will travel to the top first:
<BR>
</FONT><font color="#0000CD" face="Comic Sans MS" size="2">
<BR>     public void init()
<BR>     {
<BR>          currentX[0]=100;
<BR>          currentY[0]=0;
<BR>
<BR>          directionX[0]=1;
<BR>          directionY[0]=0;
<BR>     }
<BR>
<BR>
</Font><font color="#000000" face="Comic Sans MS" size="2">
<BR>This module as I said earlier this is the main function and as you will notice this one has the biggest amount of code in it now, so this may take a bit to explain. First here is the run() code in full.
<BR>
</FONT><font color="#0000CD" face="Comic Sans MS" size="2">
<BR>     public void run()
<BR>     {
<BR>          while(true){
<BR>               start = System.currentTimeMillis();
<BR>
<BR>               for(int i=0; i < MAX; i++){
<BR>                    if(directionX[i]==1)
<BR>                         currentX[i]+=speed;
<BR>
<BR>                    if(directionX[i]==0)
<BR>                         currentX[i]-=speed;
<BR>
<BR>                    if(currentX[i] <= 0)
<BR>                         directionX[i]=1;
<BR>
<BR>                    if(currentX[i]+20 >= width)
<BR>                         directionX[i]=0;
<BR>
<BR>                    if(directionY[i]==1)
<BR>                         currentY[i]+=speed;
<BR>
<BR>                    if(directionY[i]==0)
<BR>                         currentY[i]-=speed;
<BR>
<BR>                    if(currentY[i] <= 0)
<BR>                         directionY[i]=1;
<BR>
<BR>                    if(currentY[i]+20 >= height)
<BR>                         directionY[i]=0;
<BR>               }
<BR>
<BR>               repaint();
<BR>
<BR>               tick_end_time = System.currentTimeMillis();
<BR>               tick_duration = tick_end_time - start;
<BR>               sleep_duration = MAX_MS_PER_FRAME - tick_duration;
<BR>
<BR>               if (sleep_duration < MIN_SLEEP_TIME)
<BR>               {
<BR>                    sleep_duration = MIN_SLEEP_TIME;
<BR>               }
<BR>               fps = 1000 / (sleep_duration + tick_duration);
<BR>
<BR>               try{
<BR>                    Thread.sleep(sleep_duration);
<BR>               } catch(InterruptedException e) {}
<BR>
<BR>          }
<BR>     }
<BR>
</Font><font color="#000000" face="Comic Sans MS" size="2">
<BR>Now onto explaining the function. First this function will continually loop. This is what gives our game moving objects.
<BR>The next line is:
</FONT><font color="#0000CD" face="Comic Sans MS" size="2">
<BR>     start = System.currentTimeMillis();
<BR>
</Font><font color="#000000" face="Comic Sans MS" size="2">
<BR>This line is part of our frame rate calculations. It will set the start time to the system time at the start of the frame.
<BR>
<BR>The next section is a for loop containing the code for calculating the objects position and where to move it to next. The X and Y cords are similar so I will only explain the X cord:
<BR>
<BR>These first two if statements are used for calculating the new position in relation to its current X value:
<BR>
</FONT><font color="#0000CD" face="Comic Sans MS" size="2">
<BR>     if(directionX[i]==1)
<BR>          currentX[i]+=speed;
<BR>
</Font><font color="#000000" face="Comic Sans MS" size="2">
<BR>This says if the current object is moving right then add ‘speed’ to the current position of the object. Basically if the object is at X:0 and the speed is 10, then the new X position will be 10 (0 + 10).
<BR>
</FONT><font color="#0000CD" face="Comic Sans MS" size="2">
<BR>     if(directionX[i]==0)
<BR>          currentX[i]-=speed;
<BR>
</Font><font color="#000000" face="Comic Sans MS" size="2">
<BR>This section does the opposite to the previous if statement (moves to left).
<BR>
<BR>
</FONT><font color="#0000CD" face="Comic Sans MS" size="2">
<BR>These last two detect if the object has hit the side of the applet and if so change the direction:
<BR>     if(currentX[i] <= 0)
<BR>          directionX[i]=1;
<BR>
</Font><font color="#000000" face="Comic Sans MS" size="2">
<BR>If the current X position is less than or equal to zero then change the direction so it now moves to the right.
<BR>
</FONT><font color="#0000CD" face="Comic Sans MS" size="2">
<BR>     if(currentX[i]+20 >= width)
<BR>          directionX[i]=0;
<BR>
</Font><font color="#000000" face="Comic Sans MS" size="2">
<BR>Again this one does similar but it detects if the object has hit the right side of the applet. This one has a small variation in the checking tho. You will notice it has:
<BR>
</FONT><font color="#0000CD" face="Comic Sans MS" size="2">
<BR>     currentX[i]+20
<BR>
</Font><font color="#000000" face="Comic Sans MS" size="2">
<BR>The current X value of the object is at cord 0 of the object (its left most side). This means that X will only be greater than or equal to the width after all of the right hand size has gone out of the applet. So we must add 20 which is the width of the object. Feel free to remove the +20 or change it to higher and smaller values to observe the effects it has.
<BR>
<BR>That concludes the collision detection section.
<BR>Next you will see:
</FONT><font color="#0000CD" face="Comic Sans MS" size="2">
<BR>     repaint();
<BR>
</Font><font color="#000000" face="Comic Sans MS" size="2">
<BR>Basically all this line does is calls the functions for painting on the screen paint() and update(). I think it does some internal calculations before going to those functions first tho.
<BR>
<BR>You are probably thinking this is all a bit much right now, but don’t worry, only 2 more sections to go.
<BR>
</FONT><font color="#0000CD" face="Comic Sans MS" size="2">
<BR>     tick_end_time = System.currentTimeMillis();
<BR>     tick_duration = tick_end_time - start;
<BR>     sleep_duration = MAX_MS_PER_FRAME - tick_duration;
<BR>
<BR>     if (sleep_duration < MIN_SLEEP_TIME)
<BR>     {
<BR>          sleep_duration = MIN_SLEEP_TIME;
<BR>     }
<BR>     fps = 1000 / (sleep_duration + tick_duration);
<BR>
</Font><font color="#000000" face="Comic Sans MS" size="2">
<BR>This code is pretty simple and self explanatory so I won’t go into details. But basically it works out how long it has taken to draw the current frame. If the system is lagging it will ‘sleep_duration’ reduce ‘sleep_duration’ and if it’s going to fast it will increase ‘sleep_duration’. The sleep time is done in this final section:
<BR>
</FONT><font color="#0000CD" face="Comic Sans MS" size="2">
<BR>     try{
<BR>          Thread.sleep(sleep_duration);
<BR>     } catch(InterruptedException e) {}
<BR>
</Font><font color="#000000" face="Comic Sans MS" size="2">
<BR>This will simply pause the thread for the value in ‘sleep_duration’. This is all done to make sure the game runs at its best on all systems.
<BR>
<BR>If you want you can display the current frame rate by placing this line of code in your paint(Graphics g) function:
</FONT><font color="#0000CD" face="Comic Sans MS" size="2">
<BR>     g.drawString("FPS: "+fps,1,400);
<BR>
</Font><font color="#000000" face="Comic Sans MS" size="2">
<BR>Also be aware that that calculation doesn’t always give the correct frame rate. It is simply to regulate the speed of the app.
<BR>
<BR>
<BR>Well if you compile all that and run it you should get a green circle bouncing around your screen.
<BR>You will also notice that it flickers a lot especially if you increase the frame rate. This is because you can actually see the computer drawing the objects to the screen. In the next tutorial I will explain how to do frame buffering which will make your objects run smooth, and more.
<BR>
<BR>Thanks for reading,
<BR>Feel free to send any comments.
<BR><BR>
<CENTER></FONT>
<H1><font color="#0000CD">Java Game Tutorial - Part 2 </Font></H1>
</Center>
<font color="#000000" face="Comic Sans MS" size="2">
<BR>Welcome back.
<BR>In this tutorial I will show you how to implement buffering into your app. First here are some details on how buffering works.
<BR>The current app you have flickers. This is because you can actually see the computer drawing the images to the screen. If you use buffering the computer draws it to one area and then only once it has finished drawing the objects it displays it on the screen.
<BR>There are different ways of doing buffering, but for now I will stick with the easiest so you can get an idea of how it all works.
<BR>If you have trouble understanding that example this way may help. I like to think of buffering like someone drawing on a piece of paper. If you are watching someone draw on a piece of paper you can see every movement the person makes. But if say the person has 2 pieces of paper it could make things better. The person gives you one to look at. While you are looking at that piece of paper the person goes on and draws on the blank one. Once the person has finished drawing that one, the person will switch pages with you, and start drawing again. I know it’s a lame way of putting it but it’s simple.
<BR>
<BR>Now that all the background is out of the way we will now get to modifying the code from the first tutorial.
<BR>
<BR>First you will need to import:
<BR>
</FONT><font color="#0000CD" face="Comic Sans MS" size="2">
<BR>     java.awt.image.*;
<BR>
<BR>
</Font><font color="#000000" face="Comic Sans MS" size="2">
<BR>We also have two new variables to add:
<BR>
</FONT><font color="#0000CD" face="Comic Sans MS" size="2">
<BR>     BufferedImage bufferdImg;
<BR>     Graphics2D bufferdImgSurface;
</Font><font color="#000000" face="Comic Sans MS" size="2">
<BR>
<BR>
<BR>Scroll down until you find the function init() and add the following code:
<BR>
</FONT><font color="#0000CD" face="Comic Sans MS" size="2">
<BR>     bufferdImg = (BufferedImage)createImage(width, height);
<BR>     bufferdImgSurface = bufferdImg.createGraphics();
</Font><font color="#000000" face="Comic Sans MS" size="2">
<BR>
<BR>These two lines of code will set up the area to be drawn to.
<BR>
<BR>The last step is to modify the update(Graphics g) function. The code is as follows:
<BR>
</FONT><font color="#0000CD" face="Comic Sans MS" size="2">
<BR>     public void update(Graphics g)
<BR>     {
<BR>          Graphics2D g2 = (Graphics2D)g;
<BR>          // Set the background color.
<BR>          bufferdImgSurface.setBackground(Color.black);
<BR>
<BR>          // Clear the applet.
<BR>          bufferdImgSurface.clearRect(0, 0, width, height);
<BR>
<BR>          bufferdImgSurface.setColor(Color.green);
<BR>          //(X pos, Y pos, Width, Height)
<BR>          bufferdImgSurface.fillOval(currentX[0], currentY[0], 20,20);
<BR>
<BR>          g2.drawImage(bufferdImg, 0, 0, this);
<BR>     }
</Font><font color="#000000" face="Comic Sans MS" size="2">
<BR>
<BR>As you see we have changed it from drawing to ‘g2’ to ‘bufferedImgSurface’, and only at the very end drawing the whole frame to the screen:
</FONT><font color="#0000CD" face="Comic Sans MS" size="2">
<BR>     g2.drawImage(bufferdImg, 0, 0, this);
</Font><font color="#000000" face="Comic Sans MS" size="2">
<BR>
<BR>Now it’s ready to go. You should now have a reduction in the flickering. As I said it’s not the best way to do it but it works and it’s easy so it is fine for now.
<BR>
<BR>This next section is to show you how collision detection will be working in the game. You will notice that there is already some collision detection with the circle bouncing around the screen, but we will now expand on this. Please note most of this code will not be needed in our game so you may want to make a copy of your current file. Also you can skip this section if you wish but I recommend at least reading through it.
<BR>
<BR>Again we will start in the variables section. Locate the integer variable called MAX. The current value of this is 1 (one circle). We want to have 2 circles bouncing around the screen so we will change MAX to 2.
<BR>
<BR>Next we need to add two new variables:
</FONT><font color="#0000CD" face="Comic Sans MS" size="2">
<BR>     boolean collided=false;
<BR>     float dist;
<BR>
</Font><font color="#000000" face="Comic Sans MS" size="2">
<BR>‘collided’ is only true if the distance between the two points is less than the specified amount.
<BR>‘dist’ is the distance between the two points.
<BR>
<BR>In the ‘init()’ function add:
</FONT><font color="#0000CD" face="Comic Sans MS" size="2">
<BR>     currentX[1]=0;
<BR>     currentY[1]=100;
<BR>
<BR>     directionX[1]=0;
<BR>     directionY[1]=1;
<BR>
</Font><font color="#000000" face="Comic Sans MS" size="2">
<BR>This code is just the same as previous code so it shouldn’t need explaining.
<BR>
<BR>This next section of code should go in the ‘run()’ function just after the two circles have been moved:
<BR>
</FONT><font color="#0000CD" face="Comic Sans MS" size="2">
<BR>     dist = (int)(Math.sqrt(Math.pow((currentX[0]+20)-(currentX[1]+20),2) + Math.pow((currentY[1]+20)-(currentY[1]+20),2)));
<BR>
<BR>     if(dist < 20)
<BR>          collided = true;
<BR>     else
<BR>          collided = false;
<BR>
</Font><font color="#000000" face="Comic Sans MS" size="2">
<BR>The first line of code is the distance formula:
</FONT><font color="#0000CD" face="Comic Sans MS" size="2">
<BR>     sqrt(pow((X1)-(X2),2) + pow((Y1)-(Y2),2)))
<BR>
</Font><font color="#000000" face="Comic Sans MS" size="2">
<BR>This formula just calculates the distance between two points when given the X and Y cords.
<BR>
<BR>The next section is just an if statement that says if the distance between the two points is less than 20 then they must be touching so set ‘collided’ to true.
<BR>
<BR>Just a note. You may notice that in the distance formula I have the current position +20. This is because I am adding the diameter of the circle or you would only get the absolute X/Y cord.
<BR>
<BR>The last thing to add is to the ‘update(Graphics g)’ function:
</FONT><font color="#0000CD" face="Comic Sans MS" size="2">
<BR>     bufferdImgSurface.fillOval(currentX[1], currentY[1], 20,20);
<BR>
<BR>     if(collided==true)
<BR>          bufferdImgSurface.drawString("Collided",10,10);
<BR>
</Font><font color="#000000" face="Comic Sans MS" size="2">
<BR>Add those two lines just b4:
</FONT><font color="#0000CD" face="Comic Sans MS" size="2">
<BR>     g2.drawImage(bufferdImg, 0, 0, this);
<BR>
</Font><font color="#000000" face="Comic Sans MS" size="2">
<BR>Compile and run.
<BR>You should notice that the two circles both bounce around the screen. When the two circles are touching the word “Collided” is displayed in the top left hand corner.
<BR>
<BR>This is one of the simplest methods of collision detection and the method we will be using to detect a collision between the bullets, player and the enemy(s).
<BR>
<BR>It’s been a long time but now all the basics are now out of the way and its now time for us to start working on the actual game.
<BR>
<BR>This will require many modifications and additions to the code. Just to give you an idea of the size of the game, it’s around 7 pages.
<BR>
<BR>In this game we will be using the mouse for input we must do a few things to set up the mouse for input. First you must import the following package:
<BR>     java.awt.event.*;
<BR>
</Font><font color="#000000" face="Comic Sans MS" size="2">
<BR>You must also add to the class line:
</FONT><font color="#0000CD" face="Comic Sans MS" size="2">
<BR>     public class Game extends Applet implements Runnable, MouseMotionListener, MouseListener
<BR>
</Font><font color="#000000" face="Comic Sans MS" size="2">
<BR>That is all to the mouse section for now. We will be dealing with the mouse listener more throughout the code, but for now we will move onto the variables.
<BR>
<BR>First you can go and delete these variables as they are no longer needed:
</FONT><font color="#0000CD" face="Comic Sans MS" size="2">
<BR>     int directionX[] = new int[MAX];
<BR>     int directionY[] = new int[MAX];
</Font><font color="#000000" face="Comic Sans MS" size="2">
<BR>There are a lot of new variables to add so I am just going to give you the whole list that we will be using to make your’s and my life easier. Some of these you will already have, some you won’t. Also the comments next to them should explain them pretty well:
<BR>
</FONT><font color="#0000CD" face="Comic Sans MS" size="2">
<BR>     BufferedImage bufferdImg;
<BR>     Graphics2D bufferdImgSurface;
<BR>
<BR>     Thread gameThread;
<BR>
<BR>     int width=400, height=400, MAX=50, speed=10;
<BR>
<BR>     int currentX[] = new int[MAX];
<BR>     int currentY[] = new int[MAX];
<BR>
<BR>     int step=0,          // Number of movements left/right
<BR>     direction=1,          // Current left/right direction (0=left, 1=right)
<BR>     shipX=width/2-10,          // Current player X possition
<BR>     shipY=height-45,          // Current player Y possition
<BR>     mbx=-10,          // The mouse position after mouse down, sets the_
<BR>     mby=-10,          // enemy bullet position to this.
<BR>     randomShoot=0,          // Used to work out which enemy is shooting
<BR>     health=50,          // The players health
<BR>     BNUM=10,          // Number of bullets
<BR>     playing=0;          // Are is the game playing (0=Playing, 1=Paused, 2=Game Over, 3=Win)
<BR>
<BR>     int bX[] = new int[BNUM];	// Bullet X pos.
<BR>     int bY[] = new int[BNUM];	// Bullet Y pos.
<BR>
<BR>     int ebX[] = new int[BNUM]; // Enemy Bullet X pos.
<BR>     int ebY[] = new int[BNUM]; // Enemy Bullet Y pos.
<BR>
<BR>     long start=0,     // Frame start time
<BR>     tick_end_time,     // End frame time
<BR>     tick_duration,     // Time taken to display the frame
<BR>     sleep_duration;     // How long to sleep for
<BR>
<BR>     static final int 	MIN_SLEEP_TIME = 10,                    // Min time to sleep for
<BR>                              MAX_FPS = 20,						// Max frame rate.
<BR>                              MAX_MS_PER_FRAME = 1000 / MAX_FPS; 	// MS per frame
<BR>
<BR>     float fps=0, // Current frame rate
<BR>               dist;	// Distance between 2 points
<BR>
</Font><font color="#000000" face="Comic Sans MS" size="2">
<BR>The first function in our code is ‘start()’ this has no changes so lets move to the next one.
<BR>
<BR>Next is ‘init()’. As you remember this function sets our initial values. This has a few additions as follows:
<BR>
<BR>This section of code is for drawing a grid of circles 10 by 5.
<BR>Set up local integer variables for keeping track of what we have drawn.
<BR>
</FONT><font color="#0000CD" face="Comic Sans MS" size="2">
<BR>     int row=10,     // Current Y position
<BR>     col=10,     // Current X position
<BR>     count=0;     // How many circles have been drawn
<BR>
</Font><font color="#000000" face="Comic Sans MS" size="2">
<BR>We will set the first circle to the initial values of ‘row’ and ‘col’ so we have a starting point to work from:
</FONT><font color="#0000CD" face="Comic Sans MS" size="2">
<BR>     currentX[0]=col;
<BR>     currentY[0]=row;
<BR>
</Font><font color="#000000" face="Comic Sans MS" size="2">
<BR>This section actually sets the coordinates for each circle:
<BR>
</FONT><font color="#0000CD" face="Comic Sans MS" size="2">
<BR>     for(int i=0; i < 50; i++) {
<BR>          count++;
<BR>          currentX[i]=col;
<BR>          col+=25;
<BR>
<BR>          currentY[i]=row;
<BR>
<BR>          if(count==10){
<BR>               row+=25;
<BR>               col=10;
<BR>               count=0;
<BR>          }
<BR>     }
</Font><font color="#000000" face="Comic Sans MS" size="2">
<BR>This works by looping through each circle position. This in effect draws 10 circles with the Y value of 10. After it has looped through 10 times count will = 10. It will then add 25 to the ‘row’ value and draw another 10 circles with the Y value of 35. Each loop the X position is also moved across 25 points. It will keep doing this until 50 circles have been given values.
<BR>
</FONT><font color="#0000CD" face="Comic Sans MS" size="2">
<BR>The following two lines of code are used to start the mouse listener “listening” on the applet:
<BR>     addMouseMotionListener(this);
<BR>     addMouseListener(this);
<BR>
</Font><font color="#000000" face="Comic Sans MS" size="2">
<BR>‘MouseMotionListener’ is used for picking up the motion of the mouse. Things such as the X,Y cords and if the mouse is on the applet or not.
<BR>“MouseListener’ is used for detecting mouse clicks.
<BR>
<BR>The last section in the ‘init()’ function is just simply to give all the bullets a position off of the screen so they are hidden and ready to be fired.
</FONT><font color="#0000CD" face="Comic Sans MS" size="2">
<BR>     for(int i=0; i < BNUM; i++){
<BR>          bX[i]=-10;
<BR>          bY[i]=-10;
<BR>          ebX[i]=0;
<BR>          ebY[i]=height+10;
<BR>     }
<BR>
</Font><font color="#000000" face="Comic Sans MS" size="2">
<BR>The next function is ‘run()’. So many changes have been made to this function that you can basically delete it and I will go through it.
<BR>
</FONT><font color="#0000CD" face="Comic Sans MS" size="2">
<BR>     while(true){     // Starts the game loop
<BR>          start = System.currentTimeMillis(); // Sets the current time
<BR>
<BR>          if(playing==0){     // Are we playing or is the game over?
<BR>
</Font><font color="#000000" face="Comic Sans MS" size="2">
<BR>Next section we will move the aliens left and right. It will first move them to the right by adding 1 to step until step is greater then 15. When this occurs it will then set step to 0 and change the direction to 0 which means move them to the left. After it moves 15 positions it will also move down one row.
<BR>
</FONT><font color="#0000CD" face="Comic Sans MS" size="2">
<BR>     step++;
<BR>     for(int i=0; i < MAX; i++){
<BR>          if(step > 15) {
<BR>               if(direction==1){
<BR>                    direction=0;
<BR>               } else {
<BR>                    direction=1;
<BR>               }
<BR>          step=0;
<BR>          for(int j=0; j < MAX; j++)
<BR>               currentY[j]+=speed;
<BR>          }
<BR>          if(direction==1)
<BR>               currentX[i]+=speed;
<BR>          else
<BR>               currentX[i]-=speed;
<BR>     }
<BR>
</Font><font color="#000000" face="Comic Sans MS" size="2">
<BR>This next for loop is used to tell if the user has fired a bullet. If they have and there is a free bullet (set so only 10 bullets can be fired at once) then to set it to the current ship position. Also if the bullets are visible on the screen then move them up.
<BR>
</FONT><font color="#0000CD" face="Comic Sans MS" size="2">
<BR>     for(int i=0; i < BNUM; i++){
<BR>          if(bY[i] <= 0) {
<BR>               bX[i]=mbx;
<BR>               bY[i]=mby;
<BR>               mbx=-10;
<BR>               mby=-10;
<BR>          }
<BR>          bY[i]-=speed;
<BR>     }
<BR>
</Font><font color="#000000" face="Comic Sans MS" size="2">
<BR>Also related to the bullets is this for loop that detects any collision between the player’s bullets and the aliens. This section works by looping through each alien and then each bullet. If the distance between the two is less than 20 then a collision has occurred. The bullet and the alien will then be hidden.
<BR>
</FONT><font color="#0000CD" face="Comic Sans MS" size="2">
<BR>     for(int i=0; i < MAX; i++){
<BR>          for(int j=0; j < BNUM; j++) {
<BR>               if(!(bY[j]<=0)){
<BR>                    dist = (int)(Math.sqrt(Math.pow((currentX[i]+10)-bX[j],2) + Math.pow((currentY[i]+10)-bY[j],2)));
<BR>                    if(dist <= 20){
<BR>                         bY[j]=-50;
<BR>                         currentY[i]=-500;
<BR>                    }
<BR>               }
<BR>          }
<BR>     }
<BR>
</Font><font color="#000000" face="Comic Sans MS" size="2">
<BR>The next section is used for shooting the alien bullets. It works much the same as the previous shooting section. However this one will randomly pick a alien to shoot from.
<BR>
</FONT><font color="#0000CD" face="Comic Sans MS" size="2">
<BR>     for(int k=0; k < MAX; k++){
<BR>          randomShoot=(int)(Math.random()*MAX);
<BR>               if(currentY[randomShoot] >= 0){
<BR>                    for(int i=0; i < BNUM; i++){
<BR>                         if(ebY[i] >= height) {
<BR>                              ebX[i]=currentX[randomShoot];
<BR>                              ebY[i]=currentY[randomShoot];
<BR>                              break;
<BR>                         }
<BR>                    }
<BR>               }
<BR>     }
<BR>
</Font><font color="#000000" face="Comic Sans MS" size="2">
<BR>This is the collision detection section between the alien bullets and the player’s ship. Again it is similar to the previous section.
<BR>
</FONT><font color="#0000CD" face="Comic Sans MS" size="2">
<BR>     for(int j=0; j < BNUM; j++) {
<BR>          if(!(ebY[j]>=height)){
<BR>               dist = (int)(Math.sqrt(Math.pow((shipX+10)-ebX[j],2) + Math.pow((shipY+10)-ebY[j],2)));
<BR>               if(dist <= 20){
<BR>                    ebY[j]=height+10;
<BR>                    health-=10;
<BR>               }
<BR>          }
<BR>     }
</Font><font color="#000000" face="Comic Sans MS" size="2">
<BR>We now need to move all the alien bullets down the screen. I may not have mentioned this before but if you notice that the bullets position ‘ebY[]’ is moved to the current position plus ‘speed’. Everything that is required to move except for the ship is moved by the value ‘speed’. I did this so you can change the speed of the game if you wish.
<BR>
</FONT><font color="#0000CD" face="Comic Sans MS" size="2">
<BR>     for(int i=0; i < BNUM; i++){
<BR>          if(ebY[i] < height) {
<BR>               ebY[i]+=speed;
<BR>          }
<BR>     }
<BR>
</Font><font color="#000000" face="Comic Sans MS" size="2">
<BR>This is simple enough. If the player has no health left then set ‘playing’ to 2, which means it’s “Game Over”.
<BR>
</FONT><font color="#0000CD" face="Comic Sans MS" size="2">
<BR>     if(health <=0)
<BR>          playing=2;
<BR>
</Font><font color="#000000" face="Comic Sans MS" size="2">
<BR>This is the last section for the game loop. This will detect if all of the aliens have been destroyed, or if the aliens have invaded. If all aliens have been destroyed then set ‘playing’ to 3 which means the player wins.
<BR>
</FONT><font color="#0000CD" face="Comic Sans MS" size="2">
<BR>          int count=0;
<BR>          for(int j=0; j < MAX; j++){
<BR>               if(currentY[j]<0)
<BR>                    count++;
<BR>
<BR>               if(currentY[j]>=340)
<BR>                    playing=2;
<BR>          }
<BR>
<BR>          if(count==MAX)
<BR>               playing=3;
<BR>
<BR>
<BR>     } else { }
<BR>
<BR>     repaint();	// Redraw the screen
<BR>
</Font><font color="#000000" face="Comic Sans MS" size="2">
<BR>As explained this section calculates the frame rate and how long to sleep for. Please refer to the first tutorial for an explanation.
<BR>
</FONT><font color="#0000CD" face="Comic Sans MS" size="2">
<BR>               tick_end_time = System.currentTimeMillis();
<BR>               tick_duration = tick_end_time - start;
<BR>               sleep_duration = MAX_MS_PER_FRAME - tick_duration;
<BR>
<BR>               if (sleep_duration < MIN_SLEEP_TIME)
<BR>               {
<BR>                    sleep_duration = MIN_SLEEP_TIME;
<BR>               }
<BR>               fps = 1000 / (sleep_duration + tick_duration);
<BR>
<BR>               try{
<BR>                    Thread.sleep(sleep_duration);
<BR>                    } catch(InterruptedException e) {}
<BR>          }
<BR>     }
<BR>
</Font><font color="#000000" face="Comic Sans MS" size="2">
<BR>That’s the end of our ‘run()’ function. The next section for us to look at is the drawing section. Its all a lot to take in but don’t worry we are on the home stretch, only one more section after this.
<BR>
<BR>As I mentioned these functions are for drawing to the screen. I will go through most of the code again as I don’t want to miss anything out:
<BR>
</FONT><font color="#0000CD" face="Comic Sans MS" size="2">
<BR>     public void paint(Graphics g)
<BR>     {
<BR>          update(g);
<BR>     }
<BR>
<BR>     public void update(Graphics g)
<BR>     {
<BR>          Graphics2D g2 = (Graphics2D)g;
<BR>
<BR>     // Set the background color.
<BR>     bufferdImgSurface.setBackground(Color.black);
<BR>
<BR>     // Clear the applet.
<BR>     bufferdImgSurface.clearRect(0, 0, width, height);
<BR>
<BR>     bufferdImgSurface.setColor(Color.green);
<BR>     //(X pos, Y pos, Width, Height)
<BR>     for(int i=0; i < MAX; i++)
<BR>          bufferdImgSurface.fillOval(currentX[i], currentY[i], 20,20);
<BR>
<BR>     // Draw the read ship (a square)
<BR>     bufferdImgSurface.setColor(Color.red);
<BR>     bufferdImgSurface.fillRect(shipX, shipY, 20, 20);
<BR>
</Font><font color="#000000" face="Comic Sans MS" size="2">
<BR>This is a for loop that will draw all the bullets on the screen. I made it easy by having 10 bullets for the aliens and the player but if you change one of these numbers please be aware that it will cause problems in one place such as this. You would need to split the bullet drawing section into 2 for loops.
<BR>
</FONT><font color="#0000CD" face="Comic Sans MS" size="2">
<BR>     for(int j=0; j < BNUM; j++){
<BR>          bufferdImgSurface.setColor(Color.yellow);
<BR>          bufferdImgSurface.fillOval(bX[j], bY[j], 5,5);
<BR>
<BR>          bufferdImgSurface.setColor(Color.blue);
<BR>          bufferdImgSurface.fillOval(ebX[j], ebY[j], 5,10);
<BR>     }
<BR>     // Draw a bottom line to our window
<BR>     bufferdImgSurface.setColor(Color.red);
<BR>     bufferdImgSurface.drawString("_________________________________________________________",0,375);
<BR>
</Font><font color="#000000" face="Comic Sans MS" size="2">
<BR>These if statements display the game status, such as if the player looses it will display "****Game Over****".
<BR>
</FONT><font color="#0000CD" face="Comic Sans MS" size="2">
<BR>     if(playing==1)
<BR>          bufferdImgSurface.drawString("PAUSED", width/2-10, 390);
<BR>     else if(playing==2)
<BR>          bufferdImgSurface.drawString("****Game Over****", width/2-10, 390);
<BR>     else if(playing==3)
<BR>          bufferdImgSurface.drawString("****You Win!****", width/2-10, 390);
<BR>
</Font><font color="#000000" face="Comic Sans MS" size="2">
<BR>A simple way of displaying a health bar is to loop while the loop value is less than the value in health. On every loop draw a ‘|’. Set the X position to the current i value multiplied by 2 to give some spacing:
<BR>
</FONT><font color="#0000CD" face="Comic Sans MS" size="2">
<BR>          for(int i=0; i < health; i++)
<BR>               bufferdImgSurface.drawString(" |", (2*i), 390);
<BR>
<BR>          // Draw the buffered image to the screen.
<BR>          g2.drawImage(bufferdImg, 0, 0, this);
<BR>     }
<BR>
</Font><font color="#000000" face="Comic Sans MS" size="2">
<BR>That’s the last of our graphics section and now we are onto out last section!
<BR>This section is used for detecting mouse clicks and detecting the mouse position.
<BR>
<BR>Move the ship to the current mouse X position:
</FONT><font color="#0000CD" face="Comic Sans MS" size="2">
<BR>     public void mouseMoved(MouseEvent e) 	{ shipX=e.getX()-5; }
<BR>
<BR>     public void mouseDragged(MouseEvent e) 	{ shipX=e.getX()-5; }
<BR>
<BR>
</Font><font color="#000000" face="Comic Sans MS" size="2">
<BR>The user clicked a button so start firing a bullet from the current mouse X position and the current ship Y position:
</FONT><font color="#0000CD" face="Comic Sans MS" size="2">
<BR>     public void mouseClicked(MouseEvent e) 	{
<BR>          mbx=e.getX();
<BR>          mby=shipY;
<BR>     }
<BR>
<BR>     public void mousePressed(MouseEvent e) 	{
<BR>     mbx=e.getX();
<BR>     mby=shipY;
<BR>     }
<BR>
</Font><font color="#000000" face="Comic Sans MS" size="2">
<BR>
<BR>The mouse has entered the applet area so set ‘playing’ to 0 (start the game)
</FONT><font color="#0000CD" face="Comic Sans MS" size="2">
<BR>     public void mouseEntered(MouseEvent e) 	{ playing=0; }
<BR>
</Font><font color="#000000" face="Comic Sans MS" size="2">
<BR>The mouse has exited the applet area so set ‘playing’ to 1 (pause the game)
</FONT><font color="#0000CD" face="Comic Sans MS" size="2">
<BR>     public void mouseExited(MouseEvent e) 	{ playing=1; }
<BR>
</Font><font color="#000000" face="Comic Sans MS" size="2">
<BR>
<BR>We don’t use this function but you still must include it in your code or you will have errors:
</FONT><font color="#0000CD" face="Comic Sans MS" size="2">
<BR>     public void mouseReleased(MouseEvent e)	{ }
<BR>
</Font><font color="#000000" face="Comic Sans MS" size="2">
<BR>
<BR>
<BR>You should now be able to compile the code and play the game. Its basic I know but it should help with understanding of applets, threads and event handling.
<BR>
<BR>I hope you like my tutorial. If you find any errors please email me, also if you have any comments please email me.
<BR>
Also check out my website for more tutorials and code samples <a href="http://www.jcroucher.com">www.jcroucher.com</a>
<BR>
<BR>
<BR>This code and tutorial is copyright 2002 John Croucher.


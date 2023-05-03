Download Link: https://assignmentchef.com/product/solved-cs1520-project-2-java-graphical-components-and-event-handling
<br>
<strong>Goal: </strong>To get more experience with Java graphical components and event-handling, including MouseEvents, and to utilize Java Threads to allow motion in a graphical program.

<strong>Details: </strong>

Your program should have the <strong>same functionality as the one demonstrated in lecture</strong>.  This demonstration should be the primary way that you examine and understand the program specifications.  If you miss the demonstration in lecture, you must see either me or your TA for a demonstration during office hours.  Some specific requirements of the program are listed below, with some snapshots of the execution to show you what you need to do.

<strong>Idea:</strong>

Your program is to be a Java application that is window-based.  This means that your main class must extend JFrame.   Your program will implement a primitive version of the video game “Breakout”, which is described in more detail below.

<strong>The Game:</strong>

<ul>

 <li>The player gets a paddle that can move horizontally across the bottom of the screen. When the game is started, a ball “falls” down from a random starting point toward the bottom of the window.  The ball should be moving at an angle (not straight down).  See Figure 1.</li>

</ul>

<table>

 <tbody>

  <tr>

   <td width="4"></td>

   <td width="526"></td>

   <td width="2"></td>

   <td width="150"></td>

  </tr>

  <tr>

   <td></td>

   <td colspan="2"></td>

   <td rowspan="3" width="150">

    <table width="100%">

     <tbody>

      <tr>

       <td>Figure 1.  Note the layout of the game Window.  Your program should have a similar layout.  There should be a clear amount of room above and below the disks.  The easiest way to store and manipulate the disks is to use a two-dimensional array of rectangles for them.  The ball is a circle (ellipse, actually) and the paddle is a separate (private, inner) class that extends Rectangle2D.Double.  This allows the paddle to be used as a rectangle and to also allow additional methods to be added for it (for example, to move it across the screen).</td>

      </tr>

     </tbody>

    </table></td>

  </tr>

  <tr>

   <td></td>

   <td width="526">

    <table width="100%">

     <tbody>

      <tr>

       <td></td>

      </tr>

     </tbody>

    </table></td>

  </tr>

  <tr>

   <td></td>

  </tr>

 </tbody>

</table>




<ul>

 <li>The player’s job is to move the paddle so that the ball bounces off of it and back upward toward 6 rows of disks at the top of the screen. Each time the ball hits a disk, the disk is destroyed, and the ball bounces back off of it (usually back down toward the paddle – however, if the ball goes “above” the disks it can bounce around in that area, destroying many disks without the user even having to hit it – this is often a goal of a good Breakout player).  See Figure 2 below.</li>

</ul>




<table>

 <tbody>

  <tr>

   <td width="4"></td>

   <td width="563"></td>

   <td width="1"></td>

   <td width="114"></td>

  </tr>

  <tr>

   <td></td>

   <td rowspan="3" width="563">

    <table width="100%">

     <tbody>

      <tr>

       <td></td>

      </tr>

     </tbody>

    </table></td>

  </tr>

  <tr>

   <td></td>

   <td></td>

   <td width="114">

    <table width="100%">

     <tbody>

      <tr>

       <td>Figure 2.  Note here that the ball is “above” the disks and can bounce up there until it passes back down through an opening.  Also note that the labels on the bottom of the screen (in a panel) are showing the score and the number of balls remaining.  You  can score however you want, but it should be in a reasonable way.</td>

      </tr>

     </tbody>

    </table></td>

  </tr>

  <tr>

   <td></td>

  </tr>

 </tbody>

</table>




<ul>

 <li>If the player destroys all of the disks on the screen he/she has won the game. When this occurs, indicate the victory in the right label on the bottom of the screen.</li>

 <li>If the player “misses” the ball, it will fall through the bottom of the screen and a “new” ball will randomly appear for the player to hit. The player gets 3 balls per game – if he/she misses all of them he/she has lost the game.  When a player loses, indicate defeat in the right label on the bottom of the screen.</li>

 <li>When an initial disk is destroyed in the second “color” of disks, the speed of the ball should increase by a significant amount. This speed increase should occur again when a disk in the third “color” is destroyed.</li>

 <li>At any time during a game, the user can click on either the New Game or End Game buttons. New Game should end the current game and start a new one.  End Game should just stop the game (and its associated Threads and also remove the ball from the screen) and indicate that the game is over.</li>

</ul>

<strong>Implementation Details and Hints:</strong>

<ul>

 <li>Some things that you will need to do in this program will require some thought. Below are some details of things you will need to do and some hints at doing them:</li>

 <li><strong>Move the paddle across the screen:</strong> the left mouse button will move the paddle to the left as long as it is held down, and similar for the right mouse button. However, the paddle should not be allowed to move past either edge of the window.  The movement must be achieved by starting a “motion” thread for the paddle on mousePressed and stopping that thread (gracefully) on mouseReleased.  The reason for this is that you want the paddle to move at a consistent rate relative to the ball’s movement.  This can best be accomplished via Threads.</li>

 <li><strong>Move the ball:</strong> for this you should initially have a “deltaX” and a “deltaY” that get added to the ball’s location coordinates each time it moves.  To keep the games interesting, these can be initialized in a somewhat random fashion each game.  A thread will alternate sleeping and moving the ball, which translates to motion on the screen.  When the speed is “increased”, the deltaX and deltaY values are increased, which makes the ball appear to move faster. If the ball moves past the bottom of the screen, that ball (and its thread) should be destroyed.  If the user has any remaining balls, a new one should be created and started moving to continue the game.</li>

 <li><strong>Ball hitting the walls, the paddle and the disks:</strong> each time you move the ball, you can test to see if it is “hitting” another object using the intersects() method as defined for all Java <strong><em>Shape</em></strong> You can test to see if the ball hits the side walls or top wall by testing its coordinates against the known dimensions of the window.  When the ball hits something, either the deltaX or deltaY value should be reversed, depending upon where the ball hits (ex: if it is going down and hits the paddle, the deltaY should be reversed; if it is going up or down and hits the side wall, the deltaX should be reversed).  Additionally, if the ball has hit a disk, that disk should be removed from the array to indicate that it is no longer there (set its location to null).</li>

 <li><strong>Sound Effects:</strong> When the ball hits the paddle, a disk or any wall, an appropriate sound must be made. Sounds can easily be incorporated into Java programs using predefined classes and methods.  For more details on using Java sounds, see p. 553 of the Learning Java text and the online API.</li>

 <li><strong>Drawing the graphics:</strong> You must have a JPanel subclass that handles the graphical display of the game. Within this class the paintComponent() method will do the actual drawing.  This will simply draw the ball, paddle and disks each time it is called.  Be careful with null pointers – it is best to test for null before trying to draw an object.  It is also a good idea to have a separate thread in your program whose sole job is to refresh the screen (repaint()) every so often.  With this you will NOT have repaints from any other threads. You will find if you have repaint()s in your other threads that the graphics are choppy and unpredictable, since the repaints are occurring in different places at different rates.</li>

 <li><strong>Starting and stopping threads: </strong>recall that we do NOT want to use the deprecated stop() method, so you should stop threads using some Boolean condition to terminate the loop in the run() method. Make sure (especially when you do a New Game) that you terminate any running threads BEFORE starting new ones.  Otherwise you will have extra, unwanted threads running and it will cause irregular results (and waste CPU time).  In my version of the game, I have at most 3 threads running at a time: one for the paddle motion, one for the ball motion and one to refresh the screen.  Note that before a game is started and after a game completes NONE of these threads should be running.</li>

</ul>

<strong>Other Important Notes:</strong>

<ul>

 <li>Test your program thoroughly before handing it in. Make sure special situations are handled correctly and consistently.   There are a lot of situations that can cause the dreaded “Null Pointer Exception” (as explained above in paintComponent) if you are not careful.</li>

 <li>Since this program is somewhat complex, I strongly advise you to work on it one part at a time. For example, you may want to get the paddle motion to work, then the ball motion, then the disk interaction.  If you find that it is not working completely when it is time to turn it in, be sure to <strong>show what you have working</strong> so that you can get partial credit.</li>

</ul>

<strong>Extra Credit:</strong>

<ul>

 <li>Since this program is challenging but also potentially fun, I will allow for up to 15 extra credit points on it. There are MANY ways to improve this program, some of which are listed below.</li>

 <li>Make the ball motion more interesting by having the “bounce” from the paddle differ depending upon where on the paddle it hits. In the arcade game, a “bounce” from the edge of the paddle causes the ball to move at a harsher angle, making it harder for the user to hit it the next time.</li>

 <li>As rows of disks are destroyed, make the game more challenging by reducing the paddle size.</li>

 <li>Add additional “levels” to the game. Each time a user completes a level he/she goes on to the next level.  These can be more challenging by having more disks or a faster speed or both.</li>

 <li>Allow the user to “pause” the game by clicking on a button. This will temporarily stop the game where it is and will resume when the user clicks on the button again.</li>

 <li>In addition to your application program, write another version that is an applet and submit that together with the .html file necessary to run it.</li>

 <li>If you have any other extra credit ideas, be sure to ask me about them before putting in the effort. Also realize that 15 points is significant but still not an outrageous amount of credit.  Don’t spend a disproportionate amount of time on extra credit!</li>

</ul>

<strong>The README:</strong>

<ul>

 <li>Since all games are likely to have some variation in them, you must prepare a README.TXT file that precisely describes how to play your game. Be sure to include in your README.TXT any extra features that you have added, so that the user (i.e. TA) can take advantage of them.</li>

</ul>
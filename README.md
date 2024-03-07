# breakout
import pygame
import random
pygame.init()
screen = pygame.display.set_mode((700,500))
pygame.display.set_caption("breakout")
jump = pygame.mixer.Sound('jumping.MP3')
music = pygame.mixer.music.load('chocolate.MP3')
pygame.mixer.music.set_volume(0.25)
pygame.mixer.music.play(-1)

class brick:
    def __init__(self,xpos, ypos):
        self.xpos = xpos
        self.ypos = ypos
        self.color = (random.randrange(100, 250),random.randrange(100, 250),random.randrange(100, 250))
        self.isDead = False
    def draw(self):
        if not self.isDead:
            pygame.draw.rect(screen, self.color, (self.xpos, self.ypos, 100, 50))
    def collide(self, ball_x, ball_y):
        if not self.isDead:
            if (ball_x + 15 > self.xpos and
                ball_x < self.xpos + 100 and
                ball_y + 15 > self.ypos and
                ball_y < self.ypos + 50):
                self.isDead= True
                return True
        return False
#____________________________________________

doExit = False

clock = pygame.time.Clock()

p1Score = 0

       
#paddle
p1x = 320
p1y = 450
#ball
bx = 350 #X-Axis
by = 250 #Y-Axis
bVx = 10 #X Velocity
bVy = 10 #Y Velocity

b1 = brick(50, 70)     
b2 = brick(200, 70)
b3 = brick(340, 70)     
b4 = brick(470, 70)
b5 = brick(100, 130)     
b6 = brick(240, 130)
b7 = brick(370, 130)     
b8 = brick(500, 130)
while not doExit:   #game loop
   
       
    #In game clock
    clock.tick(60)
   
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            doExit = True

        #Insert Game Logic here:
       

       
       
    keys = pygame.key.get_pressed()
    if keys[pygame.K_LEFT]:
        p1x-=15
        pygame.mixer.Sound.play(jump)
    if keys[pygame.K_RIGHT]:
        p1x+=15
        pygame.mixer.Sound.play(jump)
        
       


    bx += bVx
    by += bVy


       
    if bx < 0 or bx + 15 > 700: #left wall bounds checking
        bVx *= -1#reflect!
           
           
    if by < 0 or by + 15 > 500:
        bVy *= -1
        print("bounce!")

   
    #hit box detection with paddle 1
 
    
    if bx < p1x + 100 and bx > p1x and by  > p1y and by < p1y + 20:
        bVy *= -1
        
    if b1.collide(bx, by):
        bVy *= -1
    if b2.collide(bx, by):
        bVy *= -1
    if b3.collide(bx, by):
        bVy *= -1
    if b4.collide(bx, by):
        bVy *= -1
    if b5.collide(bx, by):
        bVy *= -1
    if b6.collide(bx, by):
        bVy *= -1
    if b7.collide(bx, by):
        bVy *= -1
    if b8.collide(bx, by):
        bVy *= -1
   

   
        #Render section go here:
    screen.fill((0,0,0)) #black screen
    pygame.draw.line(screen, (200, 200, 200), [0, 450], [700, 450], 5) #Second Mid line
    pygame.draw.line(screen, (200, 200, 200), [0, 50], [700, 50], 5) #Second Mid line
    b1.draw()
    b2.draw()
    b3.draw()
    b4.draw()
    b5.draw()
    b6.draw()
    b7.draw()
    b8.draw()
       
        # Paddles
    pygame.draw.rect(screen, (255, 255, 255), (p1x, p1y, 100, 20), 15)
        #B A L L S
    pygame.draw.circle(screen, (255, 255, 255), (bx, by), 15, 15)
    pygame.draw.circle(screen, (0, 0, 0), (bx, by), 10, 5)
       
       
        #screen updates
    pygame.display.flip()
       
       
       
#END GAME LOOP:

pygame.quit()

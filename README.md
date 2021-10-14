# visualization-selection-sorting
visualization-selection-sorting
```python3
import pygame,sys
import time
import random

FPS=60
WIDTH=700
HEIGHT=500
arr=[]
judge=0

pygame.init()
pygame.display.set_caption('Sorting')# name of the window
screen=pygame.display.set_mode([WIDTH,HEIGHT])
clock=pygame.time.Clock()


font_name=pygame.font.match_font('arial')
def draw_text(surf,text,size,x,y):
    font=pygame.font.Font(font_name,size)
    text_surface=font.render(text,True,[255,255,255])
    text_rect=text_surface.get_rect()
    text_rect.centerx=x
    text_rect.top=y
    surf.blit(text_surface,text_rect)

def draw_init():
    screen.fill((0,0,0))
    draw_text(screen,'Click any bottom to start',50,WIDTH//2,HEIGHT//3+20)
    pygame.display.update()
    waiting=True
    while waiting:
        clock.tick(FPS)
        for event in pygame.event.get():
            if event.type==pygame.QUIT:
                sys.exit()
            elif event.type==pygame.KEYDOWN:
                waiting=False

for i in range(200):
    arr+=[i]
random.shuffle(arr)
ans=sorted(arr)


show_init=True

rem=0
ii=0
pos=0

while True:
    if show_init:
        draw_init()
        show_init=False
    clock.tick()
    for event in pygame.event.get():
        if event.type==pygame.QUIT:
            sys.exit()

    screen.fill((0,0,0))
    w=2
    for i in range(200):
        pygame.draw.rect(screen,[255,255,255],[50+i*(w+1),300-arr[i],w,arr[i]],0)
    min_val=1e9
    for j in range(ii,200):
        if arr[j]<min_val:
            min_val=arr[j]
            pos=j
    arr[ii],arr[pos]=arr[pos],arr[ii]
    ii+=1
    if ii==200:
        ii=199
    
    if ans==arr:
        draw_text(screen,'Finish',50,350,400)
    pygame.display.update()

```

import pygame, time, sys, random, os
from pygame.locals import *
from time import gmtime, strftime

pygame.init()

w = 640
h = 400

screen = pygame.display.set_mode((w, h),RESIZABLE)
clock = pygame.time.Clock()
x = y = 100

def starting():
    basicfont = pygame.font.SysFont(None, 48)
    text = basicfont.render('Starting...', True, (255, 255, 255), (0, 0, 255))
    textrect = text.get_rect()
    textrect.centerx = screen.get_rect().centerx
    textrect.centery = screen.get_rect().centery
    screen.fill((0, 0, 255))
    screen.blit(text, textrect)
    pygame.display.update()

def taskbar():
    basicfont = pygame.font.SysFont(None, 24)
    pygame.draw.rect(screen, ((0, 255, 0)), (0, h-40, w, 40), 0)
    text = basicfont.render(strftime("%Y-%m-%d", gmtime()), True, (0, 0, 0))
    text2 = basicfont.render(strftime("%H:%M:%S", gmtime()), True, (0, 0, 0))
    screen.blit(text, (w - 100, h - 37))
    screen.blit(text2, (w - 100, h - 17))
    logoimage = pygame.image.load("C:\Users\chef\Desktop\logo.png").convert()
    logoimage = pygame.transform.scale(logoimage, (40, 40))
    screen.blit(logoimage, (0, h-40),)

def start():
    button1, button2, button3 = pygame.mouse.get_pressed()
    mousex, mousey = pygame.mouse.get_pos()
    if 0 < mousex < 40 and h-40 < mousey < h:
        if button1:
            pygame.draw.rect(screen, ((255, 0, 0)), (0, int(h/2), int(w/6), int(h/2)-40), 0)
    pygame.display.update()

starting()
#time.sleep(2)

while 1:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            sys.exit()  
        elif event.type==VIDEORESIZE:
            w = event.dict['size'][0]
            h = event.dict['size'][1]
            screen=pygame.display.set_mode(event.dict['size'],RESIZABLE)
    screen.fill((255, 255, 255))
    taskbar()
    start()
    pygame.display.update()
    clock.tick(60)

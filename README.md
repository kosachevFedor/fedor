from pygame import *
from random import *
clock = time.Clock()
window = display.set_mode((1300, 700))
display.set_caption("Labirinth")
background = transform.scale(image.load("backg.jpg"), (1300,700))
mixer.init()
mixer.music.load("backk.mp3")
mixer.music.set_volume(0.01)
mixer.music.play()
class GameSprite(sprite.Sprite):
    def __init__(self, play_image, play_x, play_y, play_speed):
        super()._init_()
        self.image = transform.scale(image.load(play_image), (50, 50))
        self.speed = play_speed
        self.rect = self.image.get_rect()
        self.rect.x = play_x
        self.rect.y = play_y
    def reset(self):
        window.blit((self.image), (self.rect.x, self.rect.y))
class Player(GameSprite):
    def __init__(self, play_image, play_x, play_y, play_speed):
        super()._init_(play_image, play_x, play_y, play_speed)
    def run(self):
        key_pressed = key.get_pressed()
        if key_pressed[K_w] and self.rect.y > 0:
            self.rect.y -= self.speed
        if key_pressed[K_s] and self.rect.y < 650:
            self.rect.y += self.speed
        if key_pressed[K_d] and self.rect.x < 1250:
            self.rect.x += self.speed
        if key_pressed[K_a] and self.rect.x > 0:
            self.rect.x -= self.speed
class Enemy(GameSprite):
    def __init__(self, play_image, play_x, play_y, play_speed):
        super()._init_(play_image, play_x, play_y, play_speed)
    def rand(self,x00,x01):
        if self.rect.x <= x01 or self.rect.x >= x00:
            self.rect.x -= self.speed
        if self.rect.x == x01 or self.rect.x == x00:
            self.speed = -1*self.speed
    

                


s_play = Player("hero.png",100,100,7)
s1_enemy = Enemy("cyborg.png",1250,300,5)
s2_enemy = Enemy("cyborg.png",1000,100,5)
game = True
a = 0
while game:
    window.blit(background, (0,0))
    s_play.reset()
    s_play.run()
    s1_enemy.reset()
    s2_enemy.reset()
    s1_enemy.rand(1000,1250)
    s2_enemy.rand(750,1000)
    for e in event.get():
        if e.type == QUIT:
            game = False

    clock.tick(60)
    display.update()

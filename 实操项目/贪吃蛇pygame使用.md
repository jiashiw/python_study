### 1. 游戏初始化设置
  * 初始化框架 pygame.init()
  * 游戏窗口设置 pygame.display.set_mode(x,y)
  * 窗口标题 pygame.display.set_caption(‘’)
  * 程序主循环（处理事件、更新游戏状态、绘制游戏状态到屏幕上）
  * 设置休息帧数 pygame.time.Clock().tick
  * 渲染 pygame.draw.rect(渲染对象, 渲染颜色, 渲染范围)

```
import pygame
import sys

# 2.设置窗口及标题
screen_x = 800
screen_y = 600
window = pygame.display.set_mode((screen_x, screen_y))
pygame.display.set_caption('贪吃蛇')

# 3.设置事件循环和帧数
clock = pygame.time.Clock()

while quit:
    clock.tick(30)  # 设置帧数
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            pygame.quit()
            sys.exit()
    pygame.draw.rect(window, (245, 135, 155), (0, 0, screen_x, screen_y))
    pygame.display.flip()

```

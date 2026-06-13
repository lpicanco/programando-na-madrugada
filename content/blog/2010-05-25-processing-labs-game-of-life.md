---
title: 'Processing Labs: Game Of Life'
date: '2010-05-25T23:37:00Z'
categories:
- Processing
- Javascript
tags:
- game of life
- Javascript
- Processing
---

Comecei a estudar [processing](http://processing.org). Processing é uma linguagem de programação para trabalhar com visualização de dados. [Processing.js](http://processingjs.org) é um porte da linguagem para Javascript.

Como primeiro experimento, o famoso [Game of Life](http://en.wikipedia.org/wiki/Conway's_Game_of_Life):

```javascript
int sx, sy;
float density = 0.5;
int[][][] world;

void setup() {
    size(100, 100);
    frameRate(15);
    sx = width;
    sy = height;
    world = new int[sx][sy][2];
    stroke(255);
    // Set random cells to 'on'
    for (int i = 0; i < sx * sy * density; i++) {
        world[(int) random(sx)][(int) random(sy)][1] = 1;
    }
}

void draw() {
    background(0);
    // Drawing and update cycle
    for (int x = 0; x < sx; x = x + 1) {
        for (int y = 0; y < sy; y = y + 1) {
            if ((world[x][y][1] == 1) || (world[x][y][1] == 0 && world[x][y][0] == 1)) {
                world[x][y][0] = 1;
                point(x, y);
            }
            if (world[x][y][1] == -1) {
                world[x][y][0] = 0;
            }
            world[x][y][1] = 0;
        }
    }
    // Birth and death cycle
    for (int x = 0; x < sx; x = x + 1) {
        for (int y = 0; y < sy; y = y + 1) {
            int count = neighbors(x, y);
            if (count == 3 && world[x][y][0] == 0) {
                world[x][y][1] = 1;
            }
            if ((count < 2 || count > 3) && world[x][y][0] == 1) {
                world[x][y][1] = -1;
            }
        }
    }
}

// Count the number of adjacent cells 'on'
int neighbors(int x, int y) {
    return world[(x + 1) % sx][y][0] + world[x][(y + 1) % sy][0] + world[(x + sx - 1) % sx][y][0] + world[x][(y + sy - 1) % sy][0] + world[(x + 1) % sx][(y + 1) % sy][0] + world[(x + sx - 1) % sx][(y + 1) % sy][0] + world[(x + sx - 1) % sx][(y + sy - 1) % sy][0] + world[(x + 1) % sx][(y + sy - 1) % sy][0];
}
```
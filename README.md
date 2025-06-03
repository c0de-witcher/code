//bresenham line 
#include <graphics.h>
#include <conio.h>
#include <iostream.h>

void drawMidPointLine(int x0, int y0, int x1, int y1) {
    int dx = x1 - x0;
    int dy = y1 - y0;

    int x = x0;
    int y = y0;

    int p = 2 * dy - dx;

    putpixel(x, y, WHITE); 

    for (int i = 0; i < dx; i++) {
        x++;
        if (p < 0) {
            p = p + 2 * dy;
        } else {
            y++;
            p = p + 2 * dy - 2 * dx;
        }
        putpixel(x, y, WHITE); 
    }
}

int main() {
    int gd = DETECT, gm;
    initgraph(&gd, &gm, "C:\\Turboc3\\BGI");

    int x0, y0, x1, y1;
    cout << "Enter starting point (x0 y0): ";
    cin >> x0 >> y0;
    cout << "Enter ending point (x1 y1): ";
    cin >> x1 >> y1;

    drawMidPointLine(x0, y0, x1, y1);

    getch();
    closegraph();
    return 0;
}






//DDA line
#include <graphics.h>
#include <conio.h>
#include <iostream.h>
#include <math.h>  


int roundOff(float num) {
    return int(num + 0.5);
}


int maxValue(int a, int b) {
    return (a > b) ? a : b;
}

void drawLineDDA(int x0, int y0, int x1, int y1) {
    int dx = x1 - x0;
    int dy = y1 - y0;

    int steps = maxValue(abs(dx), abs(dy));

    float xIncrement = dx / (float)steps;
    float yIncrement = dy / (float)steps;

    float x = x0;
    float y = y0;

    for (int i = 0; i <= steps; i++) {
        putpixel(roundOff(x), roundOff(y), WHITE);
        x += xIncrement;
        y += yIncrement;
    }
}

int main() {
    int gd = DETECT, gm;
    initgraph(&gd, &gm, "C:\\Turboc3\\BGI");

    int x0, y0, x1, y1;
    cout << "Enter starting point (x0 y0): ";
    cin >> x0 >> y0;
    cout << "Enter ending point (x1 y1): ";
    cin >> x1 >> y1;

    drawLineDDA(x0, y0, x1, y1);

    getch();
    closegraph();
    return 0;
}





//mid point circle
#include <graphics.h>
#include <conio.h>
#include <iostream.h>


void drawCircleMidpoint(int xc, int yc, int r) {
    int x = 0;
    int y = r;
    int p = 1 - r;

    
    while (x <= y) {
        putpixel(xc + x, yc + y, WHITE);
        putpixel(xc - x, yc + y, WHITE);
        putpixel(xc + x, yc - y, WHITE);
        putpixel(xc - x, yc - y, WHITE);
        putpixel(xc + y, yc + x, WHITE);
        putpixel(xc - y, yc + x, WHITE);
        putpixel(xc + y, yc - x, WHITE);
        putpixel(xc - y, yc - x, WHITE);

        x++;

        if (p < 0) {
            p = p + 2 * x + 1;
        } else {
            y--;
            p = p + 2 * (x - y) + 1;
        }
    }
}

int main() {
    int gd = DETECT, gm;
    initgraph(&gd, &gm, "C:\\Turboc3\\BGI");

    int xc, yc, r;
    cout << "Enter center of circle (xc yc): ";
    cin >> xc >> yc;
    cout << "Enter radius of circle: ";
    cin >> r;

    drawCircleMidpoint(xc, yc, r);

    getch();
    closegraph();
    return 0;
}


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




//ellipse
#include <graphics.h>
#include <conio.h>
#include <iostream.h>

void drawEllipseMidpoint(int xc, int yc, int rx, int ry) {
    float x = 0;
    float y = ry;


    float rx2 = rx * rx;
    float ry2 = ry * ry;
    float twoRx2 = 2 * rx2;
    float twoRy2 = 2 * ry2;

    float px = 0;
    float py = twoRx2 * y;

    
    float p1 = ry2 - (rx2 * ry) + (0.25 * rx2);
    while (px < py) {
        putpixel(xc + x, yc + y, WHITE);
        putpixel(xc - x, yc + y, WHITE);
        putpixel(xc + x, yc - y, WHITE);
        putpixel(xc - x, yc - y, WHITE);

        x++;
        px += twoRy2;
        if (p1 < 0) {
            p1 += ry2 + px;
        } else {
            y--;
            py -= twoRx2;
            p1 += ry2 + px - py;
        }
    }

   
    float p2 = (ry2 * (x + 0.5) * (x + 0.5)) + (rx2 * (y - 1) * (y - 1)) - (rx2 * ry2);
    while (y >= 0) {
        putpixel(xc + x, yc + y, WHITE);
        putpixel(xc - x, yc + y, WHITE);
        putpixel(xc + x, yc - y, WHITE);
        putpixel(xc - x, yc - y, WHITE);

        y--;
        py -= twoRx2;
        if (p2 > 0) {
            p2 += rx2 - py;
        } else {
            x++;
            px += twoRy2;
            p2 += rx2 - py + px;
        }
    }
}

int main() {
    int gd = DETECT, gm;
    initgraph(&gd, &gm, "C:\\Turboc3\\BGI");

    int xc, yc, rx, ry;
    cout << "Enter center of ellipse (xc yc): ";
    cin >> xc >> yc;
    cout << "Enter x-radius (rx): ";
    cin >> rx;
    cout << "Enter y-radius (ry): ";
    cin >> ry;

    drawEllipseMidpoint(xc, yc, rx, ry);

    getch();
    closegraph();
    return 0;
}





//flood fill 
#include <graphics.h>
#include <conio.h>
#include <iostream.h>


int main() {
    int gd = DETECT, gm;
    initgraph(&gd, &gm, "C:\\Turboc3\\BGI");

    int n;
    cout << "Enter number of vertices: ";
    cin >> n;

   
    int points[20]; 

    for (int i = 0; i < n; i++) {
        cout << "Enter coordinates of vertex " << i + 1 << " (x y): ";
        cin >> points[2 * i] >> points[2 * i + 1];
    }

  
    points[2 * n] = points[0];
    points[2 * n + 1] = points[1];

    setcolor(WHITE); 
    drawpoly(n + 1, points);

    setfillstyle(SOLID_FILL, GREEN);

    
    int x, y;
    cout << "Enter seed point inside the polygon (x y): ";
    cin >> x >> y;

    floodfill(x, y, WHITE); 

    getch();
    closegraph();
    return 0;
}

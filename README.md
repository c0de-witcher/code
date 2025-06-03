//mid point line 
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

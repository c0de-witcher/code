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





//boundary fill
#include <graphics.h>
#include <conio.h>
#include <iostream.h>



void boundaryFill(int x, int y, int fill_color, int boundary_color) {
    int current = getpixel(x, y);
    if (current != boundary_color && current != fill_color) {
        putpixel(x, y, fill_color);

        boundaryFill(x + 1, y, fill_color, boundary_color);
        boundaryFill(x - 1, y, fill_color, boundary_color);
        boundaryFill(x, y + 1, fill_color, boundary_color);
        boundaryFill(x, y - 1, fill_color, boundary_color);
    }
}

int main() {
    int gd = DETECT, gm;
    initgraph(&gd, &gm, "C:\\Turboc3\\BGI");

    int n;
    cout << "Enter number of vertices: ";
    cin >> n;

    int points[40];  

    for (int i = 0; i < n; i++) {
        cout << "Enter vertex " << i + 1 << " (x y): ";
        cin >> points[2 * i] >> points[2 * i + 1];
    }

   
    points[2 * n] = points[0];
    points[2 * n + 1] = points[1];

    setcolor(WHITE);  
    drawpoly(n + 1, points);

    int seedX, seedY;
    cout << "Enter seed point inside the polygon (x y): ";
    cin >> seedX >> seedY;

    int fill_color = GREEN;
    int boundary_color = WHITE;

    boundaryFill(seedX, seedY, fill_color, boundary_color);

    getch();
    closegraph();
    return 0;
}


//2d translation
#include <graphics.h>
#include <conio.h>
#include <iostream.h>

int main() {
    int gd = DETECT, gm;
    initgraph(&gd, &gm, "C:\\Turboc3\\BGI");

    int n;
    cout << "Enter number of vertices: ";
    cin >> n;

    int x[20], y[20];
    cout << "Enter coordinates of vertices:\n";
    for (int k = 0; k < n; k++) {
        cout << "Vertex " << k + 1 << " (x y): ";
        cin >> x[k] >> y[k];
    }

    int tx, ty;
    cout << "Enter translation factors (Tx Ty): ";
    cin >> tx >> ty;

    
    setcolor(WHITE);
    for (int i = 0; i < n - 1; i++) {
        line(x[i], y[i], x[i + 1], y[i + 1]);
    }
    line(x[n - 1], y[n - 1], x[0], y[0]); 

    
    setcolor(GREEN);
    for (int j = 0; j < n - 1; j++) {
        line(x[j] + tx, y[j] + ty, x[j + 1] + tx, y[j + 1] + ty);
    }
    line(x[n - 1] + tx, y[n - 1] + ty, x[0] + tx, y[0] + ty);

    getch();
    closegraph();
    return 0;
}




//2d scaling#include <graphics.h>
#include <conio.h>
#include <iostream.h>


int main() {
    int gd = DETECT, gm;
    initgraph(&gd, &gm, "C:\\Turboc3\\BGI");

    int n;
    cout << "Enter number of vertices: ";
    cin >> n;

    int x[20], y[20];
    cout << "Enter coordinates of vertices:\n";
    for (int i = 0; i < n; i++) {
        cout << "Vertex " << i + 1 << " (x y): ";
        cin >> x[i] >> y[i];
    }

    float sx, sy;
    cout << "Enter scaling factors (Sx Sy): ";
    cin >> sx >> sy;

    
    setcolor(WHITE);
    for (int ij = 0; ij < n - 1; ij++) {
        line(x[ij], y[ij], x[ij + 1], y[ij + 1]);
    }
    line(x[n - 1], y[n - 1], x[0], y[0]);

   
    setcolor(GREEN);
    for (int ik = 0; ik < n - 1; ik++) {
        line(x[ik] * sx, y[ik] * sy, x[ik + 1] * sx, y[ik + 1] * sy);
    }
    line(x[n - 1] * sx, y[n - 1] * sy, x[0] * sx, y[0] * sy);

    getch();
    closegraph();
    return 0;
}



//2d rotation
#include <graphics.h>
#include <conio.h>
#include <iostream.h>
#include <math.h>


int main() {
    int gd = DETECT, gm;
    initgraph(&gd, &gm, "C:\\Turboc3\\BGI");

    int n;
    cout << "Enter number of vertices: ";
    cin >> n;

    int x[20], y[20];
    cout << "Enter coordinates of vertices:\n";
    for (int ih = 0; ih < n; ih++) {
        cout << "Vertex " << ih + 1 << " (x y): ";
        cin >> x[ih] >> y[ih];
    }

    float angle;
    cout << "Enter angle of rotation (in degrees): ";
    cin >> angle;

    float rad = angle * 3.14159 / 180.0;  

    
    setcolor(WHITE);
    for (int ik = 0; ik < n - 1; ik++) {
        line(x[ik], y[ik], x[ik + 1], y[ik + 1]);
    }
    line(x[n - 1], y[n - 1], x[0], y[0]);

    
    setcolor(GREEN);
    for (int i = 0; i < n - 1; i++) {
        int x1 = x[i] * cos(rad) - y[i] * sin(rad);
        int y1 = x[i] * sin(rad) + y[i] * cos(rad);
        int x2 = x[i + 1] * cos(rad) - y[i + 1] * sin(rad);
        int y2 = x[i + 1] * sin(rad) + y[i + 1] * cos(rad);
        line(x1, y1, x2, y2);
    }
    int x1 = x[n - 1] * cos(rad) - y[n - 1] * sin(rad);
    int y1 = x[n - 1] * sin(rad) + y[n - 1] * cos(rad);
    int x2 = x[0] * cos(rad) - y[0] * sin(rad);
    int y2 = x[0] * sin(rad) + y[0] * cos(rad);
    line(x1, y1, x2, y2);

    getch();
    closegraph();
    return 0;
}



//2d_shearing
#include <graphics.h>
#include <conio.h>
#include <iostream.h>

int main() {
    int gd = DETECT, gm;
    initgraph(&gd, &gm, "C:\\Turboc3\\BGI");

    int n;
    cout << "Enter number of vertices: ";
    cin >> n;

    int x[20], y[20];
    cout << "Enter coordinates of vertices:\n";
    for (int ia = 0; ia < n; ia++) {
        cout << "Vertex " << ia + 1 << " (x y): ";
        cin >> x[ia] >> y[ia];
    }

    float shx, shy;
    cout << "Enter shearing factors (shx shy): ";
    cin >> shx >> shy;

   
    setcolor(WHITE);
    for (int ic = 0; ic < n - 1; ic++) {
        line(x[ic], y[ic], x[ic + 1], y[ic + 1]);
    }
    line(x[n - 1], y[n - 1], x[0], y[0]);

   
    setcolor(GREEN);
    for (int i = 0; i < n - 1; i++) {
        int x1 = x[i] + shx * y[i];
        int y1 = y[i] + shy * x[i];
        int x2 = x[i + 1] + shx * y[i + 1];
        int y2 = y[i + 1] + shy * x[i + 1];
        line(x1, y1, x2, y2);
    }
    int x1 = x[n - 1] + shx * y[n - 1];
    int y1 = y[n - 1] + shy * x[n - 1];
    int x2 = x[0] + shx * y[0];
    int y2 = y[0] + shy * x[0];
    line(x1, y1, x2, y2);

    getch();
    closegraph();
    return 0;
}



//3d translation
#include <graphics.h>
#include <conio.h>
#include <iostream.h>


// Function to project 3D point to 2D (simple isometric projection)
void project(int x, int y, int z, int &px, int &py) {
    px = x - z;
    py = y - z;
}

// Function to draw a cuboid using 8 points
void drawCuboid(int x[], int y[], int z[], int color) {
    int px[8], py[8];

    int i;
    for ( i = 0; i < 8; i++) {
        project(x[i], y[i], z[i], px[i], py[i]);
    }

    setcolor(color);

    // Front face
    line(px[0], py[0], px[1], py[1]);
    line(px[1], py[1], px[2], py[2]);
    line(px[2], py[2], px[3], py[3]);
    line(px[3], py[3], px[0], py[0]);

    // Back face
    line(px[4], py[4], px[5], py[5]);
    line(px[5], py[5], px[6], py[6]);
    line(px[6], py[6], px[7], py[7]);
    line(px[7], py[7], px[4], py[4]);

    // Connect front and back
    line(px[0], py[0], px[4], py[4]);
    line(px[1], py[1], px[5], py[5]);
    line(px[2], py[2], px[6], py[6]);
    line(px[3], py[3], px[7], py[7]);
}

int main() {
    int gd = DETECT, gm;
    initgraph(&gd, &gm, "C:\\Turboc3\\BGI");

    int x[8], y[8], z[8];
    int j;

    cout << "Enter coordinates of the cuboid (8 points: x y z for each):\n";
    for ( j = 0; j < 8; j++) {
        cout << "Point " << j << " (x y z): ";
        cin >> x[j] >> y[j] >> z[j];
    }

    // Draw original cuboid
    drawCuboid(x, y, z, WHITE);
    outtextxy(10, 10, "Original Cuboid - WHITE");

    getch();

    // Translation vector
    int tx, ty, tz;
    cout << "Enter translation vector (tx ty tz): ";
    cin >> tx >> ty >> tz;

    // Apply translation
    int k;
    for ( k = 0; k < 8; k++) {
        x[k] += tx;
        y[k] += ty;
        z[k] += tz;
    }

    cleardevice();

    // Draw translated cuboid
    drawCuboid(x, y, z, GREEN);
    outtextxy(10, 10, "Translated Cuboid - GREEN");

    getch();
    closegraph();
    return 0;
}


# Fungsi-keyboard
membuat banyak titik

#include<Glut.h> 
#include<stdio.h>

float r, g, b, x, y;
bool check = true;

void mouse(int button, int state, int mousex, int mousey)
{
	if (button == GLUT_LEFT_BUTTON && state == GLUT_DOWN)
	{
		check = true;

		x = mousex;
		y = 480 - mousey;

		r = 1;
		g = 1;
		b = 1;
		printf("tombol KIRI (%d, %d) \n", x, y);
	}

	glutPostRedisplay();
}

void myKeyboard(unsigned char key, int x, int y) {
	if (key == 'r')
		r += 0.1;
	else if (key == 'R')
		r -= 0.1;
	else if (key == 'g') {
		g += 0.1;
	}
	else if (key == 'G') {
		g -= 0.1;
	}
	else if (key == 'b') {
		b += 0.1;
	}
	else if (key == 'B') {
		b -= 0.1;
	}
}

void timer(int value) {
	glutPostRedisplay();
	glutTimerFunc(50, timer, 0);
}



void display(void)
{
	glColor3f(r, g, b);  
	glPointSize(10); 

	glMatrixMode(GL_PROJECTION);
	glLoadIdentity();
	gluOrtho2D(0.0, 640.0, 0.0, 480.0);

	if (check)
	{
		glBegin(GL_POINTS); 
		glVertex2i(x, y);   

		glEnd();
	}
	glFlush();     
}

int main(int argc, char** argv)
{
	glutInit(&argc, argv);
	glutInitWindowSize(640, 480);  
	glutInitWindowPosition(10, 10);
	glutInitDisplayMode(GLUT_SINGLE | GLUT_RGB);
	glutCreateWindow("TUGAS RANCANG ");
	glClearColor(r, g, b, 0); 
	glClear(GL_COLOR_BUFFER_BIT);
	glutKeyboardFunc(myKeyboard);
	glutDisplayFunc(display);
	glutMouseFunc(mouse);
	glutMainLoop();
}

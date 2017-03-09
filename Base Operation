//                                              Specification of Program
//1. Click the left button of the mouse to draw lines, meanwhile, the coordinates will be displayed in the output panel.
     The process will end when you release the button.
//2. Click the right button of the mouse to select the area (rectangle). The area will be hollow when you release the button.
//                                                  ---Tenky Woo---

#include<iostream>
#include<opencv2/opencv.hpp>
#include<windows.h>
using namespace std;
using namespace cv;

#define WINDOW "Image"

Mat image;
Mat imagecopy;
Point pastpoint;
bool p = false;
bool g_draw = false;
Rect g_rect;

void On_mouse(int event, int x, int y, int flags, void*);
void Draw_rect1(Mat img, Rect box);
void Draw_rect2(Mat img, Rect box);

int main()
{
	image = imread("dota.jpg", 3);
	namedWindow(WINDOW, WINDOW_NORMAL);
	imshow(WINDOW, image);
	setMouseCallback(WINDOW, On_mouse, 0);
	
	while (1)
	{
		image.copyTo(imagecopy);
		if(g_draw == true)
		{
			Draw_rect2(imagecopy, g_rect);
			imshow(WINDOW, imagecopy);
		}
		else if (p == true)
		{
			imshow(WINDOW, imagecopy);
		}
		if (waitKey(10) == 27) 
			break;
	}
	return 0;
}

void On_mouse(int event, int x, int y, int flags, void*)
{
	switch (event)
	{
	case EVENT_LBUTTONUP:
	{
		p = false;
		Point pt(x, y);
		line(image,pastpoint , pt, Scalar(0, 0, 225), 2, 8, 0);
		imshow(WINDOW, image);
	}
	break;

	case EVENT_LBUTTONDOWN:
	{
		p = true;
		pastpoint = Point(x, y);
		cout << "The point is at (" << x << "," << y << ")" << endl;
		system("cls");
	}
	break;

	case EVENT_MOUSEMOVE :
	{
		if ((p == true)&&(g_draw == false))
		{
			Point pt(x, y);
			cout << "The point is at (" << x << "," << y << ")" << endl;
			line(image, pastpoint, pt, Scalar(0, 0, 225), 2, 8, 0);
			pastpoint = pt;
			system("cls");
		}
		else if ((p == false) && (g_draw == true))
		{
			g_rect.width = x - g_rect.x;
			g_rect.height = y - g_rect.y;
		}
	}
	 break;

	case EVENT_RBUTTONDOWN:
	{
		g_draw = true;
		g_rect = Rect(x, y, 0, 0);
	}
	break;

	case EVENT_RBUTTONUP:
	{
		g_draw = false;
		Draw_rect1(image, g_rect);
		imshow(WINDOW, image);
	}
	break;
	}
}

void Draw_rect1(Mat img, Rect box)
{
	rectangle(img, box.tl(), box.br(), Scalar(0, 0, 0), -1);
}

void Draw_rect2(Mat img, Rect box)
{
	rectangle(img, box.tl(), box.br(), Scalar(0, 0, 0));
}

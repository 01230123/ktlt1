#define _CRT_SECURE_NO_WARNINGS

#include <stdio.h>
#include <math.h>

#define MAXN 1000
#define MAXPOS 1000
#define inf 1000000000
#define cao_su 0
#define ca_phe 1
#define che 2

#define INPUT "NongTrai.in"
#define OUTPUT "NongTrai.out"

struct point
{
	double x, y;
	point() {}
	point(double _x, double _y)
	{
		x = _x;
		y = _y;
	}
};
struct tree
{
	point pos;
	int type;
};

double Min(double a, double b)
{
	return a < b ? a : b;
}

double Max(double a, double b)
{
	return a > b ? a : b;
}

double Dist(point a, point b)
{
	return sqrt(((a.x - b.x) * (a.x - b.x) + (a.y - b.y) * (a.y - b.y)));
}

double TotalDist(tree a[], int n, point p)
{
	double tmp = 0;
	for (int i = 0; i < n; i++)
		tmp += Dist(p, a[i].pos);
	return tmp;
}

int CountTreeType(tree a[], int n, int Type)
{
	int tmp = 0;
	for (int i = 0; i < n; i++)
	if (a[i].type == Type)
		tmp++;
	return tmp;
}


double FindPerimeter(tree a[], int n)
{
	double left = a[0].pos.x, right = a[0].pos.x;
	double top = a[0].pos.y, bottom = a[0].pos.y;
	for (int i = 1; i < n; i++)
	{
		left = Min(left, a[i].pos.x);
		right = Max(right, a[i].pos.x);
		top = Max(top, a[i].pos.y);
		bottom = Min(bottom, a[i].pos.y);
	}
	return ((right - left) + (top - bottom)) * 2;
}

double CurTotalDist(tree a[], int n, double x)
{
	double left = -MAXPOS, right = MAXPOS, tmp = inf;
	for (int turn = 1; turn <= 50; turn++)
	{
		double y1 = left + (right - left) / 3, y2 = right - (right - left) / 3;
		double tmp1 = TotalDist(a, n, point(x, y1)), tmp2 = TotalDist(a, n, point(x, y2));
		if (tmp1 < tmp2)
		{
			tmp = tmp1;
			right = y2;
		}
		else
		{
			tmp = tmp2;
			left = y1;
		}
	}
	return tmp;
}

double MinTotalDist(tree a[], int n)
{
	double left = -MAXPOS, right = MAXPOS, tmp = inf;
	for (int turn = 1; turn <= 50; turn++)
	{
		double x1 = left + (right - left) / 3, x2 = right - (right - left) / 3;
		double tmp1 = CurTotalDist(a, n, x1), tmp2 = CurTotalDist(a, n, x2);
		if (tmp1 < tmp2)
		{
			tmp = tmp1;
			right = x2;
		}
		else
		{
			tmp = tmp2;
			left = x1;
		}
	}
	return tmp;
}

point FindMedian(tree a[], int n)
{
	double X = 0, Y = 0;
	for (int i = 0; i < n; i++)
	{
		X += a[i].pos.x;
		Y += a[i].pos.y;
	}
	X /= n; Y /= n;
	for (int i = 0; i < n; i++)
	if (X == a[i].pos.x && Y == a[i].pos.y)
	{
		X += 0.1;
		break;
	}
	return point(X, Y);
}

bool ReadFile(tree a[], int &n)
{
	FILE* f = fopen(INPUT, "r");
	if (f == NULL)
		return false;
	fscanf(f, "%d", &n);
	for (int i = 0; i < n; i++)
		fscanf(f, "%lf%lf%d", &a[i].pos.x, &a[i].pos.y, &a[i].type);
	fclose(f);
	return true;
}

void WriteFile(tree a[], int n)
{
	FILE* f = fopen(OUTPUT, "w");
	//First line
	for (int i = 0; i < 3; i++)
	{
		int tmp = CountTreeType(a, n, i);
		fprintf(f, "%d ", tmp);
	}
	fprintf(f, "\n");
	//Second line
	fprintf(f, "%.0lf\n", FindPerimeter(a, n));
	//Last line
	fprintf(f, "%lf", Min(MinTotalDist(a, n), TotalDist(a, n, FindMedian(a, n))));
	fclose(f);
}

int main()
{
	int n = 0;
	tree a[MAXN];
	if (ReadFile(a, n))
		WriteFile(a, n);
	return 0;
}

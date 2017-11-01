#include <vector>
#include <opencv2\opencv.hpp>
#include <iostream>
#include <opencv2\imgproc\types_c.h>  

using namespace std;
using namespace cv;
void sharpen(const Mat &image, Mat &result)
{
	int i, j;
	result.create(image.size(), image.type());
	//抛开第一行和最后一行
	for (j = 1; j<image.rows - 1; j++)
	{
		const uchar* previous = image.ptr<const uchar>(j - 1);
		const uchar* current = image.ptr<const uchar>(j);
		const uchar* next = image.ptr<const uchar>(j + 1);
		uchar* output = result.ptr<uchar>(j);
		for (i = 1; i <image.cols-1; i++)   //抛开第一列和最后一列
		{
			*output++ = saturate_cast<uchar>(5 * current[i] - previous[i] - current[i - 1] - current[i + 1] - next[i]);
		}
	}
	result.row(0).setTo(Scalar(0));   //置0操作
	result.row(result.rows - 1).setTo(Scalar(0));
	result.col(0).setTo(Scalar(0));
	result.col(result.cols - 1).setTo(Scalar(0));
}

int main()
{
	Mat im = imread("picture.jpg");
	Mat out = im;
	sharpen(im, out);
	namedWindow("image");
	imshow("image", out);
	waitKey();
	return 0;
}

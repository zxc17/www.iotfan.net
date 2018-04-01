---
layout: post
title:  "功能测试"
date:   2018-04-01 21:17:00
categories: site
tag: 测试
---
{% highlight %}
#include <windows.h>
#include <stdio.h>
#include <direct.h>
#include <io.h>
int main()
{
	FILE *fp = NULL;
	char file[] = "E:\\diskWakeOn.txt";
	errno_t err;
	int totalTime = 0;
	int thisTime = 0;
	int bootCounter = 0;
	err = fopen_s(&fp, file, "r");
	if (err == 0){
		fscanf_s(fp,"%d\n%d:",&totalTime,&bootCounter);
		fclose(fp);
	}
	bootCounter++;
	totalTime *= 60;
	err = fopen_s(&fp,file,"w");
	if (err != 0)
		exit(0);
	fprintf_s(fp, "%d\n%d:%d", totalTime/60, bootCounter, thisTime/60);
	fclose(fp);

	while (true){
		err = fopen_s(&fp,file,"w");
		if (err != 0)
			exit(0);
		fprintf_s(fp, "%d\n%d:%d", totalTime/60, bootCounter, thisTime/60);
		fclose(fp);
		Sleep(17000);
		thisTime += 17;
		totalTime += 17;
	}
	return 0;
}
```

$$
\begin{align*}
  & \phi(x,y) = \phi \left(\sum_{i=1}^n x_ie_i, \sum_{j=1}^n y_je_j \right)
  = \sum_{i=1}^n \sum_{j=1}^n x_i y_j \phi(e_i, e_j) = \\
  & (x_1, \ldots, x_n) \left( \begin{array}{ccc}
      \phi(e_1, e_1) & \cdots & \phi(e_1, e_n) \\
      \vdots & \ddots & \vdots \\
      \phi(e_n, e_1) & \cdots & \phi(e_n, e_n)
    \end{array} \right)
  \left( \begin{array}{c}
      y_1 \\
      \vdots \\
      y_n
    \end{array} \right)
\end{align*}
$$

![云梦斋主人的微博](/assets/weibo.png)

2018-03-30

云梦斋主人
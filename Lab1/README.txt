***************************************************************************



---------------------
Just use two for loop to do the calculation and then put the result into an array
then call sortResultNA(Point *p[]) to sort the result.
Finally display the result

---------------------------------

void findClosestPair(Point *pointsByX[], Point *pointsByY[],int nPoints)
is a wrapper to call the recursive call findClosestPairDC.

double findClosestPairDC(Point *pointsByX[], Point *pointsByY[], int nPoints, Point *p[])
is used to find the closest pair recursively, p[] is used for collecting the points.

double minLR(double d1, double d2, Point *p1[],Point *p2[],Point *p[]) 
is used to compare minimal distance in left and right part of each division

double minLRS(double dLR, double dS, Point *p3[],Point *p[]) 
is used to compare distance in left and right and strip of each division

double pairDistanceInStrip(Point *YL[], Point *YR[], int nPoints, int mid, double dLR, Point *p[]);
is used to find minimal distance in strip of each division

void sortResultDC(Point *p[]) 
is used for sort the result


***************************************
Please see the excel document named "Compare DC & NA" and "Variation in DC" that I attached.


***************************************
I write a for loop, that make find both closest pair naive and divide and conquer run 10000 times.

Divide and conquer algorithm:

  timer.start();
    
  for (int i = 0; i < 10000 ; i++)
  {
      //////////////////////////////////////////////////////////////////////////
      // DIVIDE AND CONQUER CLOSEST-PAIR ALGORITHM STARTS HERE
      
      // The algorithm expects two arrays containing the same points.
      Point **pointsByX = new Point * [nPoints];
      Point **pointsByY = new Point * [nPoints];
      
      for (int j = 0; j < nPoints; j++)
        {
          pointsByX[j] = points[j];
          pointsByY[j] = points[j];
        }
      
      // NB: you should *not* have to call sort() in your
      // own code!
      sort(pointsByX, pointsByX + nPoints, lessThanX); // sort by x-coord to get X
      sort(pointsByY, pointsByY + nPoints, lessThanY); // sort by y-coord to get Y
      
      findClosestPair(pointsByX, pointsByY, nPoints);
      
      
      delete [] pointsByX;   // free storage from array ptsByX of pt refs
      delete [] pointsByY;   // free storage from array ptsByY of pt refs
      // DIVIDE AND CONQUER CLOSEST-PAIR ALGORITHM ENDS HERE
      //////////////////////////////////////////////////////////////////////////
  }
  timer.stop();

Naive algorithm:

  timer.start();
  
  ///////////////////////////////////////////////////////////////////////
  // NAIVE CLOSEST-PAIR ALGORITHM STARTS HERE
  for (int i = 0; i < 10000 ; i++)
    findClosestPairNaive(points, nPoints);
  
  // NAIVE CLOSEST-PAIR ALGORITHM ENDS HERE
  ///////////////////////////////////////////////////////////////////////
  
  timer.stop();

I tried several different input, I will list the different input and output:

---------------
MacBookAir:lab1_c++ luozheng03$ ./lab1 @2
For n = 2, the divide and conquer time is 3.72 milliseconds
For n = 2, the naive time is 0.209 milliseconds

---------------
MacBookAir:lab1_c++ luozheng03$ ./lab1 @10
For n = 10, the divide and conquer time is 49.975 milliseconds
For n = 10, the naive time is 4.293 milliseconds

---------------
MacBookAir:lab1_c++ luozheng03$ ./lab1 @20
For n = 20, the divide and conquer time is 109.982 milliseconds
For n = 20, the naive time is 20.672 milliseconds

---------------
MacBookAir:lab1_c++ luozheng03$ ./lab1 @40
For n = 40, the divide and conquer time is 261.138 milliseconds
For n = 40, the naive time is 86.572 milliseconds

---------------
MacBookAir:lab1_c++ luozheng03$ ./lab1 @80
For n = 80, the divide and conquer time is 500.572 milliseconds
For n = 80, the naive time is 368.041 milliseconds

---------------
MacBookAir:lab1_c++ luozheng03$ ./lab1 @100
For n = 100, the divide and conquer time is 624.277 milliseconds
For n = 100, the naive time is 580.599 milliseconds

---------------
MacBookAir:lab1_c++ luozheng03$ ./lab1 @110
For n = 110, the divide and conquer time is 708.895 milliseconds
For n = 110, the naive time is 706.775 milliseconds

---------------
MacBookAir:lab1_c++ luozheng03$ ./lab1 @115
For n = 115, the divide and conquer time is 724.47 milliseconds
For n = 115, the naive time is 773.216 milliseconds

---------------
MacBookAir:lab1_c++ luozheng03$ ./lab1 @120
For n = 120, the divide and conquer time is 760.493 milliseconds
For n = 120, the naive time is 866.534 milliseconds

---------------
At about n = 110 random points, the divide and conquer algorithm running time is equal to the naive algorithm running time.
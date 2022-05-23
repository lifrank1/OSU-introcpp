/*
  File: grades.cpp
  Created by: Frank Li
  Creation Date: April 8 2022
  Synopsis: Printing COVID data in a formatted table
*/

#include <iostream>
#include <cmath>
#include <iomanip>

using namespace std;

// FUNCTION PROTOTYPES GO HERE:

const int MAXCOVIDCOUNT = 15; 

int getCovidCounts(int array[], int year);
void printTop();
void calcStats(int year, int array[], int numCovidCounts, int & min, int & max);
void computeStats(int array[], int numCovidCounts, double & average, int & min, int & max); //next 4 are all helpers for calcStats
double computeNumOutliersAndSD(int array[], int numCovidCounts, double average, int & numOutliers);
void outputCounts(int array[], int numCovidCounts);
void outputOutliers(int array[], int numCovidCounts, double & average, double & SD, int & numOutliers);
void outputHighest(int lowestCount, int highestCount, int lowestCount1, int highestCount2);


int main() {
   int year1[MAXCOVIDCOUNT];
   int year2[MAXCOVIDCOUNT];
   int input = 0;
   int min(10000), max(-10000), min1(10000), max1(-100000); 
   
   cout.precision(2);
   cout.setf(ios::fixed);
   
   for(int i = 0; i < MAXCOVIDCOUNT; i++) {
      year1[i] = 0;
      year2[i] = 0;
   }
   
   //fill up year 1 array 
   int covidCountsYear1 = getCovidCounts(year1, 1);
   cout << "Enter the " << covidCountsYear1 << " COVID count number(s): "; 
   
   for (int i = 0; i < covidCountsYear1; i++) {
       cin >> input;
       year1[i] = input; 
   }
    
   //fill up year 2 array
   int covidCountsYear2 = getCovidCounts(year2, 2);
   cout << "Enter the " << covidCountsYear2 << " COVID count number(s): ";
   
   for (int i = 0; i < covidCountsYear2; i++) {
      cin >> input;
      year2[i] = input;
   }
   
   printTop();
   
      
   calcStats(1, year1, covidCountsYear1, min, max); 

   calcStats(2, year2, covidCountsYear2, min1, max1);
   outputHighest(min, max, min1, max1);
   
	
	return 0;
}



// FUNCTION DEFINITIONS GO HERE:
int getCovidCounts(int array[], int year) {
   int numCovidCounts = 0;
   int input = 0;
   cout << "Enter # of COVID counts recorded during year " << year << ": "; 
   cin >> input;
   while (input < 1 || input > 15) {
      cout << "Enter at least one but no more than 15 counts taken. Try again." << endl;
      cout << "Enter # of COVID counts recorded during year " << year << ": "; 
      cin >> input;
   }
   numCovidCounts = input; 
   
   return numCovidCounts; 
}

void printTop() {
   cout << "\nYear    Avg  Stddev   COVID Counts" << endl; 
   cout << "----------------------------------" << endl;
}




void calcStats(int year, int array[], int numCovidCounts, int & min, int & max) {
   cout.precision(1);
   cout.setf(ios::fixed);
   
   double average = 0;
   int numOutliers = 0;
   double standardDev = 0;
   
   computeStats(array, numCovidCounts, average, min, max);
   standardDev = computeNumOutliersAndSD(array, numCovidCounts, average, numOutliers);
   
   cout << "  " << year << setw(8) << average << setw(8) << setprecision(2) << standardDev << "   ";
   
   outputCounts(array, numCovidCounts);
   outputOutliers(array, numCovidCounts, average, standardDev, numOutliers);
   
}


void computeStats(int array[], int numCovidCounts, double & average, int & min, int & max) {
   int sum = 0;
   for (int i = 0; i < numCovidCounts; i++) {
      sum += array[i];
      if (array[i] < min) {
         min = array[i];
      }
      if (array[i] > max) {
         max = array[i];
      }
   }
   average = (sum + 0.0) / numCovidCounts; 
   
}




double computeNumOutliersAndSD(int array[], int numCovidCounts, double average, int & numOutliers) {
   double SD = 0;
   
   for (int i = 0; i < numCovidCounts; i++) {
      SD += pow(array[i] - average, 2); 
   }
   SD = sqrt(SD / numCovidCounts); 
   
   for (int i = 0; i < numCovidCounts; i++) {
      if (abs(array[i] - average) > SD) {
         numOutliers++; 
      }
   }
   
   return SD;
}


void outputCounts(int array[], int numCovidCounts) {
   cout << "{ ";
   for (int i = 0; i < numCovidCounts-1; i++) {
      cout << array[i] << ", ";
      
   }
   cout << array[numCovidCounts-1] << " }" << endl;
}


void outputOutliers(int array[], int numCovidCounts, double & average, double & SD, int & numOutliers){
   if (numOutliers > 0) {
   cout << "Outliers: < ";
   for (int i = 0; i < numCovidCounts; i++) {
      if (abs(array[i] - average) > SD) {
         cout << array[i];
         numOutliers--;
         if (numOutliers > 0) {
            cout << ", ";
         }
      }
   }
   cout << " >" << endl;
   }
   else {
      cout << "No outliers" << endl;
   }
}

void outputHighest(int lowestCount, int highestCount, int lowestCount1, int highestCount2) {
   if (highestCount > highestCount2) {
      cout << "\nThe first year had the highest count of " << highestCount << "." << endl; 
   }
   else if (highestCount < highestCount2) {
      cout << "\nThe second year had the highest count of " << highestCount2 << "." << endl; 
   }
   else {
      cout << "\nBoth years had the highest count of " << highestCount << "." << endl;
   }
   cout << "\nThe first year's lowest count is " << lowestCount << ".";
   cout << "\nThe second year's lowest count is " << lowestCount1 << "." << endl;
   
}



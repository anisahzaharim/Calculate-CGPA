# Calculate-CGPA
Program to calculate CGPA
by NUR ANISAH

#include <iostream>
#include <iomanip>
#include <string> // to manipulate string and array
#include <ctime>
#include <fstream> // for file 
#include <windows.h> // for sleep //loading bar
#include <conio.h> // console input and output 
#include <dos.h> // to produce beep sound 
using namespace std;
 
// declare global 
int sem [60]; // function check display
string course [60];
string grade[60];
int unit[60];

int z; // function validity
int sem2[60],grade2[60],unit2[60]; 
int q=0; 
int g=0;
int u=0;

void menu(); // function prototype 
int readData (int&, string&, int[], string[], int[], string[] ); // function prototype // ampersand to pass reference to function transcript
void displayData(int , int[],string[], int[], string[], float[], float[] ); // function prototype
void calc(int,int[],float[], int[], float[],float,float,float,float,float,float,float,float, float, float, // function prototype
          float,float,float,float,float,float,float,float,float, float, float, float,float,float, float);
void transcript (int, string, int[], string[], int[], string[]); //function prototype
void validity (int[],int[],string[],int); //function type
void checkdisplay (); // function prototype


int main()
{
  
  int choice;
  int s=0; // subject course (will hold value of i)
  int id;
  string name;
  int sem [30];
  string course [30];
  int unit[30];
  string grade[30];
  float gradepoint[30];
  float totalgp[30];
  float sumtotalgp_1 = 0 , sumtotalgp_2 = 0 ,sumtotalgp_3 = 0 ,sumtotalgp_4 = 0 ,sumtotalgp_5 = 0 ,sumtotalgp_6 = 0 ,sumtotalgp_7 = 0 ,sumtotalgp_8 = 0;
  float sumunit_1 = 0 , sumunit_2 = 0 ,sumunit_3 = 0 ,sumunit_4 = 0 ,sumunit_5 = 0 ,sumunit_6 = 0 ,sumunit_7 = 0 ,sumunit_8 = 0;
  float gpa1 = 0, gpa2 = 0,gpa3 = 0 ,gpa4 = 0,gpa5 = 0,gpa6 = 0,gpa7 = 0 ,gpa8 = 0, cgpa=0;
  
  int i=0;                                               
  bool proceed = true;
  do{
  
  
	menu(); // choose menu
	cin>>choice; // input menu
	switch(choice) {
		case 1 : // read data
		system("cls"); 
		    s = readData (id,name, sem, course,unit, grade); // function call
		system("PAUSE"); 
		    break;
		case 2: // display data
		system("cls");
		      displayData(s, sem,course,unit, grade, gradepoint,  totalgp ); // function call
		system("PAUSE"); 
		      break;
		case 3: // calc cgpa and gpa
		system("cls");
		     calc(s,unit,gradepoint,sem,totalgp,sumtotalgp_1,sumtotalgp_2,sumtotalgp_3,sumtotalgp_4,sumtotalgp_5,sumtotalgp_6,
             sumtotalgp_7,sumtotalgp_8,sumunit_1,sumunit_2,sumunit_3,sumunit_4,sumunit_5,
			 sumunit_6,sumunit_7,sumunit_8,gpa1, gpa2,gpa3,gpa4,gpa5,gpa6,gpa7,gpa8, cgpa); // function call
		system("PAUSE"); 
		     break;
		case 4: // show transcript 
		system("cls");
		     transcript(id,name,sem,course,unit,grade); // function call
		     displayData(s, sem,course,unit, grade, gradepoint,  totalgp ); // function call
		     calc(s,unit,gradepoint,sem,totalgp,sumtotalgp_1,sumtotalgp_2,sumtotalgp_3,sumtotalgp_4,sumtotalgp_5,sumtotalgp_6, 
             sumtotalgp_7,sumtotalgp_8,sumunit_1,sumunit_2,sumunit_3,sumunit_4,sumunit_5,sumunit_6,
			 sumunit_7,sumunit_8,gpa1,gpa2,gpa3,gpa4,gpa5,gpa6,gpa7,gpa8, cgpa);
		     	system("PAUSE"); 
	    	break;
		case 5: 
		      proceed=false; // exit 
		      exit(1);
			  break;
		default : cout << "INVALID. YOUR CHOICE IS NOT AVAILABLE.  \n";
		
	}
}while(proceed==true);

return 0;
}

void menu () { // function definition
system("cls");
cout << endl << endl;
cout << "           STUDENT'S GRADING SYSTEM" << endl;
  cout << "           BY : NUR ANISAH ZAHARIM"  << endl;
  cout << "               GROUP : B (Z2)" ;
cout << endl << endl ;
cout << "      ================MAIN MENU=============" << endl;
cout << "      --------------------------------------" << endl;
cout << "       1. Read data \n" ;
cout << "      --------------------------------------" << endl;
cout << "       2. Display Data \n" ;
cout << "      --------------------------------------" << endl;
cout << "       3. Calculate GPA & CGPA \n" ;
cout << "      --------------------------------------" << endl;
cout << "       4. Show transcript \n" ;
cout << "      --------------------------------------" << endl;
cout << "       5. Exit \n";
cout << "      --------------------------------------" << endl;

cout << "    Enter your choice : ";
}

int readData (int& id, string& name, int sem[], string course[], int unit[], string grade[]) // function definition
{

	cout << endl;
	/////////////////////////////////////////////////////////////////
    cout<<"\n\n\n\t\t\t\tPlease wait while loading\n\n";
   char a=177, b=219;
   cout<<"\t\t\t\t";
   for (int i=0;i<=25;i++)
   cout<<a;
   cout<<"\r";  
   cout<<"\t\t\t\t";
   for (int i=0;i<=25;i++)     // Loading bar
 {
  cout<<b;
  for (int j=0;j<=1e8;j++); 
 }
   Beep(700,800); // beep sound 
   cin.get();
   ////////////////////////////////////////////////////////////////////
	cout << endl << endl <<  "       YOUR DATA HAS BEEN DONE READ. \n";
	int i=0;
	ifstream dataStud; 
	dataStud.open("dataStud.txt"); // read data
	while (!dataStud.eof()){ // read until end of file
		dataStud >> id; // call the id in file
		getline(dataStud, name);  // call the  whole line
		cout << endl << endl;                                                                    
		cout << "         Name   : " << name << endl ;
		cout << "         Matric : " << id << endl << endl;
	
		while (dataStud>>sem[i]>>course[i]>>unit[i]>>grade[i]) // store to array 
		{
			validity(sem,unit,grade,i); // function call (check validity)
			++i; 
		}
		checkdisplay(); //function call
		
	} // end of while

	
	return i;
	
}

void validity(int sem[],int unit[],string grade[],int z) //function definition
// pass the array 
{
	
	 
    if(sem[z]<=0 || sem[z]>8 ) // check if sem greater than 8
    {
        sem2[q]=z;
        ++q; // q = 1
		
    }

    if(unit[z]<=0) // check if unit less than zero
    {
        sem2[u]=z;
        ++u; // u = 1
		
    }

    if(grade[z]!="A" && grade[z]!="A-" && grade[z]!="B+" && grade[z]!="B" &&
            grade[z]!="B-" && grade[z]!="C+" && grade[z]!="C" && grade[z]!="C-" &&
            grade[z]!="D+" && grade[z]!="D" && grade[z]!="D-" && grade[z]!="F") // check if the grade exceed
    {
        grade2[g]=z;
        ++g; // g = 1
		
    }

}

void checkdisplay() // display message if data not valid 
{

    if(q!=0) 
    {
        cout<<" Invalid semester." ;
        cout<<" Please change your semester." << endl;
    }
    if(u!=0)
    {
        cout<<" Invalid unit of subject.";
        cout<<" Please change your unit of subject." << endl;
    }
    if(g!=0)
    {
        cout<<" Invalid grade.";
        cout<<" Please change your grade." << endl;
    }

    if(q!=0 || u!=0 || g!=0) // terminate the program
    {
        exit(1);
    } 

}
void displayData(int s, int sem[],string course[], int unit[], string grade[], float gradepoint[], float totalgp[] ) // function definition
{

    for (int i=0 ; i<s ; i++)
    {
        if(grade[i]=="A") 
 	   		gradepoint[i] = 4;
 	   		
 	   	else if(grade[i]=="A-")
 	   		gradepoint[i] = 3.67;
 	
 	   	else if (grade[i]=="B+")
 	   		gradepoint[i] = 3.33;
 	   	
 	   	else if(grade[i]=="B")
 	   			gradepoint[i] = 3;
 	   	
 	   	else if(grade[i]=="B-")
 	   			gradepoint[i] = 2.67;
 	   	
 	   	else if(grade[i]=="C+")
 	   			gradepoint[i] = 2.33;
 	   		
 	   	else if(grade[i]=="C")
 	   			gradepoint[i] = 2;
 	   		
 	   	else if(grade[i]=="C-")
 	   			gradepoint[i] = 1.67;
 	   		
 	   	else if(grade[i]=="D+")
 	   		gradepoint[i] = 1.33;
 	   		
 	   	else if(grade[i]=="D")
 	   			gradepoint[i] = 1;
 	   		
 	   	else if(grade[i]=="D-")
 	   			gradepoint[i] = 0.67;
 	   	
 	   	else if (grade[i]=="F")
 	   			gradepoint[i] = 0;
 	   	else 
			cout << endl;
 	   }
 	   for (int i=0;i < s;i++)
 	   {
 	   	totalgp[i]= gradepoint[i]*unit[i]; // calculate total grade point
		}
	cout << endl << endl;
	cout << "  -------------------------------------------------------------------------------" << endl;
	cout << "  SEMESTER  " << "    COURSE  " <<   " CREDIT\t" <<  "  GRADE"  <<    "    GRADE POINT\t" << "    TOTAL GRADE POINT "<< endl;
	cout << "  -------------------------------------------------------------------------------" << endl;
	cout << endl;
	for (int i=0;i < s;i++)
	{
		cout << fixed << showpoint << setprecision(2); // set to 2 d.p
		cout << "     " << sem[i] << "\t\t" << course[i] << "\t   " << unit[i] << "\t    " << grade[i] << "\t      " << gradepoint[i]<< "\t        " << totalgp[i] << endl;
	} // output the data
	
}

void calc(int s,int unit[],float gradepoint[], int sem[], float totalgp[],float sumtotalgp_1,float sumtotalgp_2,
float sumtotalgp_3,float sumtotalgp_4,float sumtotalgp_5,float sumtotalgp_6, float sumtotalgp_7,float sumtotalgp_8,
float sumunit_1, float sumunit_2, float sumunit_3, float sumunit_4, float sumunit_5,
float sumunit_6,float sumunit_7, float sumunit_8, float gpa1, float gpa2, float gpa3, 
float gpa4, float gpa5, float gpa6, float gpa7, float gpa8,float cgpa) {

	for (int i=0; i < s; i++)
	{
	
if (sem[i]==1) // sem 1
{
  sumtotalgp_1 = sumtotalgp_1 + totalgp[i];	// calculate sum of totalgp
  sumunit_1 = sumunit_1 + unit[i]; // calculate sum of credit
  gpa1 = sumtotalgp_1 / sumunit_1; // calculate gpa
}
else if (sem[i]==2) // sem 2
{
  sumtotalgp_2 = sumtotalgp_2 + totalgp[i];	
  sumunit_2 = sumunit_2 + unit[i];
  gpa2 = sumtotalgp_2 / sumunit_2; 
} 
else if (sem[i]==3) // sem 3
{
  sumtotalgp_3 = sumtotalgp_3 + totalgp[i];
  sumunit_3 = sumunit_3 + unit[i];
  gpa3 = sumtotalgp_3 / sumunit_3; 	
} 
else if (sem[i]==4) // sem 4
{
  sumtotalgp_4 = sumtotalgp_4 + totalgp[i];	
  sumunit_4 = sumunit_4 + unit[i];
  gpa4 = sumtotalgp_4 / sumunit_4;
} 
else if (sem[i]==5) // sem 5
{
  sumtotalgp_5 = sumtotalgp_5 + totalgp[i];	
  sumunit_5 = sumunit_5 + unit[i];
  gpa5 = sumtotalgp_5 / sumunit_5;
} 
else if (sem[i]==6) // sem 6
{
  sumtotalgp_6 = sumtotalgp_6 + totalgp[i];
  sumunit_6 = sumunit_6 + unit[i];
  gpa6 = sumtotalgp_6 / sumunit_6;	
} 
else if (sem[i]==7) // sem 7
{
  sumtotalgp_7 = sumtotalgp_7 + totalgp[i];
  sumunit_7 = sumunit_7 + unit[i];
  gpa7 = sumtotalgp_7 / sumunit_7;	
} 
else if (sem[i]==8)  // sem 8
{
  sumtotalgp_8 = sumtotalgp_8 + totalgp[i];	
  sumunit_8 = sumunit_8 + unit[i];
  gpa8 = sumtotalgp_8 / sumunit_8;
} 

} //end of for
cout << endl << endl;
 cout <<  "\n     ******************GPA********************** " << endl << endl;
cout << "        SEMESTER 1  :" << "\t"<< gpa1 <<endl; // output gpa
cout << "   ----------------------------------------------" << endl;
cout << "        SEMESTER 2  :" << "\t"<< gpa2 <<endl;
cout << "   ----------------------------------------------" << endl;
cout << "        SEMESTER 3  :" << "\t"<< gpa3 <<endl;
cout << "   ----------------------------------------------" << endl;
cout << "        SEMESTER 4  :" << "\t"<< gpa4 <<endl;
cout << "   ----------------------------------------------" << endl;
cout << "        SEMESTER 5  :" << "\t"<< gpa5 <<endl;
cout << "   ----------------------------------------------" << endl;
cout << "        SEMESTER 6  :" << "\t"<< gpa6 <<endl;
cout << "   ----------------------------------------------" << endl;
cout << "        SEMESTER 7  :" << "\t"<< gpa7 <<endl;
cout << "   ----------------------------------------------" << endl;
cout << "        SEMESTER 8  :" << "\t"<< gpa8 << endl;
cout << "   ----------------------------------------------" << endl<<endl;

cgpa = (sumtotalgp_1 + sumtotalgp_2 + sumtotalgp_3 + sumtotalgp_4 + sumtotalgp_5 + sumtotalgp_6 + sumtotalgp_7 + sumtotalgp_8) // calculate cgpa
        / (sumunit_1+ sumunit_2+ sumunit_3+ sumunit_4+ sumunit_5+ sumunit_6+ sumunit_7+ sumunit_8);
 
if (cgpa <=4.00 && cgpa >=3.75) // check cgpa
{
cout << "  ----------------------------------------------" << endl;
cout << "        STATUS  :  EXCELLENT " << endl;
cout << "  ----------------------------------------------" << endl;

}
else if (cgpa <= 3.74 && cgpa >= 3.25)
{
cout << "  ----------------------------------------------" << endl;
cout << "        STATUS  : VERY GOOD" << endl;
cout << "  ----------------------------------------------" << endl;
}

else if  (cgpa <= 3.24 && cgpa >= 2.75)
{
cout << "  ----------------------------------------------" << endl;
cout << "        STATUS  : GOOD " << endl;
cout << "  ----------------------------------------------" << endl;

}
else if  (cgpa <= 2.74 && cgpa >= 2.25)
{
cout << "  ----------------------------------------------" << endl;
cout << "        STATUS  : WORK SMART" << endl;
cout << "  ----------------------------------------------" << endl;
}
else if (cgpa <= 2.24 )
{
cout << "  ----------------------------------------------" << endl;
cout << "        STATUS  :  WORK HARDER " << endl ;
cout << "  ----------------------------------------------" << endl;
}
cout << " ----------------------------------------------" << endl;
cout << "         CGPA : "<< cgpa <<endl << endl;
cout << " ----------------------------------------------" << endl;


}

void transcript (int id, string name, int sem[], string course[], int unit[], string grade[] ) // function definition
{
  
  
	
	cout << endl << "                                      Student Academic Record" << endl; 
    cout<<  "  ____________________________________________________________________________________________________________________________" << endl;
    cout << "                                                                                                                                  " << endl;
    cout << "  Student Information                                                                                                             " << endl;
    cout << "                                                                                                                                  " << endl;
    cout << "   Name       :" <<  name                               << "                      Matric No : " << id  << "                       "<< endl;
    cout << "   School     : SCHOOL OF COMPUTER SCIENCE                                                                                        " << endl;
    cout << "   Program    : COMPUTER SCIENCE                                                                                                  "<< endl;
    cout << "                                                                                                                                  "<< endl;
    cout << "                                                                                                                                  "<< endl;
    cout << " ____________________________________________________________________________________________________________________________" << endl; 
		     
   
}

# string-to-integer
// Course:  CS213 - Programming II  - 2018
// Title:   Assignment I - Individual
// source:  Problem 16 on page 505 from Problem Solving with C++, ninth edition.
// Purpose:  read data from text file & converting strings to integers
// Author: shrouq hussein        
// Version: 2
#include <iostream>
#include <fstream>
#include <vector>
#include <sstream>
using namespace std;


  int main()
  {
   std::ifstream infile ("racers data.txt");
   string line;
   vector <string>data;

    if (infile.good()) {      /// Check if file exists and then open it and read it’s content line by line and add it to a vector.
        while (getline(infile,line)){
            data.push_back(line);
        }
       infile.close(); /// Close the file.
    }
     else {
        cout << "Error!";
        return 0 ;
    }

///converting digits to int
       vector<int> values;
       int n;
       for (int i = 0; i < data.size();i++){
       stringstream stream(data[i]);
       while( stream >>n ){
        char c = stream.get();
        values.push_back(n);
        cout<<n<<" ";
     }
     cout<<endl;
        }
  ///_________________________

    int arr0[15];
    int arr1[15];
    int arr2[15];
    int num,place;
    double time0=0.0;
    double time1=0.0;
    double time2=0.0;
    double mile=0.0;
    double split_time=0.0;
    double time2racer1;
    double max_time=0.0;

  /// distribute data into 3 arrays,array for each sensor

   cout<<"Enter racer's number 100 or 132  or 182: "<<endl;
   cin>>num;
   if((num==100)||(num==132)||(num==182)){

   for (int i = 3; i < 18;i++){
            arr0[i]=values[i];
            if(num==arr0[i]){
                time0=(values[i+1]*60.0)+values[i+2]+(values[i+3]/60.0);
                 cout<<"time recorded by sensor 0 :"<<time0<<endl;
                 cout<<endl<<endl;
            }

     }


    for (int i = 18; i < 33;i++){
            arr1[i]=values[i];
             if(num==arr1[i]){
                mile=7.0;
                time1=(values[i+1]*60.0)+values[i+2]+(values[i+3]/60.0);
                split_time=(time1-time0)/mile;
              cout<<"time  recorded by sensor 1: "<<time1<<endl;
              cout<<"Split time between sensor 0 & sensor 1 is = "<<split_time<<"  minutes/mile"<<endl;
              cout<<endl<<endl;

            }

     }


    for (int i = 34; i < 48;i+=5){
            arr2[i]=values[i];
           if(num==arr2[i]){
                mile=13.1;
                time2=(values[i+1]*60.0)+values[i+2]+(values[i+3]/60.0);
                split_time=(time2-time1)/mile;
              cout<<"time  recorded by sensor 2: "<<time2<<endl;
              cout<<"Split time between sensor 1 & sensor 2 is = "<<split_time<<" minutes/mile"<<endl;
             cout<<"overall time is= "<<(time2-time0)<< " minutes"<<endl;
             cout<<"overall race pace is= "<< mile/(time2-time0)<< "  mile/minutes"<<endl<<endl;
            }

          else{
            time2racer1=(values[i+1]*60.0)+values[i+2]+(values[i+3]/60.0);
                 if(time2>max_time){
                     place=2;
                  }
                 else{
                     place=1;
                      }
                 if((time2racer1>max_time)){
                      max_time= time2racer1;
                      }
             }
     }
    if(time2>max_time){
           place=3;

          }

    cout<< "The racer’s place is : "<<place<<endl;

   }

    else{
    cout<<"There is no racer with this number"<<endl;
    return 0;
    }
    return 0;
    }

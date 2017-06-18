//
//  main.cpp
//  Project Final
//
//  Created by iMac on 31.05.17.
//  Copyright © 2017 Project Final. All rights reserved.
//

#include <iostream>
#include <stdlib.h>

struct AirPlane
{
    char* name;
    char* Number;
    char* MaxSpeed;
    int pasangersCapacity;
};

struct Coordinates
{
    char* city;
    int x;
    int y;
};

struct Plane_Route
{
    
    struct Time
    {
        int day : 3;
        int month: 2;
        int year: 16;
        int hour : 3;
        int min : 4;
        int sec : 4;
    };
    
    Time * date;
    Coordinates Start;
    Coordinates End;
    AirPlane plane;
};


void ShowPlaneInformation (AirPlane * flot ,size_t flotSize)
{
    for (size_t i=0;i<flotSize;++i)
    {
        std::cout<<"PLANE № "<<1+i<<std::endl;
        std::cout<<std::endl;
        std::cout<<"FLOT....."<<" [ "<<flot[i].name<<" ] "<<std::endl;
        std::cout<<"NUMBER..."<<" [ "<<flot[i].Number<<" ] "<<std::endl;
        std::cout<<"MAXSPEED."<<" [ "<<flot[i].MaxSpeed<<" ] "<<std::endl;
        std::cout<<"PASANGERS"<<" [ "<<flot[i].pasangersCapacity<<" ] "<<std::endl;
        
    }
    
    std::cin.get();

}
void ShowRoutesInformation (Plane_Route * route,size_t flotSize)
{
    for (int i=0;i<flotSize;++i)
    {
    
        std::cout<<std::endl;
        std::cout<<"Start City "<<" [ "<<route[i].Start.city<<" ] "<<"||||    The end of route City "<<" [ "<<route[i].End.city<<" ] "<<std::endl;
        std::cout<<std::endl;
        std::cout<<std::endl;
        std::cout<<"Point Start  - "<<1+i<<" Coordinates ="<<" [ "<<route[i].Start.x<<" ] "<<" [ "<<route[i].Start.y<<" ] "<<std::endl;
        std::cout<<"Point Finish - "<<1+i<<" Coordinates ="<<" [ "<<route[i].End.x  <<" ] "<<" [ "<<route[i].End.y  <<" ] "<<std::endl;
        std::cout<<std::endl;
        std::cout<<std::endl;
        /*
        std::cout<<"DAY "<<" [ "<<route[i].date->day<<" ] "<<std::endl;
        std::cout<<"MOUNTH "<<" [ "<<route[i].date->month<<" ] "<<std::endl;
        std::cout<<"YEAR "<<" [ "<<route[i].date->year<<" ] "<<std::endl;
        std::cout<<"HOUR "<<" [ "<<route[i].date->hour<<" ] "<<std::endl;
        std::cout<<"MINUTES "<<" [ "<<route[i].date->min<<" ] "<<std::endl;
        std::cout<<"SECOND "<<" [ "<<route[i].date->sec<<" ] "<<std::endl;
         */
        
        std::cout<<"Name plane--"<<route->plane.name<<std::endl;
        std::cout<<"Number plane--"<<route->plane.Number<<std::endl;
        std::cout<<"MaxSpeed--"<<route->plane.MaxSpeed<<std::endl;
        std::cout<<"Pasangers--"<<route->plane.pasangersCapacity<<std::endl;
        
        std::cout<<"....................................................................................."<<std::endl;
    }
    std::cin.get();
}

void FillPlaneInformation (AirPlane * flot)
{
    char buff[50] = {0};
    std::cout << "Enter airplane name: ";
    std::cin.get();
    std::cin.getline(buff, 50);
    flot->name = new char[strlen(buff)];
    strcpy(flot->name, buff);
    
    
        
    std::cout<<"Enter airplane Number № ";
        
    memset(buff, 0, 50); // удаление старого buff
    std::cin.getline(buff,50);
    flot->Number=new char [strlen(buff)];
    strcpy(flot->Number, buff);

   
    
    
    // Скорость
    std::cout<<"Enter airplane Max Speed  ";
    memset(buff, 0, 50); // удаление старого buff
    std::cin.getline(buff,50);
    flot->MaxSpeed=new char [strlen(buff)];
    strcpy(flot->MaxSpeed, buff);
    
    std::cout<<"Enter airplane Max Pasangers  ";
    std::cin>>flot->pasangersCapacity;
}

bool IsPlaneBusy(const Plane_Route * const route, const AirPlane& flot)
{
    return false;
}


void Fill_Route_Information (Plane_Route * route, AirPlane* flot, size_t flotSize)
{
    
    char buff[50] = {0};
    std::cout << "Enter route start city...";
    std::cin.get();
    std::cin.getline(buff, 50);
    route->Start.city = new char[strlen(buff)];
    strcpy(route->Start.city, buff);
    
    
    std::cout<<"Enter route End city...";
    memset(buff, 0, 50);
    std::cin.getline(buff, 50);
    route->End.city=new char [strlen(buff)];
    strcpy(route->End.city, buff);
    std::cout<<"Coordinates Start.x"<<std::endl;
    std::cin>>route->Start.x;
    std::cout<<"Coordinates Start.y"<<std::endl;
    std::cin>>route->Start.y;
    std::cout<<"Coordinates End.x"<<std::endl;
    std::cin>>route->End.x;
    std::cout<<"Coordinates End.y"<<std::endl;
    std::cin>>route->End.y;
    
    
    do
    {
        std::cout<<"Choose AirPlane (press 2 for show flot information and any key for continue) : "<<std::endl;
        int a=0;
        std::cin>>a;
        if (a==2)
            {
                ShowPlaneInformation(flot, flotSize);
            }
        std::cout << "Enter plane number: ";
        int planeNum = 0;
        std::cin>>planeNum;
        if(planeNum > flotSize)
            {
        std::cout << "This is plane number is wrong (out of range)\n";
        continue;
            }
        if(IsPlaneBusy(route, flot[planeNum-1]))
            {
        std::cout << "Current plane is busy\n";
        continue;
            }
        memcpy(&route->plane, &flot[planeNum-1], sizeof(AirPlane));
        break;
            }
        while (true);
    /*
    route->date->day=arc4random()%31;
    route->date->month=arc4random()%12;
    route->date->year=1988+arc4random()%2017;
    route->date->hour=arc4random()%24;
    route->date->min=arc4random()%59;
    route->date->sec=arc4random()%59;
     */
}




int main()
{
  
    srand((time_t)NULL);
    size_t flotSize = 0;

    AirPlane* flot = NULL;
    Plane_Route* route = NULL;
    //Plane_Route* routes;
    
    int action = 0;

    while(action != 5)
    {
        std::cout
        << "Press 1 for add ariplane information\n"
        << "Press 2 for show airplane information\n"
        << "Press 3 for add Route\n"
        << "Press 4 show routes information\n"
        << "Press 5 for exit\n";
        std::cin >> action;
        
        switch(action)
        {
            case 1 :
            {
                if(flot == NULL)
                {
      //Название самолета
                    flot = new AirPlane();
                    FillPlaneInformation(flot);
                    flotSize++;
                }
                else
                {
                    flotSize++;
                    AirPlane* temp = new AirPlane[flotSize];
                    memcpy(temp, flot, (flotSize-1)*sizeof(AirPlane));
                    delete[] flot;
                    FillPlaneInformation(&temp[flotSize-1]);
                    flot = temp;
                }
            }
                break;
                
                
                
      // На ЭКРАН
            case 2 :
            {
                ShowPlaneInformation(flot,flotSize);
            }
                break;
        
      // Информация по маршруту
                
            case 3 :
            {
                if(route == NULL)
                {
      // Город
                    route = new Plane_Route();
                    Fill_Route_Information(route, flot, flotSize);
        
      //Время
                    flotSize++;
            
                }
                else // есть хотябы один маршрут
                {
      // Город
                    flotSize++;
                    Plane_Route* temp = new Plane_Route[flotSize];
                    memcpy(temp, route, (flotSize-1)*sizeof(Plane_Route));
                    delete [] route;
                    Fill_Route_Information(&temp[flotSize-1], flot, flotSize);
                    route=temp;
                }
            }
                break;
                
            case 4:
        {
            ShowRoutesInformation(route, flotSize);
        }
            break;
                
    default:
            {
                std::cout << "Wrong command\n";
            }
        }
    }
}

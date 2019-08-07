#include<stdio.h>
#include<conio.h>
#include<stdlib.h>
#include<graphics.h>
int xpoint,ypoint;
#define up 72
#define down 80
#define right 77
#define left 75

void intro(void)
{ //setbkcolor(3);
  gotoxy(35,13);
  printf("Welcome to Snake");
  gotoxy(56,24);
  printf("Developed by Rahul Verma");
  delay(1000);
}


void point(int x,int y)    //draws the point at (x,y) posi on the screen
{
  setfillstyle(1,x/14);
   circle(x,y,5);
   floodfill(x,y,1); //0 because setcolor(0);
}


void end(void)
{
  delay(1000);
  gotoxy(35,24);
  printf("You collide!");
  delay(1000);
  cleardevice();
  gotoxy(35,13);
  printf("Thankyou for playing");
}


void block(int x,int y)
{
  rectangle(x-5,y-5,x+5,y+5);
}


void body(int x,int y)
{
 extern int input,length,i,a,cordix[200],cordiy[200];

   if(input==right)
   { arc(x-5,y,270,90,5);
     circle(x-4,y-1,1);
     circle(x-4,y+1,1);
     line(x,y,x+2,y);         // toung
     line(x+2,y,x+3,y-1);
     line(x+2,y,x+3,y+1);
   }
    else
    if(input==left)
   { arc(x+5,y,90,270,5);
     circle(x+4,y-1,1);
     circle(x+4,y+1,1);
     line(x,y,x-2,y);          //toung
     line(x-2,y,x-3,y-1);
     line(x-2,y,x-3,y+1);
     }
    else
    if(input==up)
    {arc(x,y+5,0,180,5);
     circle(x-1,y+4,1);
     circle(x+1,y+4,1);
     line(x,y,x,y-2);         //toung
     line(x,y-2,x+1,y-3);
     line(x,y-2,x-1,y-3);
     }
    else
    if(input==down)
    {arc(x,y-5,180,360,5);
     circle(x-1,y-4,1);
     circle(x+1,y-4,1);
     line(x,y,x,y+2);       //toung
     line(x,y+2,x+1,y+3);
     line(x,y+2,x-1,y+3);
     }

    for(i=1;i<=length;i++)
     {   setfillstyle(1,5);
       block(cordix[i],cordiy[i]);
       floodfill(cordix[i],cordiy[i],1);
     }

}


void boundry(void)
{
   rectangle(10,20,630,470);

}

void stopask(void)
{  //int poli[8]={200,100,470,100,470,200,200,200};
  char yn;
   //setbkcolor(13);
   setfillstyle(1,5);
  // fillpoly(4,poli);
  rectangle(200,100,470,200);
  floodfill(210,150,1);
   gotoxy(30,10);
   printf("Do you want to exit?");
   gotoxy(30,11);
   printf("Yes(press y)");
   gotoxy(45,11);
   printf("No(press n)");
   reenter:
   yn=getch();
   if(yn=='y'||yn=='Y')
   exit(0);
   else
   if(yn=='n'||yn=='N')
    {}
   else
   { fflush(stdin);
    goto reenter;
    }
}

int mx=30,my=30,input=right,length=0,i,a,cordix[200],cordiy[200];

void main(void)
{
int gd=DETECT,gm=0,lifes=3,score=0,test;
extern int mx,my,length,cordix[200],cordiy[200],input,i,a;

initgraph(&gd,&gm," ");
if(gd==-2||gd==-3||gd==-4||gd==-5)
{
printf("Graphics error!. press any button to exit.");
getch();
exit(1);
}
cleardevice();
intro();
cleardevice();
revive:
if(lifes<3)
{ input=right;
  mx=30;
  my=30;
}
    randomize();
    randomize();
    xpoint=rand()%600 +20;
    ypoint=rand()%430 +30;

while(mx>=10&&mx<=630&&my>=20&&my<=470)
{  setbkcolor(12);
   setcolor(1);
  for(i=length;i>=1;i--)        //refreshing cordinates
  { cordix[i]=cordix[i-1];
    cordiy[i]=cordiy[i-1];
  }
  resume:
   if(input==27)
    input=80;

  gotoxy(20,1);
  printf("Score: %d",score);
  gotoxy(40,1);
  printf("Lifes:%d",lifes);
  boundry();
  delay(10);
  point(xpoint,ypoint);

  if(kbhit())
  { test=getch();
    if(test==up||test==down||test==right||test==left||test==27)
       if(input==up&&test!=down||input==down&&test!=up||input==right&&test!=left||input==left&&test!=right)
       {
	 input=test;
       }
  }
  if(input==up)
   my-=10;
  else
   if(input==down)
     my+=10;
  else
  if(input==right)
   mx+=10;
  else
  if(input==left)
   mx-=10;
  else
  if(input==27)
   { stopask();
     cleardevice();
     goto resume;
    }


  cordix[0]=mx;
  cordiy[0]=my;

   body(mx,my);
  for(i=length;i>=1;i--) //checks if body is touching itself.
      if(cordix[0]==cordix[i]&&cordiy[0]==cordiy[i])
      {
	 delay(1000);
	goto bodyeat;
      }


     if(mx>=(xpoint-6)&&mx<=(xpoint+6)&&my<=(ypoint+6)&&my>=(ypoint-6))
    { length++; score+=10;               //checks if touching the food.
      randomize();
      randomize();
      xpoint=rand()%600 +20;
      ypoint=rand()%430 +30;
    }
    delay(60);
    cleardevice();

}
bodyeat:
lifes--;
length=0;
if(lifes==0)
end();
else
goto revive;
delay(1000);
closegraph();
}
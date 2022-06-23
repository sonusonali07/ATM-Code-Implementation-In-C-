#include<stdio.h>
#include<stdlib.h>
#include<string.h>
#nclude<stdio.h>
#include<stdlib.h>
#include<string.h>
#include<time.h>

#define IST (+5)
double transferAmt;

char bankName1[] = "KBL.dat";
char bankName2[] = "SBI.dat";
char bankName3[] = "CANARA.dat";
char bankName4[] = "UNION.dat";
double m = 10000;
double n = 100;

void User(int);
void Admin(int);
void create(int);
void delete(int,int);
void deposit(int,int,int);
void display(int);
void checkBalance(int);
int getPw(int);
int checkValidity(unsigned long long int,int);
void transfer(int);
void unblock(int);

struct password{
int Kbl;
int Sbi;
int Canara;
int Union;
}pw={111,222,444,333};

struct customer{
unsigned long long int account_no;
int pass;
char name[20];
double balance;
int k;
int t_hours;
int t_minutes;
int day,month,year;
include<time.h>

#define IST (+5)
double transferAmt;

main()
{
/*
FILE *ptr,*ptr1,*ptr2,*ptr3;
ptr = fopen("KBL.dat","wb");
ptr1 = fopen("SBI.dat","wb");
ptr2 = fopen("UNION.dat","wb");
ptr3 = fopen("CANARA.dat","wb");

fclose(ptr);
fclose(ptr1);
fclose(ptr2);
fclose(ptr3);
*/
for(;;)
 {
 int bankCode,choice;
 FILE *ptr;
 printf("\n**************************************************************\n");
 printf("WELCOME TO THE ATM WORLD...\n");
 printf("****************************************************************\n");
 start:
 printf("\nEnter ur bank code:\n");
 printf("\t(AVAILABLE BANK CODES:\n\tKBL : 1111\n\tSBI : 2222\n\tUNION : 3333\n\tCANARA : 4444))\n");
 scanf("%d",&bankCode);

 switch(bankCode)
 {
  case 1111:printf("\nWelcome to KBL bank!\n\t HAPPY TRANSACTION...!\n");
            break;
  case 2222:printf("\nWelcome to SBI bank!\n\t HAPPY TRANSACTION....!\n");
            break;
  case 3333:printf("\nWelcome to UNION bank!\n\t HAPPY TRANSACTION....!\n");
            break;
  case 4444:printf("\nWelcome to CANARA bank!\n\t HAPPY TRANSACTION....!\n
 break;
  default:printf("\nInvalid bank code!\n");
          printf("please refer from instruction and try again\n\n********************\n\n");
          goto start;
          exit(0);
          break;
 }//switch bankCode
 printf("\n\n--------------------------------------------------------\n");
 printf("\nPlz press..\n1.For Admin.\n2.For User\n");
 scanf("%d",&choice);

 if(choice==1)
 {
  Admin(bankCode);
 }//if
 else if(choice==2)
 {
  User(bankCode);
 }//elif
 else
 {
  printf("\nInvalid choice....\n");
  exit(0);
 }//else
}//fot(;;)
}

/****************************************************************/

void User(int bankCode)
{
 int choice;
 for(;;)
 {
  printf("\n\n====================================\n");
  printf("\nPlz press...\n1.For DEPOSIT.\n2.WITHDRAW.\n3.CHECK BALANCE\n4.TRANSFER\n");
  scanf("%d",&choice);

  switch(choice)
  {
   case 1:deposit(bankCode,1,0);
 break;
   case 2:deposit(bankCode,2,1);
        break;
   case 3:checkBalance(bankCode);
        break;
   case 4:transfer(bankCode);
        break;
   default:printf("\ninvalid choice !\n");
        return;
  }//switch
 }//for
}//user

/*******************************************************************/
int getPw(int bankCode)
{
   switch(bankCode)
     {
     case 1111:return pw.Kbl;
     case 2222:return pw.Sbi;
     case 3333:return pw.Union;
     case 4444:return pw.Canara;
     default : return 0;
    }
} //getpw

void Admin(int bankCode)
{
 int choice,pwd1;
  printf("Enter password:\n");
  scanf("%d",&pwd1);

  if(pwd1 == (getPw(bankCode)))
  {
   printf("logged in successfully...\n");

  for(;;)
  {
   printf("\n\n------------------------------------------------------------\n");
   printf("\nPlz press...\n1.To CREATE NEW ACCOUNT.\n2.TO DISPLAY DESPLAY DETAILS OF ALL USERS.\n3.TO MODIFY USER DATA\n4.TO DELETE ACCOUNT\n5.UNBLOCK\n");
   scanf("%d",&choice);

  switch(choice)
   {
    case 1:create(bankCode);
        break;

    case 2:display(bankCode);
        break;

    case 3:delete(bankCode,2);
         break;

    case 4:delete(bankCode,1);
        break;

    case 5:unblock(bankCode);
        break;
     default:printf("invalid choice!\n");
        return;
 }//switch
 }//for
}//if

else
{
exit(0);
}
}//admin

/******************************************************************/

void deposit(int bankCode,int transaction1,int transaction2)
{
 FILE *ptr1,*ptr2;
 char bankName[11];
 struct customer c3;
 ptr2=fopen("temp.dat","wb");
 time_t rawtime;
 struct tm *info;

 time(&rawtime);
 info=gmtime(&rawtime);
 int t_hourss=(info->tm_hour+IST)%24;
   int t_minutess=(info->tm_min+35);
 if(t_minutess>60)
 {
   int something = t_minutess/60;
  t_hourss = t_hourss+something;
  t_minutess = t_minutess%60;
 }
 printf("%2d:%02d\n",t_hourss,t_minutess);

 switch(bankCode)
 {
  case 1111:
        ptr1=fopen("KBL.dat","rb");
        strcpy(bankName,bankName1);
        break;

 case 2222:
        ptr1=fopen("SBI.dat","rb");
        strcpy(bankName,bankName2);
        break;

 case 3333:
        ptr1=fopen("UNION.dat","rb");
        strcpy(bankName,bankName3);
        break;

 case 4444:
        ptr1=fopen("CANARA.dat","rb");
        strcpy(bankName,bankName4);
        break;
 default:printf("invalid bank code..\n");
        return;
 }//switch

int flag1=0;
int pin,chance=3;
unsigned long long int num;
printf("enter ur num:\n");
scanf("%llu",&num);

double amount;

while(fread(&c3,sizeof(struct customer),1,ptr1))
{

 if(c3.account_no==num )
 {
  if(c3.state == 0)
  {
    printf("***********************************************\n\n");
    printf("SORRY...  THIS  ACCOUNT  NUMBER  IS  BLOCKED\n TRANSACTION NOT ALLOWED !\n");
    printf("TO CONTINUE TRANSACTIONS PLEASE UNBLOCK YOUR ACCOUNT THROUGH BANK");
    printf("\n\n**************************************************\n");
    exit(0);
  }//if done
  flag1=1;

  while(chance>=0){
  printf("enter ur pass:\n");
  scanf("%d",&pin);
         if(pin==c3.pass)
        {
          printf("congrats! %s u have successfully logged in...\n",c3.name);

         double amount;
                if(transaction1 == 1 && transaction2==0)
                {
                        printf("enter amount to deposit:\n");
                        scanf("%lf",&amount);
                        c3.balance+=amount;

                        printf("\nUr current balance is= %lf\n",c3.balance);

                        fwrite(&c3,sizeof(struct customer),1,ptr2);
                        break;
               }//trans1
                else
                {
                if(c3.total>=25000)
                        {
                          printf("u  have exceeded max limit per today\n");
                         exit(0);
                        }
        if((t_hourss-c3.t_hours)==0 && (t_minutess-c3.t_minutes)<3 && c3.k>=2 )
{
                        printf("\nBut, SORRY..u have exeeded maximum transaction limit per day...\n");
                                exit(0);
                        }
                        if((t_minutess-c3.t_minutes)>3)
                        {
                        c3.k=0;
                        c3.total=0.0;
                        }

                        if(transaction2==1){
                        printf("enter the amount to  be withdrawn:\n");
                             scanf("%lf",&amount);
                        }
                        else
                        {
                                  printf("Enter the amount to be transferred:\n");
                                scanf("%lf",&amount);
                                transferAmt=amount;
                        }
                 if(amount<n)
                {
                        printf("Sorry..The amount is less than minimum amount\n");
                        fwrite(&c3,sizeof(struct customer),1,ptr2);
                        break;
                }
                else if(amount>m)
                {
                        printf("Sorry.. th amount is greater than max transaction per withdrawn\n");
                        fwrite(&c3,sizeof(struct customer),1,ptr2);
                        break;
                }

                else if(amount>c3.balance)
                {
                        printf("Sorry withdrawal amount is greater than ur account balance\n");
                         fwrite(&c3,sizeof(struct customer),1,ptr2);
                        break;
                }
                else
                {
                   c3.balance = c3.balance - amount;
 c3.total+=amount;
                   c3.k+=1;
                        time(&rawtime);
                        info=gmtime(&rawtime);
                        c3.t_hours=(info->tm_hour+IST)%24;
                        c3.t_minutes=(info->tm_min+35);

                        fwrite(&c3,sizeof(struct customer),1,ptr2);

                        printf("Ur current balance is= %lf\n",c3.balance);
                        break;
                }
                }//trans else
        }
  else if(chance>1)
  {
   printf("invalid password....try again\n");
   chance-=1;
  }
  else
  {
   printf("invalid passward\n");
   printf("*** UR ACCOUNT IS BLOCKED NOW !***\n*** U R NOT ALLOWED TO DO FURTHER TRANSACTIONS.***.\n");
   c3.state=0;
   fwrite(&c3,sizeof(struct customer),1,ptr2);
   break;
  }
 }//inner while
 }//outer if

 else
 {
 fwrite(&c3,sizeof(struct customer),1,ptr2);
 }

}//outer while
 fclose(ptr1);
 fclose(ptr2);

 if(flag1==0)
 {
  printf("invalid account number..\n");
                                          
}
  remove(bankName1);
  rename("temp.dat",bankName1);

}//deposit

/*****************************************************************/
int checkValidity(unsigned long long int acc,int size)
{
 int count=0;
 while(acc!=0)
 {
  acc=acc/10;
  count++;
 }
 if(count==size)
 {
  return 1;
 }
 else
  {
   return 0;
  }
}


void create(bankCode)
{
 int month,day,year;
 FILE *ptr1,*ptr2;
 char bankName[11];
 int pwd1;
 struct customer c1;
 switch(bankCode)
 {
  case 1111:
        ptr1=fopen("KBL.dat","ab");
        ptr2=fopen("KBL.dat","rb");
        strcpy(bankName,bankName1);
        break;
 case 2222:
 ptr1=fopen("SBI.dat","ab");
        ptr2=fopen("SBI.dat","rb");
        strcpy(bankName,bankName2);
        break;

 case 3333:
        ptr1=fopen("UNION.dat","ab");
        ptr2=fopen("UNION.dat","rb");
        strcpy(bankName,bankName3);
        break;

 case 4444:
        ptr1=fopen("CANARA.dat","ab");
        ptr2=fopen("CANARA.dat","rb");
        strcpy(bankName,bankName4);
        break;
 default:printf("invalid bank code..\n");
        return;

 }//switch

unsigned long long int acc,mob;
char Name[20];
int pwd,flag;
int size,vflag;

         printf("enter details for new user:\n");

//label  for setting num
setAccountNumber:
printf("enter new account number\n");
 scanf("%llu",&acc);
printf(" account num = %llu",acc);

        vflag=checkValidity(acc,16);

         if(vflag==0)
        {
        printf("\nInvalid account number !\nAccount number must have16 digit number\n");
        goto setAccountNumber;
        }
  }

setMobNumber:
printf("\nEnter ur mobile number:\n");
scanf("%llu",&mob);

vflag=checkValidity(mob,10);

if(vflag==0)
{
 printf("\nInvalid mobile number !\n mobile number must have 10 digit..\n");
 goto setMobNumber;
}

if(NULL !=ptr2){
 fseek(ptr2,0,SEEK_END);
 size=ftell(ptr2);
 fclose(ptr2);

        if(size == 0)
        {
        c1.account_no=acc;
        c1.mobNum=mob;
        c1.total = 0;
        flag=1;
        }

        else
        {
        ptr2=fopen(bankName,"rb");
                while(fread(&c1,sizeof(struct customer),1,ptr2))
                {
                        flag=0;
                        if(c1.account_no != acc)
                        {
                        c1.account_no=acc;
                        c1.mobNum=mob;
                        flag=1;
                        c1.total = 0;
                        }
                        else
                                                     
 {
                        printf("This account no is already existed...\nplz try another number!\n");
                        break;
                        }
                }//while
        }//el
}//outermost if
if(flag==1)
{
  printf("%llu\n",c1.account_no);
  printf("set password  for user:\n");
  scanf("%d",&c1.pass);
  c1.total = 0.0;
  c1.balance=0.0;
  c1.k=0;
setdate:
 printf("enter date of birth  of the customer...\n");
printf("enter day\n");
scanf("%d",&day);

if(day<=0  || day>=31)
{
printf("invalid day\n");
printf("enter the day again\n");
goto setdate;
}
        c1.day = day;
        setmonth:
        printf("enter the month of dob\n");
        scanf("%d",&month);

        if(month<=0 || month>=12)
        {
        printf("invalid month\n");
        printf("enter the valid month\n");
        goto setmonth;
        }
         c1.month = month;

                setyear:
                printf("enter the year of dob\n");
  scanf("%d",&year);

                if(year<=1900 || year>=2021)
                {
                printf("invalid year\n");
                printf("enter the valid year\n\nyear can't be more than 2021\n");
                goto setyear;
                }
                c1.year = year;

                         printf("enter ur name:\n");
                        scanf("%s",c1.name);
                        c1.state=1;

fwrite(&c1,sizeof(struct customer),1,ptr1);
}

fclose(ptr1);
fclose(ptr2);

}//create

/***************************************************************/

void display(int bankCode)
{
 FILE *ptr1;
 char bankName[11];
 switch(bankCode)
 {
  case 1111:
        ptr1=fopen("KBL.dat","rb");
        strcpy(bankName,bankName1);
        break;

 case 2222:
        ptr1=fopen("SBI.dat","rb");
       strcpy(bankName,bankName2);
        break;

 case 3333:
        ptr1=fopen("UNION.dat","rb");
                                           
 strcpy(bankName,bankName3);
        break;

 case 4444:
        ptr1=fopen("CANARA.dat","rb");
        strcpy(bankName,bankName4);
        break;

 default:printf("invalid bank code..\n");
        return;

 }//switch

 struct customer c;
 while(fread(&c,sizeof(struct customer),1,ptr1))
 {
  printf("Name:%s\tACCOUNT N0.:%llu\tPASSWORD:%d\tMOB_NO:%llu\tBALANCE=%lf\tk=%d\n",c.name,c.account_no,c.pass,c.mobNum,c.balance,c.k);
   printf("\tLAST TRANSACTION: %2d:%02d\tSTATE:%d\n\n",c.t_hours,c.t_minutes,c.state);
 }
 fclose(ptr1);
}//display

/*************************************************************/

void checkBalance(int bankCode)
{
 FILE *ptr1;
 char bankName[11];
 switch(bankCode)
 {
  case 1111:
        ptr1=fopen("KBL.dat","rb");
        strcpy(bankName,bankName1);
        break;

 case 2222:
        ptr1=fopen("SBI.dat","rb");
        strcpy(bankName,bankName2);
        break;

 case 3333:
        ptr1=fopen("UNION.dat","rb");
  strcpy(bankName,bankName3);
        break;

 case 4444:
        ptr1=fopen("CANARA.dat","rb");
        strcpy(bankName,bankName4);
        break;

 default:printf("invalid bank code..\n");
        return;

 }//switch

unsigned long long int num;
int pas;//,flag=0;

struct customer c2;
printf("enter ur account number:\n");
scanf("%llu",&num);
printf("enter ur passward:\n");
scanf("%d",&pas);
       // ptr1=fopen(bankName,"rb");
   while(fread(&c2,sizeof(struct  customer),1,ptr1))
        {
         if(c2.state==1)
         {
          if(num== c2.account_no && pas==c2.pass)
             {
                printf("ur current balance is= %lf\n",c2.balance);
                break;
              }
         }
         else
            printf("UR ACCOUNT NUM IS BLOCKED !U CANNOT CHECK UR BALANCE\n");
        }
   fclose(ptr1);
}

/***************************************************************************************************************/

void delete(int bankCode,int ch)
{
 FILE *ptr1,*ptr;
 struct customer c1;
 unsigned long long int account_no;
 char bankName[11];
 ptr=fopen("temp.dat","wb");
  switch(bankCode)
  {
   case 1111:
         ptr1=fopen("KBL.dat","rb");
         strcpy(bankName,bankName1);
         break;

  case 2222:
         ptr1=fopen("SBI.dat","rb");
         strcpy(bankName,bankName2);
         break;

  case 3333:
         ptr1=fopen("UNION.dat","rb");
         strcpy(bankName,bankName3);
         break;

  case 4444:
        ptr1=fopen("CANARA.dat","rb");
         strcpy(bankName,bankName4);
         break;
  }//switch
     printf("enter the account number u  want  to  delete or modify\n");
     scanf("%llu",&account_no);

    while(fread(&c1,sizeof(struct  customer),1,ptr1))
         {           if(account_no == c1.account_no)
              {
                 if(ch==1)
                  continue;
                 else
                 {
                  printf("enter new name:\nenter new account number\nenter new password:\nenter modified balance:\n");
                  scanf("%s %ld %d %lf",c1.name,&c1.account_no,&c1.pass,&c1.balance);
                  fwrite(&c1,sizeof(struct customer),1,ptr);
                 }//el
 }//if

          else
           {
            fwrite(&c1,sizeof(struct customer),1,ptr);
          }//else

         }//while
 remove(bankName);
 rename("temp.dat",bankName);
 fclose(ptr);
 fclose(ptr1);
 }//delete


/***********************************************************************/

void transfer(bankCode)
{

 FILE *ptr1,*ptr2;
 char bankName[11];
 struct customer c3;
 int enBankCode;
 unsigned long long int enAcc;
 ptr2=fopen("temp.dat","wb");

 printf("Enter the Bank code of receiver:\n");
 scanf("%d",&enBankCode);
 printf("Enter the account number of receiver:\n");
 scanf("%llu",&enAcc);

 switch(enBankCode)
 {
  case 1111:
        ptr1=fopen("KBL.dat","rb");
        strcpy(bankName,bankName1);
        break;
  case 2222:
        ptr1=fopen("SBI.dat","rb");
        strcpy(bankName,bankName2);
        break;

  case 3333:
        ptr1=fopen("UNION.dat","rb");
        strcpy(bankName,bankName3);
        break;

  case 4444:
        ptr1=fopen("CANARA.dat","rb");
        strcpy(bankName,bankName4);
        break;

  default:printf("invalid bank code..\n");
        return;

 }//switch

 int flag1=0;
 int num,sState;
 while(fread(&c3,sizeof(struct customer),1,ptr1))
 {
  if(c3.account_no==enAcc)
  {
   deposit(bankCode,2,2);
   flag1=1;
   c3.balance+=transferAmt;
   printf("bal = %lf\n",c3.balance);
   printf("Transaction Successfull...!\n");

   fwrite(&c3,sizeof(struct customer),1,ptr2);

  }
  else
  {
  fwrite(&c3,sizeof(struct customer),1,ptr2);
  }
                                              
}
 fclose(ptr1);
 fclose(ptr2);

 if(flag1==0)
 {
  printf("invalid account number..\n");
 }

  remove(bankName);
  rename("temp.dat",bankName);
}

/***********************************************************************/

void unblock(bankCode)
{
 unsigned long long int bAcc;
 char bankName[11];
 FILE *ptr1,*ptr2;

 switch(bankCode)
 {
  case 1111:
        ptr1=fopen("KBL.dat","rb");
        strcpy(bankName,bankName1);
        break;

  case 2222:
        ptr1=fopen("SBI.dat","rb");
        strcpy(bankName,bankName2);
        break;

  case 3333:
        ptr1=fopen("UNION.dat","rb");
        strcpy(bankName,bankName3);
        break;

  case 4444:
        ptr1=fopen("CANARA.dat","rb");
        strcpy(bankName,bankName4);
        break;

  default:printf("invalid bank code..\n");
        return;

 }//switch

 ptr2=fopen("temp.dat","wb");
 struct customer c;

 printf("Enter account number:\n");
 scanf("%llu",&bAcc);

 while(fread(&c,sizeof(struct customer),1,ptr1)){
  if(c.account_no==bAcc)
  {
   c.state=1;
   fwrite(&c,sizeof(struct customer),1,ptr2);
   printf("UNBLOCKED SUCCESSFULLY..\n");
  }//if
  else
  {
   fwrite(&c,sizeof(struct customer),1,ptr2);
  }
 }//while
 remove(bankName);
 rename("temp.dat",bankName);
 fclose(ptr2);
 fclose(ptr1);

}

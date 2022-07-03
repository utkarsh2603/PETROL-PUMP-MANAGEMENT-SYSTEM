//password is 'ppms'
#include <ctype.h>
#include <string.h>
#include <stdio.h>
#include <dos.h>
#include <iomanip.h>
#include <iostream.h>
#include <fstream.h>
#include <process.h>
#include <conio.h>

class pump
{
private:
    float totpet, totrspet, charg, qty;
    int totservice, tottyer, sno, pak;
    float totdis, totrsdis, tlubric, ratepetrol, ratedisel;
    float trslubric, trslubricpak, trsservice, trstyer, tlubricpak;
    char no[15], item[10];

public:
    void end();
    void sale(float, float, float, float, float, float, int, float, int, float, int, float);
    void start();
    int service();
    void entry(float, float, char *);
    int tyers();
    void show();
    void bill();
    void find();
    void getdata(char *, int, char *, float, float);
    void bill(char *, float, float, float, float, float, float, int, float, int, float, float);
    void password();
} petrol;

void main()
{
    clrscr();
    char no[15], item[10];
    float ratepetrol, ratedisel, ratelub, costlub = 0, lub = 0, costpak;
    float costservice = 0, costtyer = 0, litpet = 0, costpet = 0, litdis = 0, costdis = 0;
    int m = 1, d, x = 0, sno, choice, choicepet, choicedis, choicelubric;
    int pak = 0, totservice = 0, tottyer = 0;
    float totpet = 0, totrspet = 0, totdis = 0, totrsdis = 0, tlubric = 0, trslubric = 0;
    float tlubricpak = 0, trslubricpak = 0, trsservice = 0, trstyer = 0;
    float charg, rs_pk = 0, qty;

    petrol.start();
    clrscr();
    petrol.password();
    textmode(C80);
    textcolor(15);
    int i;
    for (i = 1; i <= 80; i++)
    {
        gotoxy(i, 1);
        cprintf("#");
        //delay(20);
    }
    for (i = 2; i <= 23; i++)
    {
        gotoxy(80, i);
        cprintf("#");
        //delay(20);
    }
    for (i = 80; i >= 1; i--)
    {
        gotoxy(i, 24);
        cprintf("#");
        //delay(20);
    }
    for (i = 23; i >= 2; i--)
    {
        gotoxy(1, i);
        cprintf("#");
        //delay(20);
    }
    delay(200);

    gotoxy(25, 10);
    textcolor(14);
    cprintf("Enter the rate of Petrol :: ");
    cin >> ratepetrol;
    gotoxy(25, 13);
    textcolor(14);
    cprintf("Enter the rate of Diesel :: ");
    cin >> ratedisel;
    while (m < 4)
    {
        clrscr();
        textcolor(15);
        int i;
        for (i = 1; i <= 80; i++)
        {
            gotoxy(i, 1);
            cprintf("^");
            //delay(20);
        }
        for (i = 2; i <= 23; i++)
        {
            gotoxy(80, i);
            cprintf("^");
            //delay(20);
        }
        for (i = 80; i >= 1; i--)
        {
            gotoxy(i, 24);
            cprintf("^");
            //delay(20);
        }
        for (i = 23; i >= 2; i--)
        {
            gotoxy(1, i);
            cprintf("^");
            //delay(20);
        }
        delay(200);

        gotoxy(25, 8);
        textcolor(2);
        cprintf("Enter [ 1 ]  for Add New Record ");
        gotoxy(25, 10);
        cprintf("Enter [ 2 ]  for Display All Records ");
        gotoxy(25, 12);
        cprintf("Enter [ 3 ]  for Find Any Record ");
        gotoxy(25, 14);
        cprintf("Enter [ 4 ]  for Exit ");
        gotoxy(25, 18);
        textcolor(14);
        cprintf("Enter Your Choice Here :: ");
        cin >> m;
        clrscr();
        if (m == 1)
        {
            d = 2;
            fstream fill;
            fill.open("p.dat", ios::app);
            int i, j, k;
            fill.seekg(0, ios::end);
            char *p;
            i = fill.tellg();
            j = sizeof(pump);
            k = i / j;
            j++;
            sno = k + 1;
            gotoxy(10, 3);
            textcolor(4);
            cprintf("N E W  V E H I C L E ");
            gotoxy(10, 4);
            cprintf("---------------------");
            gotoxy(10, 5);
            textcolor(6);
            cprintf("Service Number :: ");
            cout << sno;
            gotoxy(10, 7);
        vno:
            gotoxy(6, 8);
            textcolor(14);
            cprintf("Please enter vehicle number in this format [hr03c1234] only  :: ");
            gets(no);
            if (strlen(no) == 0)
            {
                gotoxy(10, 12);
                textcolor(4);
                cprintf("Vehicle Number cannot left blank");
                gotoxy(10, 14);
                cprintf("Enter  Vehicle Number please....");
                getch();
                gotoxy(10, 12);
                clreol();
                gotoxy(10, 14);
                clreol();
                goto vno;
            }
            for (int r = 0; no[r] != '\0'; r++) //loop to change name to uppercase
            {
                no[r] = toupper(no[r]);
            }
            litpet = costpet = litdis = costdis = lub = costlub = pak = rs_pk = x = costservice = costtyer = 0;
            while (d > 1)
            {
                clrscr();
                petrol.entry(ratepetrol, ratedisel, no);
                cin >> choice;
                switch (choice)
                {
                case 1:
                    clrscr();
                    gotoxy(33, 2);
                    strcpy(item, "Petrol");
                    textcolor(2);
                    cprintf("PETROL");
                    gotoxy(33, 3);
                    cprintf("------\n\n");
		    gotoxy(10, 5);
		    textcolor(6);
		    cprintf("Enter [ 1 ]   for  Liter\n ");
		    gotoxy(10, 6);
		    cprintf("Enter [ 2 ]   for  Rupees ");
		    gotoxy(10, 7);
		    textcolor(14);
		    cprintf("Enter Your Choice (1 or 2) :: ");
		    cin >> choicepet;
		    if (choicepet == 1)
		    {
			gotoxy(10, 10);
			textcolor(14);
			cprintf("  How many liters :: ");
			cin >> litpet;
			totpet = totpet + litpet;
			qty = litpet;
			costpet = litpet * ratepetrol;
			charg = costpet;
			totrspet = totrspet + costpet;
			gotoxy(10, 12);
			textcolor(5);
			cprintf("     Rupees. ");
			cprintf("%5.2f", costpet);
			cprintf(" only");
			gotoxy(50, 23);
			textcolor(15);
			cprintf("Press Enter key ");
			getch();
		    }
		    if (choicepet == 2)
		    {
			gotoxy(10, 10);
			textcolor(14);
			cprintf("   How much Rupees :: ");
			cin >> costpet;
			charg = costpet;
			totrspet = totrspet + costpet;
			qty = costpet / ratepetrol;
			litpet = qty;
			totpet = totpet + qty;
			gotoxy(10, 12);
			textcolor(5);
			cprintf("     Petrol filled :: %.2f  liters", qty);
			gotoxy(50, 23);
			textcolor(15);
			cprintf("Press Enter key ");
			getch();
		    }
		    break;
		case 2:
		    clrscr();
		    strcpy(item, "Diesel");
		    gotoxy(33, 2);
		    textcolor(2);
		    cprintf("DIESEL");
		    gotoxy(33, 3);
		    cprintf("------");
		    gotoxy(10, 5);
		    textcolor(6);
		    cprintf("Enter [ 1 ]   for  Liter\n ");
		    gotoxy(10, 6);
		    cprintf("Enter [ 2 ]   for  Rupees ");
		    gotoxy(10, 7);
		    textcolor(14);
		    cprintf(" \n   Enter your choice (1 or 2 ) :: ");
		    cin >> choicedis;
		    if (choicedis == 1)
		    {
			gotoxy(10, 10);
			textcolor(14);
			cprintf("How many liters :: ");
			cin >> litdis;
			totdis = totdis + litdis;
			qty = litdis;
			costdis = litdis * ratedisel;
			charg = costdis;
			totrsdis = totrsdis + costdis;
			gotoxy(10, 12);
			textcolor(5);
			cprintf("Rupees :: ");
			cprintf("%.2f", costdis);
			cprintf("  only.");
			gotoxy(50, 23);
			textcolor(15);
			cprintf("Press Enter key ");
			getch();
		    }
		    if (choicedis == 2)
		    {
			gotoxy(10, 10);
			textcolor(14);
			cprintf("   How much Rupees :: ");
			cin >> costdis;
			totrsdis = totrsdis + costdis;
			charg = costdis;
			qty = costdis / ratedisel;
			litdis = qty;
			totdis = totdis + qty;
			gotoxy(10, 12);
			textcolor(5);
			cprintf("       Diesel filled = %.2f  liters ", qty);
			gotoxy(50, 23);
			textcolor(15);
			cprintf("Press Enter key ");
			getch();
		    }

		    break;

		case 3:
		    clrscr();
		    strcpy(item, "Tyers");
		    charg = petrol.tyers();
		    costtyer = charg;
		    tottyer++;
		    trstyer = trstyer + charg;
		    gotoxy(50, 23);
		    textcolor(15);
		    cprintf("Press Enter key ");
		    getch();
		    break;

		case 4:
		    clrscr();
		    x++;
		    strcpy(item, "Service");
		    charg = petrol.service();
		    qty = 0;
		    costservice = charg;
		    trsservice = charg + trsservice;
		    totservice++;
		    gotoxy(50, 23);
		    textcolor(15);
		    cprintf("Press Enter key ");
		    getch();
		    break;
		case 5:
		    clrscr();
		    strcpy(item, "Lubricant");
		    gotoxy(33, 2);
		    textcolor(2);
		    cprintf("LUBRICANTS");
		    gotoxy(33, 3);
		    cprintf("----------");
		    gotoxy(10, 5);
		    textcolor(6);
		    cprintf("Enter  [ 1 ]   for  liter ");
		    gotoxy(10, 6);
		    cprintf("Enter  [ 2 ]   for  Packets");
		    gotoxy(10, 7);
		    textcolor(14);
		    cprintf("Enter Your choice :: ");
		    cin >> choicelubric;
		    switch (choicelubric)
		    {
		    case 1:
			gotoxy(10, 9);
			textcolor(6);
			cprintf("Rate of the oil ::");
			cin >> ratelub;
			gotoxy(10, 10);
			textcolor(14);
			cprintf("How many liters :: ");
			cin >> lub;
			qty = lub;
			tlubric = lub + tlubric;
			charg = ratelub * lub;
			costlub = charg;
			trslubric = trslubric + charg;
			gotoxy(10, 13);
			textcolor(5);
			cprintf("The charges for ");
			cout << lub;
			cprintf("  liters oil  :: ");
			cprintf("%.2f", charg);
			cprintf("   Rupees only.");
			gotoxy(50, 23);
			textcolor(15);
			cprintf("Press Enter key ");
			getch();
			break;
		    case 2:
			gotoxy(10, 9);
			textcolor(6);
			cprintf("Enter the rate of one packet :: ");
			cin >> costpak;
			gotoxy(10, 10);
			textcolor(14);
			cprintf("Enter how many packets you want to buy :: ");
			cin >> pak;
			qty = pak;
			tlubricpak = tlubricpak + pak;
			charg = pak * costpak;
			rs_pk = charg;
			trslubricpak = trslubricpak + charg;
			gotoxy(10, 13);
			textcolor(5);
			cprintf("The charges for the ");
			cout << pak;
			cprintf("  packets  :: ");
			cprintf("%.2f", rs_pk);
			cprintf("  Rupees  only");
			gotoxy(50, 23);
			textcolor(15);
			cprintf("Press Enter key ");
			getch();
			break;
		    }
		    break;

		case 6:
		    clrscr();
		    petrol.bill(no, litpet, costpet, litdis, costdis, lub, costlub, pak, rs_pk, x,
				costservice, costtyer);
		    getch();
		    break;
		case 7:
		    d = 0;
		    break;
		}
		petrol.getdata(no, sno, item, qty, charg);
		fill.write((char *)&petrol, sizeof(petrol));
		fill.close();
	    }
	}
	if (m == 2)
	{
	    clrscr();
	    petrol.show();
	}
	if (m == 3)
	{
	    clrscr();
	    petrol.find();
	    getch();
	}
	if (m == 4)
	    break;
    }
    petrol.sale(totpet, totrspet, totdis, totrsdis, tlubric, trslubric, tlubricpak, trslubricpak, totservice, trsservice, tottyer, trstyer);
    petrol.end();
}

//:::::::::::::::::::::::| functions  |:::::::::::::::::::::::::::::://

void pump::start()
{
    textmode(C40);
    char a[10][42];
    textcolor(15);
    strcpy(a[1], "A  S O F T W A R E   D E V L O P E D ");
    strcpy(a[2], "F O R");
    strcpy(a[3], "     ");
    strcpy(a[4], "PETROL PUMP MANAGEMENT SYSTEM");
    strcpy(a[5], "  ");
    strcpy(a[6], "     ");
    int r = 4;
    for (int j = 1; j <= 6;j++)
    {
	int l = strlen(a[j]);
	int x = ((40 - l) / 2) + 1;
	gotoxy(x, r);
	for (int p = 0; p < l; p++)
	{
	    putch(a[j][p]);
            //delay(60);
        }

        delay(20);
        if (j == 7)
            textcolor(7 + BLINK);
        else
            textcolor(WHITE);
        r = r + 2;
        if (j == 5)
            r = r + 2;
    }
    textcolor(WHITE + BLINK);
    gotoxy(13, 24);
    cprintf("WAIT FOR MOMENT...");
    textcolor(WHITE);
    delay(1000);
    textmode(C80);
}

//////////////////////////////////////////////////////////////////////////////////////

void pump::entry(float x, float y, char *xx)
{
    gotoxy(37, 1);
    textcolor(4);
    cprintf("MENU");
    gotoxy(36, 2);
    cprintf("------");
    gotoxy(27, 3);
    textcolor(2);
    cprintf("VEHICLE NUMBER :: ");
    cout << xx;
    gotoxy(10, 5);
    textcolor(14);

    cprintf("RATE OF PETROL :: Rs ");
    cout << setprecision(2) << x;
    gotoxy(45, 5);
    textcolor(14);

    cprintf("RATE OF DIESEL :: Rs  ");
    cout << setprecision(2) << y;
    gotoxy(30, 8);
    textcolor(5);

    cprintf("ENTER [ 1 ]   FOR PETROL ");
    gotoxy(30, 10);
    cprintf("ENTER [ 2 ]   FOR DIESEL ");
    gotoxy(30, 12);
    cprintf("ENTER [ 3 ]   FOR TYERS ");
    gotoxy(30, 14);
    cprintf("ENTER [ 4 ]   FOR SERVICE ");
    gotoxy(30, 16);
    cprintf("ENTER [ 5 ]   FOR LUCBRICANTS ");
    gotoxy(30, 18);
    cprintf("ENTER [ 6 ]   FOR DISPLAY CURRENT RECORD ");
    gotoxy(30, 20);
    cprintf("ENTER [ 7 ]   FOR EXIT FROM CURRENT RECORD ");
    gotoxy(30, 24);
    textcolor(14);

    cprintf("Enter Your choice ::  ");
}
//////////////////////////////////////////////////////////////////////////////////////

int pump::service()
{
    int ch, ch1, charg;
    clrscr();
    gotoxy(37, 3);
    textcolor(2);
    cprintf("SERVICES");
    gotoxy(37, 4);
    cprintf("--------");
    gotoxy(10, 6);
    textcolor(6);
    cprintf("Enter [ 1 ]  For Washing ");
    gotoxy(10, 7);
    cprintf("Enter [ 2 ]  For Internal Cleaning ");
    gotoxy(10, 8);
    cprintf("Enter [ 3 ]  For Washing and Polishing ");
    gotoxy(10, 10);
    textcolor(14);
    cprintf("Enter Your choice (1 or 2 or 3) :: ");
    cin >> ch;
    clrscr();
    switch (ch)
    {
    case 1:
        gotoxy(10, 7);
        textcolor(6);
        cprintf("Enter [ 1 ]  For Two Wheeler ");
        gotoxy(10, 8);
        cprintf("Enter [ 2 ]  For Four Wheeler ");
        gotoxy(10, 10);
        textcolor(14);
        cprintf("Enter Your choice (1 or 2) :: ");
        cin >> ch1;
        if (ch1 == 1)
            charg = 30;
        else
            charg = 80;
        gotoxy(10, 13);
        textcolor(5);
        cprintf("Washing Charges :: Rs ");
        cout << charg;
        break;
    case 2:
        charg = 150;
        gotoxy(10, 13);
        textcolor(5);
        cprintf("Inner Cleaning Charges :: Rs ");
        cout << charg;
        break;
    case 3:
        gotoxy(10, 7);
        textcolor(6);
        cprintf("Enter [ 1 ]  For Two Wheeler \n");
        gotoxy(10, 9);
        cprintf("Enter [ 2 ]  For Four Wheeler\n");
        gotoxy(10, 11);
        textcolor(14);
        cprintf("Enter Your Choice (1 or 2) :: ");
        cin >> ch1;
        if (ch1 == 1)
            charg = 50;
        else
            charg = 120;
        gotoxy(10, 15);
        textcolor(5);
        cprintf("Washing and Polishing charges :: Rs ");
        cout << charg;
        break;
    }
    return (charg);
    getch();
}

//////////////////////////////////////////////////////////////////////////////////////

void pump::sale(float totpet, float totrspet, float totdis, float totrsdis,
                float tlubric, float trslubric, int tlubricpak, float trslubricpak,
                int totservice, float trsservice, int tottyer, float trstyer)
{
    clrscr();
    float sale = 0;
    sale = totrspet + totrsdis + trslubric + trslubricpak + trsservice + trstyer;
    gotoxy(30, 2);
    textcolor(4);
    cprintf("TODAY'S SALE ");
    gotoxy(29, 3);
    cprintf("--------------");
    gotoxy(14, 5);
    textcolor(3);
    cprintf("ITEM                                           RUPEES");
    gotoxy(14, 6);
    cprintf("-----                                        --------");
    gotoxy(12, 8);
    textcolor(14);
    cprintf("PETROL ");
    gotoxy(62, 8);
    cprintf("%.2f", totrspet);
    gotoxy(12, 10);
    cprintf("DIESEL ");
    gotoxy(62, 10);
    cprintf("%.2f", totrsdis);
    gotoxy(12, 12);
    cprintf("LUBRICANT 1) LITERS");
    gotoxy(62, 12);
    cprintf("%.2f", trslubric);
    gotoxy(21, 13);
    cprintf(" 2) PACKETS ");
    gotoxy(62, 13);
    cprintf("%.2f", trslubricpak);
    gotoxy(12, 15);
    cprintf("VEHICLES SERVICE");
    gotoxy(62, 15);
    cprintf("%.2f", trsservice);
    gotoxy(12, 17);
    cprintf("TYERS");
    gotoxy(62, 17);
    cprintf("%.2f", trstyer);
    gotoxy(10, 19);
    cprintf("--------------------------------------------------------");
    gotoxy(51, 21);
    textcolor(5);
    cprintf("CASH : ");
    cprintf("%.2f", sale);
    gotoxy(50, 22);
    cprintf("-----");
    gotoxy(60, 24);
    textcolor(15);
    cprintf("press any key...");
    getch();
}
//////////////////////////////////////////////////////////////////////////////////////

void pump::end()
{
    textmode(C40);
    textcolor(15);
    int i;
    for (i = 1; i <= 40; i++)
    {
        gotoxy(i, 1);
        cprintf("*");
        //delay(40);
    }
    for (i = 2; i <= 23; i++)
    {
        gotoxy(40, i);
        cprintf("*");
        //delay(40);
    }
    for (i = 40; i >= 1; i--)
    {
        gotoxy(i, 24);
        cprintf("*");
        //delay(40);
    }
    for (i = 23; i >= 2; i--)
    {
        gotoxy(1, i);
        cprintf("*");
        //delay(40);
    }
    delay(300);
    textcolor(WHITE);

    gotoxy(6, 8);
    cprintf("T H A N K S  F O R  U S I N G");
    gotoxy(16, 10);
    cprintf("T H I S");
    gotoxy(12, 12);
    cprintf("S O F T W A R E");
    gotoxy(8, 22);
    textcolor(WHITE + BLINK);
    cprintf("Press any key to exit ...");
    getch();
    textmode(C80);
}
//////////////////////////////////////////////////////////////////////////////////////

int pump::tyers()
{
    int ty, choice, tb;
    float rt, amount, amount1, rtb, charg;
    textcolor(6);
    gotoxy(5, 3);
    cprintf("Enter [ 1 ]  For New Tyre ");
    gotoxy(5, 4);

    cprintf("Enter [ 2 ]  For Tube ");
    gotoxy(5, 5);
    cprintf("Enter [ 3 ]  For Tyre and Tube ");
    textcolor(14);
    gotoxy(5, 7);
    cprintf("Enter your choice (1 or 2 or 3) :: ");
    cin >> choice;
    switch (choice)
    {
    case 1:
        textcolor(14);
        clrscr();
        gotoxy(5, 3);
        cprintf("Enter no of tyers you want to buy :: ");
        cin >> ty;
        gotoxy(5, 4);
        cprintf("Cost per tyre :: Rs ");
        cin >> rt;
        amount = ty * rt;
        textcolor(5);
        gotoxy(5, 6);
        cprintf("The cost of ");
        cout << ty;
        cprintf(" tyers is :: Rs ");
        cprintf("%.2f", amount);
        break;
    case 2:
        textcolor(14);
        clrscr();
        gotoxy(5, 3);
        cprintf("How many tubes want to buy ::  ");
        cin >> tb;
        gotoxy(5, 4);
        cprintf("Cost per tube :: Rs ");
        cin >> rtb;
        amount = tb * rtb;
        textcolor(5);
        gotoxy(5, 6);
        cprintf("The cost of ");
        cout << tb;
        cprintf(" tube is :: Rs ");
        cprintf("%.2f", amount);
        break;
    case 3:
        textcolor(14);
        clrscr();
        gotoxy(5, 3);
        cprintf("Enter no of tyers you want to buy :: ");
        cin >> ty;
        gotoxy(5, 4);
        cprintf("Cost of one tyre :: Rs ");
        cin >> rt;
        amount1 = ty * rt;
        textcolor(5);
        gotoxy(5, 5);
        cprintf("The cost of ");
        cout << ty;
        cprintf(" tyers is :: Rs ");
        cprintf("%.2f", amount1);
        textcolor(14);
        gotoxy(5, 7);
        cprintf("How many tubes want to buy :: ");
        cin >> tb;
        gotoxy(5, 8);
        cprintf("Cost per tube :: Rs ");
        cin >> rtb;
        charg = tb * rtb;
        textcolor(5);
        gotoxy(5, 9);
        cprintf("The cost of ");
        cout << tb;
        cprintf(" tubes is :: Rs ");
        cprintf("%.2f", charg);

        amount = charg + amount1;
        textcolor(5);
        gotoxy(5, 12);
        cprintf("Total charges  for ");
        cout << ty;
        cprintf(" tyer and ");
        cout << tb;
        cprintf("tube :: Rs ");
        cprintf("%.2f", amount);
        break;
    }
    return (amount);
}
//////////////////////////////////////////////////////////////////////////////////////

void pump::find()
{
    char no1[15];
    int y = 0;
    fstream file;

    clrscr();
    file.open("p.dat", ios::in | ios::out);
    file.seekg(0, ios::beg);
    clrscr();
    gotoxy(5, 6);
    textcolor(14);
    cprintf("ENTER VEHICLE NUMBER :: # ");
    gets(no1);
    for (int p = 0; no1[p] != '\0'; p++)
    {
        no1[p] = toupper(no1[p]);
    }

    file.read((char *)&petrol, sizeof(petrol));
    while (!file.eof())
    {
        if (strcmp(no1, no) == 0)
        {
            y = 8;
            clrscr();
            gotoxy(16, 10);
            textcolor(5);
            cprintf("The record number is :: ");
            cout << sno;
            gotoxy(16, 12);
            cprintf("Work done ");
            cout << item;
            gotoxy(16, 14);
            cprintf("Charges ");
            cprintf("%.2f", charg);
            getch();
        }
        file.read((char *)&petrol, sizeof(petrol));
    }
    file.close();
    if (y == 0)
    {
        gotoxy(30, 12);
        textcolor(15);
        cprintf("No entry of this number ");
    }
}
//////////////////////////////////////////////////////////////////////////////////////

void pump::show()
{
    clrscr();
    fstream file;
    file.open("p.dat", ios::in, ios::out);
    file.seekg(0, ios::beg);
    int row = 3;
    int flag = 0;
    char ch;
    gotoxy(1, 1);
    textcolor(3);
    cprintf("S NO. VEHICLE NUMBER           WORK DONE         QTY                CHARGES");
    gotoxy(1, 2);
    cprintf("---------------------------------------------------------------------------------");
    while (file.read((char *)&petrol, sizeof(petrol)))
    {
        _setcursortype(_NOCURSOR);
        flag = 0;
        delay(100);

        gotoxy(3, row);
        textcolor(14);
        cprintf("%d", sno);
        gotoxy(8, row);
        cprintf("%s", no);
        gotoxy(33, row);
        cprintf("%s", item);
        gotoxy(50, row);
        cprintf("%.2f", qty);

        gotoxy(71, row);
        cprintf("%.2f", charg);

        if (row == 23)
        {
            flag = 1;
            row = 3;
            gotoxy(17, 25);
            textcolor(15);
            cprintf("Press any key to go back to MAIN MENU....");
            ch = getch();
            if (ch == 27)
                break;
            clrscr();
            gotoxy(1, 1);
            textcolor(3);
            cprintf("S NO. VEHICLE NUMBER           WORK DONE         QTY             CHARGES  ");
            gotoxy(1, 2);
            cprintf("------------------------------------------");
        }
        else
            row = row + 2;
    }
    if (!flag)
    {
        gotoxy(20, 25);
        textcolor(15);
        cprintf("Press any key to go back to MAIN MENU....");
        getch();
    }
    file.close();
}
//////////////////////////////////////////////////////////////////////////////////////
void pump::getdata(char *no2, int sno1, char *item1, float qty1, float charg1)
{
    strcpy(no, no2);
    sno = sno1;
    strcpy(item, item1);
    qty = qty1;
    charg = charg1;
}
//////////////////////////////////////////////////////////////////////////////////////

void pump::bill(char *no, float litpet, float cpet, float litdis, float cdis, float lubric, float clubric, int pak, float cpak, int service, float cservice, float ctyer)
{

    clrscr();
    float sale = 0;
    sale = cpet + cdis + clubric + cpak + cservice + ctyer;
    gotoxy(27, 1);
    textcolor(4);
    cprintf("INDIA PETROL PUMP AND SERVICE STATION  ");
    gotoxy(26, 2);
    cprintf("---------------------------------------");
    gotoxy(30, 3);
    textcolor(14);
    cprintf("VECHICLE NUMBER # ");
    cout << no;
    gotoxy(14, 5);
    textcolor(3);
    cprintf("ITEM                 QUANTITY                 AMOUNT");
    gotoxy(14, 6);
    cprintf("-----               ----------               --------");
    gotoxy(12, 8);
    textcolor(2);
    cprintf("PETROL ");
    gotoxy(37, 8);
    cprintf("%.2f", litpet);
    gotoxy(62, 8);
    cprintf("%.2f", cpet);
    gotoxy(12, 10);
    cprintf("DIESEL ");
    gotoxy(37, 10);
    cprintf("%.2f", litdis);
    gotoxy(62, 10);
    cprintf("%.2f", cdis);

    gotoxy(12, 12);
    cprintf("LUBRICANT 1) LITERS");
    gotoxy(37, 12);
    cprintf("%.2f", lubric);
    gotoxy(62, 12);
    cprintf("%.2f", clubric);
    gotoxy(21, 13);
    cprintf(" 2) PACKETS ");
    gotoxy(37, 13);
    cprintf("%.2d", pak);
    gotoxy(63, 13);
    cprintf("%.2f", cpak);
    gotoxy(12, 15);
    cprintf("SERVICE");
    gotoxy(37, 15);
    cprintf("%2d", service);
    gotoxy(62, 15);
    cprintf("%4.2f", cservice);
    gotoxy(12, 17);
    cprintf("TYERS");
    gotoxy(62, 17);
    cprintf("%.2f", ctyer);
    textcolor(3);
    gotoxy(12, 19);
    cprintf("-----------------------------------------------------------");
    gotoxy(51, 21);
    textcolor(5);
    cprintf("CHARGES : ");
    cprintf("%4.2f", sale);
    gotoxy(50, 22);
    cprintf("--------");
}
//////////////////////////////////////////////////////////////////////////////////////

void pump::password()
{
    char pass[10] = {"ppms"};
    char pass1[10];
    textmode(C40);
label:
    gotoxy(10, 10);
    textcolor(3);
    cprintf("Enter password :: ");
    textcolor(15);
    gets(pass1);
    gotoxy(10, 11);
    delay(300);
    if (!(strcmp(pass, pass1) == 0))
    {
	gotoxy(20, 19);
	textcolor(5);
	cprintf("Invalid password");
	getch();
	clrscr();
	goto label;
    }
    gotoxy(20, 22);
    textcolor(5);
    cprintf("Correct password ");
    delay(1000);
    textmode(C80);
}

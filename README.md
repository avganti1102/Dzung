#include<stdio.h>
#include<math.h>
#include<conio.h>
#include<string.h>
#include<stdlib.h>

struct HS{
	char Sohieu[9];
	char Hoten[26];
	float diem;
};

int main()
{
	HS KQ[100]; int n;
	char S[9];
	for (n=0; n<=100;n++)
		{
			printf("Nhap so hieu: ");
			fflush(stdin);gets(S);
			if(strcmp(S," ")==0)break;
			strcpy(KQ[n].Sohieu,S);
			printf("Ho va ten: ");
			fflush(stdin);gets(KQ[n].Hoten);
			printf("Diem: ");scanf("%f",&KQ[n].diem);
		}
	//Sap xep lai mang
	for(int i=0;i<n-1;i++)
		for(int j=n-1;j>i;j++)
			if(KQ[j].diem>KQ[j-1].diem)
			{
				HS tg;
				tg=KQ[j];
				KQ[j]=KQ[j-1];
				KQ[j-1]=tg;
			}
	//Luu bang diem vao tep v.b
	FILE *v;
	v = fopen("sodiem.txt","wt");
	if(v==NULL)
	{
		printf("Loi mo tep...!!");
		exit(1);
	}
	printf("STT      So hieu       Ho ten      Diem:\n");
	for(int i=0;i<n;i++)
		fprintf(v,"%3d %10s %-28s %5.1f\n",i+1,KQ[i].Sohieu,KQ[i].Hoten,KQ[i].diem);
		fclose(v);
	printf("Duyet tep:\n");
	//duyet tep
	v = fopen("sodiem.txt","rt");
	if(v==NULL)
	{
		printf("Loi mo tep!!");exit(1);
	}
	int d8=0; HS tg; int b;
	fscanf(v,"%d%s%s%f",&b,tg.Sohieu,tg.Hoten,tg.diem);
	if(tg.diem>8){
		printf("%3d%10s%-28s%5.1f",b,tg.Sohieu,tg.Hoten,tg.diem);
		//d8++;
		
	}
	
	fclose(v);
	printf("So hoc sinh co diem >8: %d",d8);
	return 0;
}

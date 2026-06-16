# jogos-em-C
## PONG

```PONG
#include<stdio.h>
#include<windows.h>
#include<conio.h>

int main(){
SetConsoleOutputCP(65001);
int tecla=0;
int y1=1, y2=1;
int largura=25, comprimento=120;
int xb=comprimento/2, yb=largura/2;
int xd=1, yd=1;
int p1=0, p2=0;
int velocidade=67;
int aleatorio;
srand(time(NULL));

printf("\033[%d;%dH", 10, 43);
printf(" _______   _______    _      .   ______ ");
printf("\033[%d;%dH", 11, 43);
printf("|   __  | |   _   |  | |     |  |       ");
printf("\033[%d;%dH", 12, 43);
printf("|   ____| |  | |  |  |  |    |  |   ___ ");
printf("\033[%d;%dH", 13, 43);
printf("|  |      |  |_|  |  |   |   |  |      |");
printf("\033[%d;%dH", 14, 43);
printf("|__|      |_______|  |    |__|  |______|");

printf("\033[%d;%dH", 20, 50);
printf("Aperte enter para começar");
printf("\033[?25l");

while(tecla!=13){
tecla=getch();
}
system("cls");

while(1){
//jogadores 1 e 2 desenhar
for (int i=0; i<=5; i++){
printf("\033[%d;%dH",y1+i, 1);
printf("|");
}
for (int i=0; i<=5; i++){
printf("\033[%d;%dH",y2+i, comprimento);
printf("|");
}

if (kbhit()){
tecla = getch();

//tecla w
if(tecla==119 && y1>1){
printf("\033[%d;%dH",y1+5, 1);
printf(" ");
y1--;
}
//tecla s
if(tecla==115 && y1<largura){
printf("\033[%d;%dH",y1, 1);
printf(" ");
y1++;
}

//jogador 2
if (tecla == 224) {
tecla = getch();

//tecla cima
if(tecla==72 && y2>1){
printf("\033[%d;%dH",y2+5, comprimento);
printf(" ");
y2--;
}
//tecla baixo
if(tecla==80 && y2<largura){
printf("\033[%d;%dH",y2, comprimento);
printf(" ");
y2++;
}}
}

//Bolinha
printf("\033[%d;%dH",yb, xb);
printf(" ");
yb+=yd;
xb+=xd;

//colisão com a parte de baixo da tela
if(yb==largura+5 || yb==largura+4){
yd=-1;
}

//colisão com a parte de cima da tela
if(yb==1 || yb==2){
yd=+1;
}

//colisão com a parte direita da tela
if(xb>=comprimento-1){
if(yb>=y2 && yb<y2+6){
if(velocidade>5){velocidade-=5;}
xd=-1;
if(rand()%2+1==1){
yd=1;	
} else{
yd=-1;
}
if(yb==y2 || yb==y2+5){xd--;}
} else{
//bolinha ultrapassa jogador 2
p1++;
xb=comprimento/2;
yb=largura/2;
xd=-1;
yd=1;
velocidade=67;
_sleep(500);
}}

//colisão com a parte esquerda da tela
if(xb<=2){
if(yb>=y1 && yb<y1+6){
if(velocidade>5){velocidade-=5;}
xd=1;
if(rand()%2+1==1){
yd=1;	
} else{
yd=-1;
}
if(yb==y1 || yb==y1+5){xd++;}
} else{
//bolinha ultrapassa jogador 1
p2++;
xb=comprimento/2;
yb=largura/2;
xd=1;
yd=1;
velocidade=67;
_sleep(500);
}}

printf("\033[%d;%dH",yb, xb);
printf("O");

//pontuação
printf("\033[%d;%dH", 1, comprimento/2);
printf("%d | %d", p1, p2);
_sleep(velocidade);
}}
```

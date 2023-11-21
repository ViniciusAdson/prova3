# prova3
Questão 1:
#include <stdio.h>
#include <string.h>

int romanos(char sigla){
   
   switch (sigla)
   {
        case 'I': return 1;
        case 'V': return 5;
        case 'X': return 10;
        case 'L': return 50;
        case 'C': return 100;
        case 'D': return 500;
        case 'M': return 1000;
        default: return 0;
   }
}

int function_RomanoParaDecimal(char *romano){
    int res = 0;
    for (int i = 0; romano[i]; i++) {
        if (romanosConstantes(romano[i]) < romanosConstantes(romano[i + 1])) {
            res-= romanosConstantes(romano[i]);
        } else {
            res+= romanosConstantes(romano[i]);
        }
    }

    return res;
}

void DecimalPara_binario(int decimal,char binario[]){
    binario[0] = '\0';

   while (decimal > 0) {
        char digito[2];
        sprintf(digito, "%d", decimal % 2);
        strcat(binario, digito);
        decimal = decimal / 2;
    }

    int tamanho= strlen(binario);
    for (int i = 0; i < tamanho / 2; i++) {
        char temp = binario[i];
        binario[i] = binario[tamanho - 1 - i];
        binario[tamanho - 1 - i] = temp;
    }
}

void Decimal_Para_Hexadecimal(int decimal, char hexadecimal[]){
   int i = 0,resto;
   hexadecimal[0] = '\0';
   
   while (decimal > 0) {
        resto = decimal % 16;
        char dig[2];
        if (resto < 10) {
            sprintf(dig,"%d",resto);
        } else {
             sprintf(dig, "%c", resto - 10 + 'a');
        }
        strcat(hexadecimal, dig);
        decimal = decimal / 16;
        i++;
    }
    int comprimento = strlen(hexadecimal);
    for (int i = 0; i < comprimento / 2; i++) {
        char temp = hexadecimal[i];
        hexadecimal[i] = hexadecimal[comprimento - 1 - i];
        hexadecimal[comprimento - 1 - i] = temp;
    }
}

int main(){
   char num_romano[15],binario[32], hexadecimal[100];
   int decimal;
   scanf("%s",num_romano); 
   decimal = function_RomanoParaDecimal(num_romano);
   DecimalPara_binario(decimal, binario);
   Decimal_Para_Hexadecimal(decimal,hexadecimal);
   printf("%s na base 2: %s\n",num_romano, binario);
   printf("%s na base 10: %d\n",num_romano, decimal);
   printf("%s na base 16: %s\n",num_romano, hexadecimal);
   return 0;
}


Questão 2

#include <stdio.h>
#include <math.h>

double calculoMontante(int mes, double aporte, double juros) {
    return aporte *(1 + juros) * (((pow(1 + juros,mes) - 1)/juros));
}

int main() {
    int nmeses;
    double aportemensal, taxajuros;

    scanf("%d", &nmeses);
    scanf("%lf", &aportemensal);
    scanf("%lf", &taxajuros);

    for (int i = 1; i <= nmeses; i++) {
        double montante = calculoMontante(i, aportemensal, taxajuros);
        printf("Montante ao fim do mes %d: R$ %.2f\n", i, montante);
    }
    return 0;
}

Questão 3

#include <stdio.h>
#include <string.h>
#include <ctype.h>

int validarPlaca(char *placa){  
   if (strlen(placa)==8){
      for (int i = 0; i < 3; i++){
        if (!isalpha(placa[i])){
            return 0;
        }
      }
      if (placa[3] != '-' || !isdigit(placa[4]) || !isdigit(placa[5]) || !isdigit(placa[6]) || !isdigit(placa[7])){
        return 0;
      } 
   }
   else if (strlen(placa)==7){
      for (int i = 0; i <3; i++){
         if (!isalpha(placa[i])){
           return 0;
         }
      }
      if (!isdigit(placa[3]) || !isalpha(placa[4]) || !isdigit(placa[5]) || !isdigit(placa[6])){
        return 0;
      }
   }
   else{
      return 0;
   }
   return 1;
}

int validacaoDiaSemana(char * dia){
   char *diasValidos[] = {"SEGUNDA-FEIRA", "TERCA-FEIRA", "QUARTA-FEIRA", "QUINTA-FEIRA", "SEXTA-FEIRA", "SABADO", "DOMINGO"};
   for (int i = 0; i < 7; i++){
     if (strcmp(dia, diasValidos[i]) == 0){
        return 1;
     }
   }
   return 0;
}

int main(){
   char placa[10];
   char diaDaSemana[20];
   int marca = 0;
   scanf("%s",placa);
   scanf("%s",diaDaSemana); 
   if (!validarPlaca(placa)) {
        printf("Placa invalida\n"); 
        marca++;
    }
   if (!validacaoDiaSemana(diaDaSemana)) {
        printf("Dia da semana invalido\n");
        marca++;
    }
    if(marca>0){
     return 0;
    }
    else{
       for (int i = 0; i < strlen(diaDaSemana); i++) {
         diaDaSemana[i] = tolower(diaDaSemana[i]);
       }
    }
    int ultimoDigito = placa[strlen(placa) -  1]-'0';

    if(strcmp(diaDaSemana,"segunda-feira")==0 && (ultimoDigito==0||ultimoDigito==1 )){
          printf("%s nao pode circular %s\n",placa,diaDaSemana);
    }
    else if(strcmp(diaDaSemana,"terca-feira")==0 && (ultimoDigito==2||ultimoDigito==3)){
          printf("%s nao pode circular %s\n",placa,diaDaSemana);
    }
     else if(strcmp(diaDaSemana,"quarta-feira")==0 && (ultimoDigito==4||ultimoDigito==5)){
          printf("%s nao pode circular %s\n",placa,diaDaSemana);
     }
     else if(strcmp(diaDaSemana,"quinta-feira")==0 && (ultimoDigito==6||ultimoDigito==7)){
          printf("%s nao pode circular %s\n",placa,diaDaSemana);
     }
     else if(strcmp(diaDaSemana,"sexta-feira")==0 && (ultimoDigito==8||ultimoDigito==9)){
          printf("%s nao pode circular %s\n",placa,diaDaSemana);
     }
     else if(strcmp(diaDaSemana,"sabado")==0 || strcmp(diaDaSemana,"domingo")==0){
      printf("Nao ha proibicao no fim de semana\n");
     }
     else{
      printf("%s pode circular %s\n", placa, diaDaSemana);
     }

    return 0;
}

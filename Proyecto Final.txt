# include <stdlib.h>
# include <conio.h>
# include <stdio.h>
# include <string.h>
# include <iostream>


typedef 
 char string[50];

//INICIO Declaracion del vector
struct caja{
string x;
string apellido;
int cedula;
};

typedef caja vector; 

caja arreglo[100];
//FIN declaracion del vector


struct principal{
 string valor;
 struct principal*prox;
 struct secundario*sig;
};principal;

principal*p1=NULL;

struct secundario {
string x;
string apellido;
int cedula;
int dianaci;
int mesnaci;
int anonaci;
string ciunaci;
string ciuresi;
int diamue;
int mesmue;
int anomue;
struct secundario*prox;
};secundario;
secundario*p2=NULL;


void crear2(principal*p1,int m,FILE **archi){
string a;
int n;
 secundario*nuevo=NULL;
 secundario*aux=NULL;
 principal*aux2=p1;
 while (aux2->prox!=NULL) 
	 aux2=aux2->prox;
  for (int j=0;j<m;j++){
    nuevo= (secundario *)malloc(sizeof(secundario));
	nuevo->prox=NULL;
	fgets(a,25,*archi);       //     printf("Indique nombre del habitante\n");
	strcpy(nuevo->x,a);
	fgets(a,25,*archi);       //     printf("Indique apellido del habitante\n");
	strcpy(nuevo->apellido,a);
	fgets(a,25,*archi);       // 	   printf("Indique cedula del habitante\n");
    n=atoi(a);
    nuevo->cedula=n;
	fgets(a,25,*archi);       // 	   printf("Indique dia de nacimiento del habitante\n");
    n=atoi(a);
	nuevo->dianaci=n;
	fgets(a,25,*archi);       // 	   printf("Indique mes de nacimiento del habitante\n");
    n=atoi(a);
	nuevo->mesnaci=n;
	fgets(a,25,*archi);       // 	   printf("Indique ano de nacimiento del habitante\n");
    n=atoi(a);
	nuevo->anonaci=n;
    fgets(a,25,*archi);       //     printf("Indique ciudad de nacimiento del habitante\n");
	strcpy(nuevo->ciunaci,a);
	fgets(a,25,*archi);       //     printf("Indique ciudad de residencia del habitante\n");
	strcpy(nuevo->ciuresi,a);
	fgets(a,25,*archi);       // 	   printf("Indique dia de defuncion del habitante\n");
    n=atoi(a);
	nuevo->diamue=n;
	fgets(a,25,*archi);       // 	   printf("Indique mes de defuncion del habitante\n");
    n=atoi(a);
	nuevo->mesmue=n;
	fgets(a,25,*archi);       // 	   printf("Indique ano de defuncion del habitante\n");
    n=atoi(a);
	nuevo->anomue=n;
    if (j==0){
	  aux=nuevo;
	  aux2->sig=nuevo;
	 }
	 else{
	  while (aux->prox!=NULL)
	   aux=aux->prox;
       aux->prox=nuevo;	 
	 }
  }
  }
void crear1(principal**p1){
string a;
int m;
int n;
principal*aux=NULL;
principal*nuevo=NULL;
string ruta;
FILE *archi=NULL;
printf("Indique ruta del archivo\n");
scanf("%s",ruta);
archi=fopen(ruta,"r");
if (!(archi=fopen(ruta,"r"))){
   printf("Error el archivo no existe");
   system("PAUSE");
}
else{
  fgets(a,25,archi);
  n=atoi(a);
  //printf("%i",n);
  //printf("\n");
  for(int i=0;i<n;i++){
    nuevo= (principal *)malloc(sizeof(principal));
	nuevo->prox=NULL;
	nuevo->sig=NULL;
	fgets(a,25,archi);
	strcpy(nuevo->valor,a);
	if (i==0){
	  aux=nuevo;
	  *p1=nuevo;
	}
	else {
	  while (aux->prox!=NULL)
	    aux=aux->prox;
     aux->prox=nuevo;
	}
  fgets(a,25,archi);
  m=atoi(a);
 if (m!=0)
  crear2(*p1,m,&archi);
  }
}
/*printf(*archi);
system("PAUSE");*/
fclose(archi);
}

void imprimir (principal*p1){
principal*aux=p1; 
while (aux!=NULL){
	printf("Nombre de la Ciudad: ");
	printf("%s\n",aux->valor);
	printf("Habitante(s):\n");
	printf("\n");
	  secundario*aux2=aux->sig;
      while (aux2!=NULL){
		printf("Nombre: %s",aux2->x);
		printf("Apellido: %s",aux2->apellido);
		printf("Cedula : %i\n",aux2->cedula);
        printf("Fecha de Nacimiento: ");
		printf("%i",aux2->dianaci);
		printf("/%i",aux2->mesnaci);
		printf("/%i\n",aux2->anonaci);
		printf("Ciudad de Nacimiento: %s",aux2->ciunaci);
		printf("Ciudad de Resindencia: %s",aux2->ciuresi);
		printf("Fecha de Defuncion: ");
		printf("%i",aux2->diamue);
		printf("/%i",aux2->mesmue);
		printf("/%i\n",aux2->anomue);
		printf("\n");
		printf("\n");
	   aux2=aux2->prox;
	  }
	 aux=aux->prox;
  } 
system("PAUSE");
}

void crearciudad(principal*p1){
string ciu;
char salto[5]="\n";
int x;
principal *aux=p1;
printf("Indique Nombre de la Ciudad a Crear\n");
scanf("%s",&ciu);
strcat(ciu,salto); 
while ((strcmp(ciu,aux->valor)!=0)&&(aux->prox!=NULL))  //FALTA AGREGAR SALTO DE LINEA A CIUDAD
 aux=aux->prox;
if (strcmp(ciu,aux->valor)==0){
 printf("Error, la ciudad indicada ya existe\n");
 system("PAUSE");
}
else{ 
 aux=p1;
 principal *nuevo=(principal *)malloc(sizeof(principal));
 nuevo->prox=NULL;
 nuevo->sig=NULL; 
 strcpy(nuevo->valor,ciu);
 while (aux->prox!=NULL)
	 aux=aux->prox;
 aux->prox=nuevo;
}
}

int bciu(principal *p1, string ciu){
principal *aux=p1;
 while (aux!=NULL){
  if (strcmp(aux->valor,ciu)==0)
	  break;
 aux=aux->prox;
 }
 if (aux==NULL)
	 return (0);
 else
	 return(1);
}


int bhabi(principal *p1,string ciu, int cedu){
principal *aux=p1;
 while (strcmp(aux->valor,ciu)!=0)
  aux=aux->prox;
 secundario *aux2=aux->sig;
  if (aux2==NULL)
	return (1);
  while (aux2!=NULL){
   if (aux2->cedula==cedu)
	   break;
   aux2=aux2->prox;
  }
  if (aux2==NULL)
	  return(1);
  else
	  return(0);
}


void mudar(principal**p1, string ciu1, string ciu2, int &cedu){
principal *aux=*p1;
secundario *aux2=NULL;
 while (strcmp(aux->valor,ciu1)!=0)
	 aux=aux->prox;
 aux2=aux->sig;
 secundario *nuevo=(secundario *)malloc(sizeof(secundario));
 nuevo->prox=NULL;
 if (aux2->cedula==cedu){
	strcpy(nuevo->x,aux2->x);
	strcpy(nuevo->apellido,aux2->apellido);
	nuevo->cedula=aux2->cedula;
	nuevo->dianaci=aux2->dianaci;
	nuevo->mesnaci=aux2->mesnaci;
	nuevo->anonaci=aux2->anonaci;
	strcpy(nuevo->ciunaci,aux2->ciunaci);
	strcpy(nuevo->ciuresi,ciu2);
	nuevo->diamue=aux2->diamue;
	nuevo->mesmue=aux2->mesmue;
	nuevo->anomue=aux2->anomue;
	secundario *t=aux2;
	aux->sig=aux2->prox;
	delete(t);
 }
 else{
	while (aux2->prox->cedula!=cedu)
		aux2=aux2->prox;
	strcpy(nuevo->x,aux2->prox->x);
    strcpy(nuevo->apellido,aux2->prox->apellido);
	nuevo->cedula=aux2->prox->cedula;
	nuevo->dianaci=aux2->prox->dianaci;
	nuevo->mesnaci=aux2->prox->mesnaci;
	nuevo->anonaci=aux2->prox->anonaci;
	strcpy(nuevo->ciunaci,aux2->prox->ciunaci);
	strcpy(nuevo->ciuresi,ciu2);
	nuevo->diamue=aux2->prox->diamue;
	nuevo->mesmue=aux2->prox->mesmue;
	nuevo->anomue=aux2->prox->anomue;
	secundario *t=aux2->prox;
	aux2->prox=aux2->prox->prox;
	delete(t);
 }
aux=*p1;
	while (strcmp(aux->valor,ciu2)!=0)
		aux=aux->prox;
	aux2=aux->sig;
	if (aux2==NULL)
		aux->sig=nuevo;
	else{
	while (aux2->prox!=NULL)
		aux2=aux2->prox;
	aux2->prox=nuevo;
	}
}

void crearhabi(principal*p1,string ciu){
principal *aux=p1;
string cadena;
char salto[3]="\n";
int num;
int cont=0;
while (aux!=NULL){
  if(strcmp(ciu,aux->valor)==0){
   cont=1;
   if (aux->sig==NULL){
     printf("Indique el Nombre del Habitante\n");
     scanf("%s",&cadena);
	 strcat(cadena,salto);
	 secundario *nuevo=(secundario *)malloc(sizeof(secundario));
     nuevo->prox=NULL;
     strcpy(nuevo->x,cadena);
     printf("Indique el Apellido del Habitante\n");
     scanf("%s",&cadena);
	 strcat(cadena,salto);
	 strcpy(nuevo->apellido,cadena);
	 printf("Indique Cedula del Habitante\n");
     scanf("%i",&num);
	 nuevo->cedula=num;
     printf("Indique Dia de Nacimiento del Habitante\n");
     scanf("%i",&num);
	 nuevo->dianaci=num;
	 printf("Indique Mes de Nacimiento del Habitante\n");
     scanf("%i",&num);
	 nuevo->mesnaci=num;
	 printf("Indique Ano de Nacimiento del Habitante\n");
     scanf("%i",&num);
	 nuevo->anonaci=num;
	 printf("Indique el Ciudad de Nacimiento del Habitante\n");
     scanf("%s",&cadena);
	 strcat(cadena,salto);
	 strcpy(nuevo->ciunaci,cadena);
     strcpy(nuevo->ciuresi,ciu);
	 nuevo->diamue=0;
	 nuevo->mesmue=0;
	 nuevo->anomue=0;
	 aux->sig=nuevo;
   }
   else{
   secundario *aux2=aux->sig;
   printf("Indique el Cedula del Habitante\n");
   scanf("%i",&num);
    while ((aux2->cedula!=num)&&(aux2->prox!=NULL))
      aux2=aux2->prox;
	if (aux2->cedula==num){
      printf("ERROR EL HABITANTE YA EXISTE\n");
	  system("PAUSE");
	}
	else{
     secundario *nuevo=(secundario *)malloc(sizeof(secundario));
     nuevo->prox=NULL;
     printf("Indique el Nombre del Habitante\n");
     scanf("%s",&cadena);
	 strcat(cadena,salto);
     strcpy(nuevo->x,cadena);
     printf("Indique el Apellido del Habitante\n");
     scanf("%s",&cadena);
	 strcat(cadena,salto);
	 strcpy(nuevo->apellido,cadena);
	 nuevo->cedula=num;
     printf("Indique Dia de Nacimiento del Habitante\n");
     scanf("%i",&num);
	 nuevo->dianaci=num;
	 printf("Indique Mes de Nacimiento del Habitante\n");
     scanf("%i",&num);
	 nuevo->mesnaci=num;
	 printf("Indique Ano de Nacimiento del Habitante\n");
     scanf("%i",&num);
	 nuevo->anonaci=num;
	 printf("Indique el Ciudad de Nacimiento del Habitante\n");
     scanf("%s",&cadena);
	 strcat(cadena,salto);
	 strcpy(nuevo->ciunaci,cadena);
	 strcpy(nuevo->ciuresi,ciu);
	 nuevo->diamue=0;
	 nuevo->mesmue=0;
	 nuevo->anomue=0;
     aux2->prox=nuevo;
	}
   }
  }
  aux=aux->prox;
}
if (cont!=1){
	  printf("Error no existe la ciudad %s \n",ciu);
      system("PAUSE");
 }
}

void mhabi(principal *p1){
principal *aux=p1;
string ciu;
char salto[3]="\n";
printf("Indique Ciudad de Residencia del Habitante\n");
scanf("%s",&ciu);
strcat(ciu,salto);
 if (bciu(p1,ciu)==1){
 int cedu;
  printf("Indique Cedula del Difunto\n");
  scanf("%i",&cedu);
  if (bhabi(p1,ciu,cedu==0)){
  int a;
  secundario*aux2=NULL;
    while (strcmp(aux->valor,ciu)!=0)
		aux=aux->prox;
	aux2=aux->sig;
	while(aux2->cedula!=cedu)
	 aux2=aux2->prox;
	if (aux2->diamue==0){
	printf("Indique Dia de Defuncion del Habitante\n");
    scanf("%i",&a);
	aux2->diamue=a;
    printf("Indique Mes de Defuncion del Habitante\n");
    scanf("%i",&a);
	aux2->mesmue=a;
	printf("Indique Ano de Defuncion del Habitante\n");
    scanf("%i",&a);
	aux2->anomue=a;
	}
	else{
	printf("ERROR el Habitante ya Posee Fecha de Defuncion\n");
	system("PAUSE");
	}
  }
  else{
  printf("ERROR el Habitante no Existe\n");
  system("PAUSE");
  }
 }
else{
  printf("ERROR la Ciudad no Existe\n");
  system("PAUSE");
}
}

void imprimevector(vector arreglo[],int n){
	printf("Los Habitante(s) que Cumplen Ambas Condiciones Son:\n");
	//printf("%i",n);
   for (int i=0;i<n;i++){
	    printf("Nombre: %s",arreglo[i].x);
		printf("Apellido: %s",arreglo[i].apellido);
		printf("Cedula : %i\n",arreglo[i].cedula);
		printf("\n\n");
   }
}
void eliciu(principal *&p1,string ciu){

    	if (bciu(p1,ciu)==1){ // entra si hay ciudad
			  principal *aux=p1;
			  principal *auxciu2=p1;
			  secundario *aux2=NULL;  // recorrer y matar a los muertos antes de mudar 
              secundario *b=NULL;	

              while (strcmp(aux->valor,ciu)!=0) // para encontrar la ciudad IMPORTANTE ACTUALIZAR EL PUNTEROO!!! 
				  aux=aux->prox;
			  aux2=aux->sig;

			  while (aux2!=NULL) { // ya no es el primero
				if (aux2->prox!=NULL){  
				  if (aux2->prox->diamue!=0){ // esta muerta	
				    b=aux2->prox;
					aux2->prox=b->prox;
					delete(b);
				     if (aux2->prox==NULL)
					    break; 
				  }
				  else
					 if (aux2->prox->prox==NULL)
						 break;
					 else
						 aux2=aux2->prox;
				  }
				  else
				   break;
			  }
			  aux2=aux->sig;
				 
			  if (aux2->diamue!=0){ // es el primero 
			     
				  b=aux2;
				  aux2=aux2->prox;
				  aux->sig=aux2;
				  delete(b);
			  }
				 aux=p1;
			  if (strcmp(aux->valor,ciu)==0){  //la ciudad a eliminar es la primera 
			    auxciu2=aux->prox;
				aux2=aux->sig;
				if (aux2!=NULL)   //la ciudad no esta vacia 
				  while (aux2!=NULL){
	                secundario *nuevo=(secundario *)malloc(sizeof(secundario));
					nuevo->prox=NULL;
					strcpy(nuevo->x,aux2->x);
					strcpy(nuevo->apellido,aux2->apellido);
					nuevo->cedula=aux2->cedula;
					nuevo->dianaci=aux2->dianaci;
					nuevo->mesnaci=aux2->mesnaci;
					nuevo->anonaci=aux2->anonaci;
					strcpy(nuevo->ciunaci,aux2->ciunaci);
					strcpy(nuevo->ciuresi,auxciu2->valor); 
					nuevo->diamue=aux2->diamue;
					nuevo->mesmue=aux2->mesmue;
					nuevo->anomue=aux2->anomue;
					secundario *t=aux2;
					aux->sig=aux2->prox;
					aux2=aux2->prox;
					delete(t);		
					nuevo->prox=auxciu2->sig;
					auxciu2->sig=nuevo;
				  }
				  p1=p1->prox;
				  delete(aux);
			  }
			  else{
			  while (strcmp(aux->prox->valor,ciu)!=0)
				  aux=aux->prox;
			  if (aux->prox->prox==NULL)
				  auxciu2=p1;
			  else 
				  auxciu2=aux->prox->prox;// ya tengo la ciudad 1 y la ciudad 2
			  aux2=aux->prox->sig;   //parando aux2 en el primer habitante de la ciudad a eliminar 
			  if (aux2!=NULL)   //la ciudad no esta vacia 
				  while (aux2!=NULL){
	                secundario *nuevo=(secundario *)malloc(sizeof(secundario));
					nuevo->prox=NULL;
					strcpy(nuevo->x,aux2->x);
					strcpy(nuevo->apellido,aux2->apellido);
					nuevo->cedula=aux2->cedula;
					nuevo->dianaci=aux2->dianaci;
					nuevo->mesnaci=aux2->mesnaci;
					nuevo->anonaci=aux2->anonaci;
					strcpy(nuevo->ciunaci,aux2->ciunaci);
					strcpy(nuevo->ciuresi,auxciu2->valor);
					nuevo->diamue=aux2->diamue;
					nuevo->mesmue=aux2->mesmue;
					nuevo->anomue=aux2->anomue;
					secundario *t=aux2;
					aux->prox->sig=aux2->prox;
					aux2=aux2->prox;
					delete(t);		
					nuevo->prox=auxciu2->sig;
					auxciu2->sig=nuevo;
				  }//deberia mudar todos sus habitantes...
				  aux->prox=aux->prox->prox;
			  }
			} //si la ciudad existe
			}

void ordena (vector arreglo[], int n) {
int menor;
int pos;
caja aux;
 for (int i=0;i<n;i++){
  menor=arreglo[i].cedula;
  pos=i;
  for (int j=i+1;j<n;j++){ 
	 if (arreglo[j].cedula<menor) {
	  menor=arreglo[j].cedula;
	  pos=j;
	 }
  }
 aux.cedula=arreglo[i].cedula;
 strcpy(aux.apellido,arreglo[i].apellido);
 strcpy(aux.x,arreglo[i].x);
 arreglo[i].cedula=menor;
 strcpy(arreglo[i].apellido,arreglo[pos].apellido);
 strcpy(arreglo[i].x,arreglo[pos].x);
 arreglo[pos].cedula=aux.cedula;
 strcpy(arreglo[pos].apellido,aux.apellido);
 strcpy(arreglo[pos].x,aux.x);
}
}

void reque1(principal *p1,vector arreglo[]){
 principal *aux=p1;
 int cont=0;
 int cont2=0;
 char salto[3]="\n";
 secundario *aux2=NULL;
 string ciux;
 string ciuy;
 printf("Indique Nombre de Ciudad de Nacimientos \n");
 scanf("%s",ciux);
 strcat(ciux,salto);
 //if(bciu(p1,ciux)==1){
   printf("Indique Nombre de Ciudad de Residencia\n");
   scanf("%s",ciuy);
   strcat(ciuy,salto);
   int i=0;
   if (bciu(p1,ciuy)==1){
	 while(strcmp(aux->valor,ciuy)!=0)
		 aux=aux->prox;
     aux2=aux->sig;
	 while(aux2!=NULL){
     if (strcmp(aux2->ciunaci,ciux)==0){
	   cont=cont+1;
	   strcpy(arreglo[i].x,aux2->x);
	   strcpy(arreglo[i].apellido,aux2->apellido);
	   arreglo[i].cedula=aux2->cedula;
	   i=i+1;
	 }
	 aux2=aux2->prox;
	 }
   }
   else{
     printf("ERROR no existe la ciudad %s\n",ciuy);
	 system("PAUSE");
   }
/*}
 else{
	 cont2=1;
	 printf("ERROR no existe la ciudad %s\n",ciux);
	 system("PAUSE");
 }*/
 if (cont!=0){
	 printf("\n");
	 ordena(arreglo,cont);
     imprimevector(arreglo,cont);
	 system("PAUSE");
 }
 else
	 if (cont!=1){
	   printf("No Existe Ningun Habitante que Cumpla Ambas Condiciones\n",ciux);
	   system("PAUSE");
	 }
}

void reque2(principal *p1,vector arreglo[]){
 principal *aux=p1;
 int cont2=0;
 int cont=0;
 char salto[3]="\n";
 secundario *aux2=NULL;
 string ciux;
 printf("Indique Nombre de Ciudad de Nacimientos y Fallecimientos \n");
 scanf("%s",ciux);
 strcat(ciux,salto);
 if(bciu(p1,ciux)==1){
   int i=0;
	 while(strcmp(aux->valor,ciux)!=0)
		 aux=aux->prox;
     aux2=aux->sig;
	 while(aux2!=NULL){
     if (strcmp(aux2->ciunaci,ciux)==0)
	  if (aux2->diamue!=0){
	   cont=cont+1;
	   strcpy(arreglo[i].x,aux2->x);
	   strcpy(arreglo[i].apellido,aux2->apellido);
	   arreglo[i].cedula=aux2->cedula;
	   i=i+1;
	 }
	  aux2=aux2->prox;
	 }
 }
 else{
	 cont2=1;
	 printf("ERROR no existe la ciudad %s\n",ciux);
	 system("PAUSE");
 }
 if (cont!=0){
	 printf("\n");
	 ordena(arreglo,cont);
     imprimevector(arreglo,cont);
	 system("PAUSE");
 }
 else
	 if (cont2!=1){
	   printf("No Existe Ningun Habitante que Cumpla Ambas Condiciones\n",ciux);
	   system("PAUSE");
	 }
}


void reque3(principal *p1,vector arreglo[]){
 principal *aux=p1;
 int cont=0;
 int cont2=0;
 char salto[3]="\n";
 secundario *aux2=NULL;
 string ciux;
 printf("Indique Nombre de Ciudad de Nacimientos y Residencia \n");
 scanf("%s",ciux);
 strcat(ciux,salto);
 if(bciu(p1,ciux)==1){
   int i=0;
	 while(strcmp(aux->valor,ciux)!=0)
		 aux=aux->prox;
     aux2=aux->sig;
	 while(aux2!=NULL){
     if (strcmp(aux2->ciunaci,ciux)==0){
		 if (aux2->diamue==0){
		 cont=cont+1;
	   strcpy(arreglo[i].x,aux2->x);
	   strcpy(arreglo[i].apellido,aux2->apellido);
	   arreglo[i].cedula=aux2->cedula;
	   i=i+1;
		 }
	 }
	 aux2=aux2->prox;
	 }
 }
 else{
	 cont2=1;
	 printf("ERROR no existe la ciudad %s\n",ciux);
	 system("PAUSE");
 }
 if (cont!=0){
	 printf("\n");
	 ordena(arreglo,cont);
     imprimevector(arreglo,cont);
	 system("PAUSE");
 }
 else{
	 if (cont2!=1){
	   printf("No Existe Ningun Habitante que Cumpla Ambas Condiciones\n",ciux);
	   system("PAUSE");
	 }
 }
}


void salida (principal *p1){
 principal *aux=p1;
 secundario *aux2=NULL;
 int contciu=0;
 int conthabi=0;
 FILE *archi;
 archi=fopen("g:\coco.txt","w");
 if (aux!=NULL)
 while(aux!=NULL){
  contciu++;
  aux=aux->prox;
 }
 fprintf(archi,"%i\n",contciu);
 aux=p1;
 for (int i=0;i<contciu;i++){
    fprintf(archi,"%s",aux->valor);
    aux2=aux->sig;
    conthabi=0;
	 while(aux2!=NULL){
		 conthabi++;
		 aux2=aux2->prox;
	 }
    fprintf(archi,"%i\n",conthabi);
	 aux2=aux->sig;
   
	 for(int j=0;j<conthabi;j++){
	  fprintf(archi,"%s",aux2->x);
	  fprintf(archi,"%s",aux2->apellido);
	  fprintf(archi,"%i\n",aux2->cedula);
	  fprintf(archi,"%i\n",aux2->dianaci);
	  fprintf(archi,"%i\n",aux2->mesnaci);
	  fprintf(archi,"%i\n",aux2->anonaci);
	  fprintf(archi,"%s",aux2->ciunaci);
	  fprintf(archi,"%s",aux2->ciuresi);
      fprintf(archi,"%i\n",aux2->diamue);
	  fprintf(archi,"%i\n",aux2->mesmue);
	  fprintf(archi,"%i\n",aux2->anomue);
	  aux2=aux2->prox;
   }
	aux=aux->prox;

 }
 
 fclose(archi);
}
  

 
void main(){
int opc=10;
string ciu;
char salto[3]="\n";
int n;
while (opc!=0){
system ("cls");
printf("        MENU               \n");
printf("\n");
printf("  0.- SALIR\n");
printf("  1.- CARGAR\n");
printf("  2.- IMPRIMIR\n");
printf("  3.- CREAR CIUDAD\n");
printf("  4.- REGISTRAR NACIMIENTO\n");
printf("  5.- MUDAR HABITANTE\n");
printf("  6.- ELIMINAR CIUDAD\n");
printf("  7.- REGISTRO DE FALLECIMIENTO\n");
printf("\n\n");
printf("       CONSULTAS\n");
printf("\n");
printf(" 8.- Mostrar Habitantes Nacidos en una Ciudad X y Resindenciados en una Ciudad Y");
printf(" 9.- Mostrar Habitantes Nacidos y Fallecidos en una Misma Ciudad X\n");
printf(" 10.- Mostrar Habitantes Nacidos y Residenciados en una Misma Ciudad X\n");
scanf("%i",&opc);
switch ( opc ){

	    case 0:
			salida(p1);
			break;
	    case 1:
			system ("cls");
			crear1(&p1);
			break;
		case 2:
			system ("cls");
			imprimir(p1);
			break;
		case 3:
			system ("cls");
			crearciudad(p1);
			break;
		case 4:
			system ("cls");
			printf("Indique la Ciudad donde se Creara Habitante\n");
			scanf("%s",&ciu);
			strcat(ciu,salto);
			crearhabi(p1,ciu);
			break;
		case 5:
		    string ciu1;
			string ciu2;
			int cedu;
			system ("cls");
			printf("Indique Nombre de la Ciudad de Residencia del Habitante\n");
			scanf("%s",&ciu1);
			strcat(ciu1,salto);
			if (bciu(p1,ciu1)==1){
			 printf("Indique el Nombre de la Nueva Ciudad de Residencia del Habitante\n");
			  scanf("%s",&ciu2);
			  strcat(ciu2,salto);
			  if (bciu(p1,ciu2)==1){
				   printf("Indique la Cedula del Habitante \n");
				   scanf("%i",&cedu);
				  if (bhabi(p1,ciu1,cedu)==1){
					printf("ERROR EL HABITANTE NO EXISTE\n");
				    system("PAUSE");
				  }
				else{
					mudar(&p1,ciu1,ciu2,cedu);
				}
			  }
			  else{
				printf("NO EXISTE LA CIUDAD %s",ciu2);
				system("PAUSE");
				}
			}
			else{
			 printf("NO EXISTE LA CIUDAD %s",ciu1);
			 system("PAUSE");
			}
			 break;
		case 6:
			system ("cls");
		    string ciu;
			printf("Indique el Nombre de la Ciudad a Eliminar\n");
			scanf("%s",&ciu);
			strcat(ciu,salto);
			if (bciu(p1,ciu)==1){ // entra si hay ciudad
			  principal *aux=p1;      
			  if (strcmp(aux->valor,ciu)==0){ // si es la primera ciudad
				  if(aux->sig==NULL){  // si la ciudad esta vacia
				  principal *b=aux;
				  p1=aux->prox;
				  delete(b);
				}
				  else{
					eliciu(p1,ciu);
				  }
			  }
			  else{
			  while (strcmp(aux->prox->valor,ciu)!=0) // para encontrar la ciudad IMPORTANTE ACTUALIZAR EL PUNTEROO!!! 
				 aux=aux->prox;
			   if(aux->prox->sig==NULL){
			     principal *b=aux->prox;
				 aux->prox=b->prox;
				 delete(b);
			   }
			   else
				 eliciu(p1,ciu);
			  }
			}
			else{
			printf("ERROR LA CIUDAD NO EXISTE");
			system("PAUSE");
			}
			break;
		case 7:
			system ("cls");   
			mhabi(p1);
			   break;
		case 8:
			system ("cls");   
			reque1(p1,arreglo);
			   break;
		case 9:
			system ("cls");   
			reque2(p1,arreglo);
			   break;
	    case 10:
			system ("cls");   
			reque3(p1,arreglo);
			   break;
		default:
			printf("ERROR opcion no valida\n");
			system("PAUSE");
			break;
		}
  }
}
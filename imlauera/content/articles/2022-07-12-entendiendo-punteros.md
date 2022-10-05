---
layout: post
title: Entendiendo Punteros
date: 2022-07-12 08:59 -0300
---

```c
#include <stdio.h>
#include <stdlib.h>

char *printLocalTime()
{
  char *timeStringBuff=malloc(30); //50 chars should be enough
  //char timeStringBuff[100]; //50 chars should be enough
  char *mic = "2022";
  char c = 'm';
  int test = 1;
  char prueba[50]; char *prueba_m = malloc(50);
  printf("%d\n",sizeof(prueba));
  printf("%d\n",sizeof(prueba_m));
  sprintf(timeStringBuff, "they tried everything %s %d\n",mic,test);
  //Optional: Construct String object
  // Esto retorna un puntero a la direccion de memoria en donde esta timeStringBuff
  // *timeStringBuff = timeStringBuff[0]
  // *(timeStringBuff+3) = timeStringBuff[3]
  printf("%s\n",timeStringBuff);
  // Vos no retornas la palabra cuando ejecutas return timeStringBufff retornas un puntero
  // que apunta a la primer letra del char. Y lo que hace el '%s' es leer hasta que encuentra el \0
  printf("%c\n",*timeStringBuff);
  char hola[] = {'h','o','l','a','\0'};
  printf("%s\n",hola);
  // Cambio valor
  for(int i=0; i<10000; i++){
    sprintf(timeStringBuff, "reincarnation");
  }
  printf("%s\n",timeStringBuff);
  if (c == 'm') printf("we're winning\n");
  
  return timeStringBuff;
}

int main()
{
    char *freeThis = printLocalTime();
    printf("%s\n",freeThis);
    free(freeThis);
    printf("%s\n",freeThis);
    int a = 65;
    printf("%c\n",(char)a);
    return 0;
}
```



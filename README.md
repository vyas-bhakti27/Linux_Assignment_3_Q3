

#include<stdio.h>
#include<pthread.h>
#include<stdlib.h>
//#include<sys/main.h>
#include<unistd.h>

void* proc(void* program)
{
sleep(2);
return 0;
}

int main()
{
pthread_attr_t ATTR;
pthread_t Id;
void *stk;
size_t siz;
int err;

size_t my_stksize=300000;
void * my_stacks;

pthread_attr_init(&ATTR);
pthread_attr_getstacksize(&ATTR,&siz);
pthread_attr_getstackaddr(&ATTR,&stk);

printf("Default: addr=%08x default size=%d\n",stk,siz);

my_stacks=(void*)malloc(my_stksize);

pthread_attr_setstack(&ATTR,my_stacks,my_stksize);
pthread_create(&Id,&ATTR,proc,NULL);
pthread_attr_getstack(&ATTR,&stk,&siz);

printf("newly defined stack :Addr=08%x  and size =%d\n",stk,siz);
sleep(3);
return (0);
}

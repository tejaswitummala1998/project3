# project3
#include <stdio.h>

#include <dirent.h>

#include<string.h>

int count=0;    //coutn stores the  numbe rof files encountered

//this fucntion simply prints the content of the array pased

void display(char *arr[])

{

    int i=0;

    for(i=0;i<count;i++){

        printf("%s\n",arr[i]);  

    }

}

//ascendign order comparator

int StringCompare(  void* a,  void* b)

{

    char  **char_a = a;

    char  **char_b = b;

    return strcmp(*char_a, *char_b);

}

//descending order comparator

int StringCompare1(  void* a,  void* b)

{

    char  **char_a = b;

    char  **char_b = a;

    return strcmp(*char_a, *char_b);

}

//stringout function

//if c is -f sorts in ascending

//if  c is -b sorts in descending

void stringout( char *str[],char *c)

{

    if(strcmp(c,"-f")==0)

        qsort( str, count, sizeof(char*), StringCompare);

    else if(strcmp(c,"-b")==0)

        qsort( str, count, sizeof(char*), StringCompare1);

}



int main(int argc, char *argv[])

{

    struct dirent *de;  // Pointer for directory entry

  

    // opendir() returns a pointer of DIR type.  

    DIR *dr = opendir(argv[1]);

  

    if (dr == NULL)  // opendir returns NULL if couldn't open directory

    {

        printf("Could not open current directory" );

        return 0;

    }

  

    //stores the file names

    char *c[100000];

    

     //readfiles

    while ((de = readdir(dr)) != NULL){

        c[count]=de->d_name;

        count++;

    }

  

    closedir(dr);

    //if argumnets passed has sort flag then call sort function

   if(argc>2){

    stringout(c,argv[2]);

    display(c);

   }

   else{

      display(c);

   }



    return 0;

}


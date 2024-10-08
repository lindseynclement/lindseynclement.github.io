---
layout: project
type: project
image: img/pokemon.webp
title: "Pokémon Database"
date: 2024-09-05
published: true
labels:
  - C
  - Database
  - Back-End Development
summary: "Building a database of Pokémon objects"
---

<div class="text-center p-4">
  <img width="400px" class="rounded float-start pe-4" src="../img/pokemon.webp">
</div>

The Pokémon database was a solo project I created in my Program Structure 3 class (ICS 212) at UH Mānoa, a class in which I learned the C and C++ coding languages. This project creates a database the user can interact with. The database holds Pokémon objects and, when prompted by the user, can add Pokémon to the database. Furthermore, it can read a list of Pokémon objects from a text file and import them into the database, as well as printing the current Pokémo in the database to a text file. This project was composed of four files that worked collaboratively: driver.c, iofunctions.c, iofunctions.h, and pokemon.h. 

The driver.c file is a file written in C that interacts with the user by prompting them to enter a Pokémon’s level and name. If the user provides a valid level and name, the Pokémon is added to the database. If the input is incorrect, an error message appears. The program will keep asking the user to add up to 5 Pokémon, saving each one in the pokemonbank. After each entry, the user is asked if they want to add another Pokémon (by entering 0 to continue or -1 to stop). If there’s any mistake in the input, the program will stop. Some code from the file can be seen below:

```cpp
while (stop != -1 && numpokemons < 5){
        printf("\nPlease insert new pokemon's level: ");
        if (scanf("%d", &pokemonbank[numpokemons].level) == 1){
            getchar();
            printf("\nPlease insert new pokemon's name: ");
            fgets(pokemonbank[numpokemons].name, sizeof(pokemonbank[numpokemons]).name , stdin);
            pokemonbank[numpokemons].name[strlen(pokemonbank[numpokemons].name)- 1] = '\0';
            numpokemons++;
            if (numpokemons < 5){
                printf("\nWould you like to input another pokemon? 0 for yes and -1 for no: ");
                if (scanf("%d", &choice) != 1){
                    printf("\nInvalid input\n");
                    stop = -1;
                    val = -1;
                }
                else if (choice != -1 && choice != 0){
                    printf("\nInvalid input\n");
                    stop = -1;
                    val = -1;
                }
                else if (choice == -1){
                    stop = -1;
                    val = 0;
                    valid = 0;
                }
            }
        }
        else{
            printf("\nInvalid input\n");
            stop = -1;
            val = -1;
        }
    }
```

The iofunctions.c file is also written in C and contains two methods writefile and readfile. Writefile prints the current contents of the database to a text file, and readfile reads Pokémon objects from a text file and imports them into the database. Here is some code from the iofunctions.c file that illustrates how a text file can be imported into the database:

```cpp
int readfile(struct pokemon pokearray[], int* num, char filename[])
{
    FILE *infile;
    int val;
    int count;

    count = 0;
    infile = fopen(filename, "r");

    if (infile != NULL){
        while (count < *num){
            if (fscanf(infile, "%d", &pokearray[count].level) != EOF){
                if (fscanf(infile, "%s", pokearray[count].name) != EOF){
                    count++;
                }
                else{
                    val = -1;
                }
            }
            else{
                val = -1;
            }
        }

        fclose(infile);
    }
    else{
        val = -1;
    }

    if (val != -1){
        writefile(pokearray, count, "in.txt");
        *num = count;
        val = 0;
    }
    return val;
}

```
In C programming, header files help keep code organized. The files iofunctions.h and pokemon.h are examples of header files. The iofunctions.h file contains the function prototypes for the readfile and writefile functions, while the pokemon.h file includes the pokemon structure that defines what a Pokémon is, such as its level and name. Below is the code found in pokemon.h:

```cpp
struct pokemon
{
    int level;
    char name[20];
};
```
This project taught me how to read and write to text files, which is essential for managing data efficiently. It also sharpened my database skills, particularly in organizing records. Overall, the project strengthened my ability to work with both data handling and file systems in C, which are both critical elements of software development.

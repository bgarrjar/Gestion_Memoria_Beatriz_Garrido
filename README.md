# Gestion_Memoria_Beatriz_Garrido

https://github.com/bgarrjar/Gestion_Memoria_Beatriz_Garrido.git

#include <sys/mman.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <sys/wait.h>

#define SIZE 4096

int main() {
    char *shared_memory = mmap(NULL, SIZE, PROT_READ|PROT_WRITE, MAP_SHARED|MAP_ANONYMOUS, -1, 0);
    if (shared_memory == MAP_FAILED) {
        perror("mmap");
        exit(EXIT_FAILURE);
    }
    
    pid_t pid = fork();
    
    if (pid < 0) {
        perror("fork");
        exit(EXIT_FAILURE);
    } else if (pid == 0) {
        printf("Child reads: %s\n", shared_memory);
        munmap(shared_memory, SIZE);
        exit(EXIT_SUCCESS);
    } else {
        strcpy(shared_memory, "Hello, child process!");
        wait(NULL);
        munmap(shared_memory, SIZE);
    }

    return 0;
}

# Resolución Paso a Paso

El programa da error al compilarlo en mi ordenador ya que el sistema operativo es Windows y el código está usando librerias que solo funcionan en Linux. Hay que descargarse un programa que haga que funcionen estas librerias en mi máquina. 

### 1. Instalación de Ubuntu a través del terminal en Clion
    Después de la instalación, me pide crear un usuario y contraseña y validar esa contraseña. 

### 2. Clonación del repositorio de Github:
    comando: git clone https://github.com/bgarrjar/Gestion_Memoria_Beatriz_Garrido.git

### 3. Actualización de la maquina virtual:
    comando: sudo apt update

### 4. Instalación compilador de C:
    Al contrario que en CLion, aquí me tengo que instalar el compilador gcc para que el programa se pueda compilar. 
    comando: sudo apt install gcc

### 5. Creación del ejecutable para poder ejecutar el main.c:
    Comando: gcc main.c -o main
    uso el comando ls para ver que está creado. 

### 6. Comprobación de que el ejecutable funciona: 
    Comando: ./ main
    Con este comando se ejecuta el programa obteniendo en la pantalla el siguiente mensaje: Child reads: Hello, child process!



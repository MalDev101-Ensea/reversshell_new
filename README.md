# reversshell_new
Ce projet contient deux fichiers permettant de réaliser un assembleur pour une shellcode de reverse shell en ASM et un injecteur en C.

## Contenu des fichiers

1. **`reverseshell.c`** : Ce fichier C exécute directement une shellcode pour un reverse shell. Il alloue de la mémoire exécutable, y copie le shellcode et l'exécute.

2. **`shellcode_reverseshell.asm`** : Ce fichier ASM contient une shellcode pour un reverse shell. Il utilise des appels système pour créer un socket, se connecter à un serveur, dupliquer les descripteurs de fichiers et exécuter `/bin/sh`.

## Instructions d'utilisation

### 1. Compilation de `reverseshell.c`

Pour compiler le fichier C, utilisez la commande suivante :


gcc  -z execstack  reverseshell.c -o reverseshell


### 2. Execution de `reverseshell.c`
./reverseshell


### 3.Assemblage de shellcode_reverseshell.asm
nasm -f elf32 -o shellcode_reverseshell.o shellcode_reverseshell.asm

### 4. Extraction du shellcode en format hexadécimal


ld -o shellcode_reverseshell shellcode_reverseshell.o
objcopy -O binary shellcode_reverseshell shellcode_reverseshell.bin
hexdump -v -e '"\\""x" 1/1 "%02x" ""' shellcode_reverseshell.bin


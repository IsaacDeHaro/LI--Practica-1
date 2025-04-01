# Practica 1: Ingresar un nombre

## Codigo:
```
// **************************************************************
// * Programa: Capturar y mostrar un nombre en ARM64 Assembly  *
// * Autor: DE HARO RAMIREZ ISAAC                                      *
// * Fecha: 01-04-2025                                      *
// * Descripción: El usuario ingresa un nombre y el programa   *
// *              lo muestra en pantalla.                      *
// **************************************************************

.section .data
    mensaje:    .asciz "Ingresa tu nombre: "
    salida:     .asciz "Hola, "

.section .bss
    .lcomm buffer, 100   // Reserva 100 bytes para almacenar el nombre

.section .text
    .global _start

_start:
    // Escribir mensaje de solicitud
    mov x0, 1          // File descriptor 1 (stdout)
    ldr x1, =mensaje   // Dirección del mensaje
    mov x2, 18         // Longitud del mensaje
    mov x8, 64         // syscall write
    svc 0              // Llamada al sistema

    // Leer nombre del usuario
    mov x0, 0          // File descriptor 0 (stdin)
    ldr x1, =buffer    // Dirección del buffer
    mov x2, 100        // Longitud máxima
    mov x8, 63         // syscall read
    svc 0              // Llamada al sistema

    // Escribir "Hola, "
    mov x0, 1          // File descriptor 1 (stdout)
    ldr x1, =salida    // Dirección del mensaje de saludo
    mov x2, 6          // Longitud del mensaje
    mov x8, 64         // syscall write
    svc 0              // Llamada al sistema

    // Escribir nombre del usuario
    mov x0, 1          // File descriptor 1 (stdout)
    ldr x1, =buffer    // Dirección del buffer
    mov x2, 100        // Longitud del nombre leído
    mov x8, 64         // syscall write
    svc 0              // Llamada al sistema

    // Salir del programa
    mov x8, 93         // syscall exit
    mov x0, 0          // Código de salida 0
    svc 0              // Llamada al sistema
```
## Asciinema
https://asciinema.org/a/EKFt61Zp2CDaHcGqPQnyufDms

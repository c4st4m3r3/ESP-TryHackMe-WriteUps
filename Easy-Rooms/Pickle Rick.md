# Writeup en español para la room de THM "Pickle Rick".
Como siempre en mis WriteUps, las flags están redactadas para que tengáis que realizar vosotros también los ejercicios :D\
Vamos a trabajar en ellos paso por paso así que ¡que nadie se preocupe!
```

ESTE WRITEUP ESTÁ EN PROCESO DE REDACCIÓN. ¡VUELVE PRONTO PARA PODER LEERLO!

```
## INTRODUCCIÓN:
En esta room de nivel principiante nos presentan una máquina con temática de Rick y Morty ¡¡WUBBA LUBBA DUB-DUB!!\
¡Rick se ha convertido en pepinillo! Necesitamos encontrar 3 flags en la máquina que serán los 3 ingredientes que Rick necesita para poder volver a reconvertirse en humano. ¡Vamos a ayudarle!

## PASO 1. ENUMERACIÓN:
Comenzamos arrancando la máquina. Dejemosle al menos 5 minutos para que pueda arrancar correctamente.\
Lo primero que haremos, como en la mayoría de casos será utilizar nmap para realizar un escaneo de los puertos que se encuentran abiertos así como de los servicios que se encuentran disponibles en la misma:

```
nmap -sV -p- IP.DE.NUESTRA.MÁQUINA
```

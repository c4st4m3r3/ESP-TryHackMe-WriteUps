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
Comenzamos arrancando la máquina. Démosle al menos 5 minutos para que pueda arrancar correctamente.\
Lo primero que haremos, como en la mayoría de casos, será utilizar nmap para realizar un escaneo de los puertos que se encuentran abiertos así como de los servicios que se encuentran disponibles en los mismos:

```
nmap -sV -p- IP.DE.LA.MÁQUINA -vvv
```

Sintaxis del comando:
- nmap: Utilizamos la herramienta de análisis nmap.
- -sV: Indicamos que queremos hacer un escaneo de tipo "Service Detection". Lo que hará será analizar los servicios que se encuentran funcionando en los puertos que encuentre abiertos.
- -p-: Indicamos que queremos analizar todos los puertos del equipo en cuestión.
- -vvv: Queremos que nmap nos de toda la información posible así que con este comando aumentamos la verbosidad del escaneo al máximo.

Una vez terminado el escaneo podemos observar que existen 2 puertos abiertos con los siguientes servicios:
- Puerto 22: Servicio ssh.
- Puerto 80: Servicio http.

Por lo tanto, tenemos un servidor web funcionando. Vamos a acceder al mismo con nuestro navegador en la dirección http://IP.DE.LA.MÁQUINA

Nos encontraremos con la siguiente web:
![PickleRick_1](https://user-images.githubusercontent.com/93337563/139298610-5c5bbe21-720e-4dc2-ad1d-93bb31146523.png)

No parece que esto nos de mucha información util la verdad. Vamos a ver si encontramos algo en el código fuente de la web. Podemos observar lo siguiente entre las líneas 28 y 34:\
![PickleRick_2](https://user-images.githubusercontent.com/93337563/139299301-d298f990-f009-4086-9e3b-e5b5953032ca.png)

De momento tenemos un nombre de usuario. ¿Tal vez podemos usarlo en el servicio SSH que hemos enumerado previamente? No obstante, antes de eso, podemos probar a visitar el archivo robots.txt de la web (¡¡siempre es buena idea darnos un paseo por el archivo robots.txt. Muchas veces encontramos cosas útiles!!). Podemos acceder al mismo desde http://IP.DE.LA.MÁQUINA/robots.txt

Parece que lo único que contiene es la famosa frase de Rick: Wubbalubbadubdub. ¿Podría ser la contraseña para el usuario que hemos encontrado antes?

Vamos a seguir enumerando; pero ahora la web. Para ello utilizaremos gobuster. El comando que emplearemos será el siguiente:

```
gobuster -d -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u IP.DE.LA.MÁQUINA
```

Sintaxis del comando:
- gobuster: Utilizamos la herramienta de análisis gobuster.
- -d: Indicamos que queremos hacer un análisis de los directorios.
- -w: Indicamos el path de la wordlist que queremos usar para comparar. En mi caso he utilizado "Directory Lists 2.3" en su formato medio. Si estáis trabajando desde       Kali Linux la tendréis instalada por defecto. En la AttackBox de THM también se encuentra disponible.
- -u: Dirección IP del servidor web que vamos a analizar. En este caso la dirección ip de nuestra máquina. ¡No os olvidéis del http antes de la IP!

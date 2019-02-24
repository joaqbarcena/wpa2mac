#Antes de usar
Estos scripts fueron hechos con fines de investigacion para MacOS, el uso de estos de forma libre esta bajo su
responsabilidad
La instalacion en si no requiere de mucho mas, mas que algunas tools preinstaladas
```bash
$ brew install wireshark
$ brew install aircrack-ng 
$ brew install crunch 
$ sudo ln -s /System/Library/PrivateFrameworks/Apple80211.framework/Versions/Current/Resources/airport /usr/local/sbin/airport
```

#Usage
Primero debe ejecutarse el handshake con permisos root
```bash
$ sudo ./handshake <channel> <bssid>
```
Esto habilita el modo monitor sobre el bssid que elegiste, y abre un filtro sobre los paquetes
del 4-way handshake, lo recomedable es que lacantidad de paquetes sea `> 100` a veces puede que por
distancia o infraestructura le cueste demasiado capturar paquetes por lo cual puede que no capture 
toda la negociacion aun siendo > 100

Para forzar handshakes, es necesario hacer un jamming o como en la suite de aircrack se conoce como
el ataque de de-auth (aireplay-ng --deauth ....) aireplay en mac no funciona correctamente aun debido al AirPort
por lo que encontre un programa bastante fiable y amigable 
`https://github.com/unixpickle/JamWiFi`
Una masa, hay que procurar abrir el programa y hacer el scan antes ejecutar el handshake, ya que una vez este en modo
monitor no podra hacer un scan. No voy a explicar su uso por que realmente es muy intuitivo y funcional

Una vez capturado los paquetes damos `ctrl + c` para matar el proceso, y tambien cerrar el JamWiFi
```bash
$ ./crack <Prefix> <Start> <End> <bssid>
```
`Prefix` : Es un nro o palabra que no se altera en la generacion del diccionario
`Start` : Es un nro que se toma como base
`End`   : Es un nro que se toma fin, se llega aqui desde la base +1 +1 +1 +1 ...
`bssid` : Del que se capturaron los paquetes

Este va a abrir la misma pantalla del clasico aircrack-ng. 

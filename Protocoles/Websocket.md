protocole : https://www.rfc-editor.org/rfc/rfc6455.txt

Le protocole Websocket permette d'établir une connexion ouverte entre les deux partie permettant ainsi au deux partie d'envoyer des données sans avoir besoin de faire des requête [[HTTP]] en permanence. Celui-ci se base sur le protocole [[TCP]].
Ce protocole est divisé en deux partie l'handshake et enfin l'envoie/réception de message.

Le client va faire une requête souhaitant établir une connexion par websocket au serveur (handshake ouvrante). Si celui-ci accepte la connexion ils pourront commencer à discuter. Les données pourront donc transiter entre les deux par unité appelé des "message".

Un message est composé d'un ensemble de "frame" (fragment). Chaque frame possède un type qui lui est associé et chaque frame appartenant au même message possède le même type.
Il existe des types pour les données textuel (interprété en UTF-8), donnée binaire (l'interprétation est laissé à l'application) et enfin des frames de contrôle qui n'ont pas pour but de transporté des donnée mais qui sont utilisé pour envoyer des signal comme par exemple que la connexion doit être coupé

## Handshake

L'handshake c'est ce qui va permettre d'établir connexion par websocket entre le client et le serveur. Il y a deux type d'handshake

1. Handshake ouvrante
2. Handshake fermante

### Handshake ouvrante

L'handshake ouvrante va permettre d'établir la connexion entre les deux partie. Celle-ci se fait via une requête HTTP Upgrade envoyer par le client de la forme suivante

### Requête cliente

```
GET /chat HTTP/1.1
Host: server.example.com
Upgrade: websocket
Connection: Upgrade
Origin: http://example.com
Sec-WebSocket-key: dGhlIHNhbXBsZSBub25jZQ==
Sec-WebSocket-Protocol: chat, superchat
Sec-WebSocket-Version: 13
```

Dans cette requête le client va pouvoir ajouter des champs relative au websocket

- `Sec-WebSocket-Protocol` : va permettre d'informer le serveur quelles sous protocole le client supporte. Le serveur devra choisir l'un de ses protocole
- `Sec-WebSocket-Version` : Va permettre d'indiquer au serveur quelle version du protocole le client souhaite utiliser
- `Sec-WebSocket-Key` : Cette clé va être utilisé par le serveur pour générer la réponse du serveur afin d'indiquer que la requête à bien été traité par le serveur et que celui-ci accepte bien les websocket. Elle est généré en gérant des bytes aléatoire en base64 et ne doit pas dépasser 16 bytes de longueur

### Requête serveur

Si le serveur accepte la connexion par websocket il va renvoyer une réponse de la forme suivante :

```
HTTP/1.1 101 Swicthing Protocols
Upgrade: websocket
Connection: Upgrade
Sec-WebSocket-Accept: s3pPLMBiTxaQ9kYGzzhZRbK+xOo=
Sec-WebSocket-Protocol: chat
```

La réponse du serveur est plus simple que la requête que le client doit envoyer elle contient deux champs relative au websocket :

- `Sec-WebSocket-Protocol`: Indique quel protocole sera utilisé. Le protocole est choisi en fonction de ce que le serveur supporte et de ce que le client supporte aussi
- `Sec-WebSocket-Accept`: Va permettre d'indiquer que si le serveur accepte bien la connexion. La valeur est créer à partir de la clé envoyé par le client en y concaténant la valeur `258EAFA5-E914-47DA-95CA-C5AB0DC85B11`. Une fois la concaténation faite le serveur prendre le hash SHA-1 de cette concaténation et va l'encoder en base64. Si cette valeur n'est pas la valeur que ce que le client attendait ou si le champ n'existe pas la connexion ne sera pas établie

La réponse du serveur doit avoir pour status code `101` tout autre status code sera et devra être considéré comme un échec

## Handshake fermante

L'handshake fermante  va être initié par l'une des deux entités en envoyant une frame de contrôle qui va contenir une séquence de contrôle spécifique pour indiquer le début de l'handshake fermante.
En recevant ce genre de frame l'autre entité va lui envoyer une frame fermante. Une fois que cette dernière à été reçu alors l'entité ayant initié la fermeture va fermer la connexion en étant sûr qu'aucune autre donnée n'arrivera à l'avenir.

Il est important de prendre en compte que l'entité qui reçoit la frame initiant la coupure de connexion ne doit plus envoyé de donnée et doit seulement renvoyé une frame fermante

## Sécurité

La sécurité du protocole se base sur 3 points :

Tout d'abord si on est dans le cas d'une page web le protocole va utiliser l'origine de la page pour restreindre les pages pouvant accéder au serveur

Le protocole ne pourra pas établir de connexion avec un serveur ayant été créer avant les protocole [[SMTP]] et [[HTTP]]

Enfin on ne pourra pas établir de connexion quand des données d'autre protocole (comme le protocole [[HTTP]]) sont envoyé au serveur websocket comme par exemple si on envoie un formulaire au serveur.

### Relation entre [[TCP]] et [[HTTP]]

Le protocole des web socket est un protocole basé sur le protocole [[TCP]] et sa seule relation avec le protocole [[HTTP]] vient de la requête envoyé pour établir la connexion ([[#Handshake ouvrante]])

Par défaut le protocole utilise le port 80 et il utilisera le port 443 pour des connexion sécurisé par [[TLS]]

## Les URI

Il existe deux formats d'URI pour les websocket

```
ws-URI = "ws://host[:port]/path/[?query]"
wss-URI = "wss://host[:port]/path/[?query]"
```

Les uri `ws` utilise le port 80 par défaut et les uri `wss` utilisent le port 443 et font référence au connexion sécurisé

## Frame

Les message sont les unités qui vont transporté les données. Ces dernier sont composé d'une ou plusieurs frame (fragment). Voici à quoi ressemble une frame et les partie qui la compose:

```
	  0                   1                   2                   3
      0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
     +-+-+-+-+-------+-+-------------+-------------------------------+
     |F|R|R|R| opcode|M| Payload len |    Extended payload length    |
     |I|S|S|S|  (4)  |A|     (7)     |             (16/64)           |
     |N|V|V|V|       |S|             |   (if payload len==126/127)   |
     | |1|2|3|       |K|             |                               |
     +-+-+-+-+-------+-+-------------+ - - - - - - - - - - - - - - - +
     |     Extended payload length continued, if payload len == 127  |
     + - - - - - - - - - - - - - - - +-------------------------------+
     |                               |Masking-key, if MASK set to 1  |
     +-------------------------------+-------------------------------+
     | Masking-key (continued)       |          Payload Data         |
     +-------------------------------- - - - - - - - - - - - - - - - +
     :                     Payload Data continued ...                :
     + - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - +
     |                     Payload Data continued ...                |
     +---------------------------------------------------------------+
```

FIN : 1 bit

Ce bit va indiquer si c'est le dernier fragment d'un message si il est égale à 1 alors on est sur le dernier fragment et cela veut dire qu'on à récupérer le message au complet.
Il se peut qu'un message soit composé d'une seule frame

Opcode : 4 bits

Il va servir pour définir comment le "Payload data" doit être interprété. Si un opcode invalide ou inconnu est envoyé alors l'entité qui recois le message doit fermer la connexion et envoyer une erreur

- `%x1` : indique c'est du texte
- `%x2` : Indique que c'est des données binaire
- `%x3-7` : Indique que c'est une frame de controle
- `%x8` : Indique que la connexion doit être coupé
- `%x9` : Indique un ping
- `%xA` : Indique un pong
- `%xB-F` : sont réservé pour d'autre frame de controle

Payload length : 7, 7+16, 7+64

Indique la longueur du payload

Payload data : (x+y) bytes

## Envoie et réception

### Envoi

Voici les étapes nécessaire pour envoyer un message

- Le client doit s'assurer que la connexion est ouverte. Si a un moment le statut de connexion change alors le client doit s'arrêter immédiatement 
- Le client doit encapsuler les données en une frame ou en plusieurs si la donnée est trop large
- Le client doit s'assurer que le `opcode` est la bonne valeur pour que celle ci soit interprété de la bonne façon
- Le bit de FIN sur la dernière frame doit être a 1

### Réception

Voici les étapes nécessaire à la réception :

- Les données entrantes doivent être parsé en tant que des websocket frames
- Les frame doivent être traité en fonction de leur `opcode`
- Si la frame reçu n'est qu'une partie d'un message est n'est pas la frame de fin alors les donnée doivent être concaténer jusqu'à l'arriver de la dernière frame

## Fermer la connexion

Pour fermer la connexion l'une des entités doit envoyer une frame de fermeture càd une frame de contrôle ayant pour `opcode = %x8`. De plus elle doit indiquer un code et la raison de la fermeture

Une fois la frame envoyé ou reçu la handshake fermante est initié et donc que la connexion est en train d'être fermé mais elle n'est pas encore fermé à ce stade.
En effet la connexion sera entièrement fermé une fois que l'entité qui à reçu cette frame renvoi aussi une frame de fermeture et que la connexion [[TCP]] soit fermé

Dans le cas ou les deux entités ne sont pas d'accord sur le code de fermeture alors elles vont démarrer indépendamment de l'autre la coupure de la connexion

## Ping / pong

Le client peut envoyer des frames de type ping (opcode 0x9). Dans ce cas ci le serveur doit répondre le plus vite possible avec une frame de type pong (opcode 0xA)

Dans le cas ou le client a envoyer plusieurs frame de type ping sans que le serveur est eu le temps de repondre le serveur doit alors répondre à la dernier frame reçu

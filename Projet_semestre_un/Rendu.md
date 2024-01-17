# TP Réseau avec VLAN et protocoles

## Matériel

Nous avons congifuré au total 20 VPCS ainsi que 6 switchs et 3 routeurs. 

Tout cela est dispatché dans 3 bâtiments :

- Le premier contient un routeur, un switch et 4 VPCS qui sont dans un vlan.
- Le deuxième contient un routeur, 4 switchs et 12 VPCS qui sont dans 5 vlan.
- Le troisième contient un routeur, un switch et 4 VPCS

## Configuration

Pour commencer, notre objectif était de faire trois réseaux différents (un par bâtiment) et que ceux ci puissent communiquer entre eux. 
Nous avons décider de les configurer comme ceci :

#### Bâtiment 1  <span style="font-size: 15px; font-weight: bold; color: white;">(ip en 10.0.0.0)</span> 

Il y a 4 VPCS connecté à un switch lui même connecté a un routeur. 
Il n'y a qu'un vlan : vlan 10
Les 4 VPCS ont comme ip :
- 10.0.10.13/24
- 10.0.10.14/24
- 10.0.10.15/24
- 10.0.10.16/24

Ils ont tous comme gateway 10.0.10.254 (l'ip du routeur)
Le routeur a comme ip : 10.0.10.254/24
Pour le switch, nous avons fait un access vers les 4 VPCS.


#### Bâtiment 3  <span style="font-size: 15px; font-weight: bold; color: white;">(ip en 20.0.0.0)</span> 

Il y a un routeur avec 5 ip :
- 20.0.10.254
- 20.0.20.254
- 20.0.30.254
- 20.0.40.254
- 20.0.50.254

Ce routeur est connecté a un switch que l'on va appelé IOU1 pour plus de facilité.
IOU1 


#### Bâtiment 1  <span style="font-size: 15px; font-weight: bold; color: white;">(ip en 10.0.0.0)</span> 

Il y a 4 VPCS connecté à un switch lui même connecté a un routeur. 
Il n'y a qu'un vlan : vlan 10
Les 4 VPCS ont comme ip :
- 30.0.10.13/24
- 30.0.10.14/24
- 30.0.10.15/24
- 30.0.10.16/24

Ils ont tous comme gateway 30.0.10.254 (l'ip du routeur)
Le routeur a comme ip : 30.0.10.254/24
Pour le switch, nous avons fait un access vers les 4 VPCS.

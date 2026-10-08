 # FortiGate-60F-Network-Security-Lab


Déploiement, sécurisation et optimisation d'une infrastructure réseau avec FortiGate 60F

1. Contexte et objectif

Ce projet consiste en la configuration et la sécurisation d'une infrastructure réseau basée sur un FortiGate 60F physique, utilisé comme équipement central de sécurité, de routage, de filtrage et de contrôle des communications.

L'objectif du laboratoire était de mettre en pratique plusieurs fonctionnalités essentielles d'un pare-feu nouvelle génération :

segmentation réseau ; configuration LAN / DMZ / WAN ; routage IPv4 ; objets réseau et services ; politiques Firewall ; NAT et DNAT ; publication de services ; sécurisation d'un serveur 3CX ; DNS et Split DNS ; VPN ;
SD-WAN ; supervision des liens WAN ; filtrage Web ;prévention d'intrusion IPS ; journalisation et analyse du trafic ; QoS et Traffic Shaping.
Une attention particulière a été portée à l'intégration d'un environnement 3CX/VoIP, avec séparation du serveur dans une DMZ, publication contrôlée des services nécessaires et priorisation du trafic SIP/RTP.

L'objectif n'était pas uniquement de configurer le FortiGate, mais également de comprendre la relation entre :
Architecture - Routage - Firewall - NAT - Services - Sécurité - Supervision - Optimisation

2. Architecture du laboratoire

L'architecture repose sur un FortiGate 60F placé au centre de l'infrastructure. Le FortiGate assure notamment la connexion vers Internet, le routage entre les différentes zones, la segmentation LAN/DMZ, le filtrage, la traduction NAT, la publication contrôlée du serveur 3CX, la gestion de plusieurs liens WAN, le VPN, les fonctions de sécurité ainsi que la supervision et l'analyse des flux.

Architecture logique
Architecture multi-WAN / SD-WAN

3. Technologies et outils utilisés
4. Préparation et administration du FortiGate

   4.1. Vue générale des interfaces
   

Cette capture présente l'organisation générale des interfaces du FortiGate 60F. Elle permet de documenter les interfaces internes, la DMZ, WAN1, WAN2 et l'organisation de la connectivité du laboratoire.
Compétences démontrées : Administration d'un FortiGate physique ; identification des interfaces ; organisation de l'infrastructure réseau.
<img width="1359" height="708" alt="001-vue-generale-interfaces" src="https://github.com/user-attachments/assets/b4350775-a117-40ea-837c-fb8d1f3ed6db" />

   4.2 Inventaire et administration

Cette capture documente l'environnement d'administration du FortiGate 60F et l'organisation des interfaces utilisées par le laboratoire.
Compétences démontrées : Administration via FortiOS ; identification des composants réseau.
<img width="1470" height="956" alt="001-FGT-B-Inventaire et administration" src="https://github.com/user-attachments/assets/575ceb75-056f-4334-b6ab-864a28577f85" />

5. Configuration des interfaces réseau

   5.1 LAN, DMZ et WAN

Le FortiGate sépare l'infrastructure en plusieurs zones réseau. Le LAN représente le réseau interne, la DMZ les services exposés ou contrôlés, et WAN1/WAN2 la connectivité externe.
Compétences démontrées : Segmentation LAN/DMZ/WAN ; conception réseau ; contrôle inter-zones.
<img width="1405" height="724" alt="002-FGT- Interfaces LAN _ DMZ_WAN" src="https://github.com/user-attachments/assets/5116e885-9cb7-41aa-bd6a-8979a9adbb80" />

6. Routage IPv4

   6.1 Configuration du routage

La table de routage du FortiGate contient notamment une route par défaut 0.0.0.0/0 permettant au trafic destiné aux réseaux externes d'être transmis vers la passerelle WAN.

Compétences démontrées : Routage IPv4 ; route par défaut ; analyse réseau.
<img width="1290" height="649" alt="003-FGT-Routage" src="https://github.com/user-attachments/assets/10449d59-91ce-403b-bea9-57afc3901405" />

   6.2 Validation du routage avec la CLI

La table de routage a également été vérifiée directement depuis la CLI FortiOS afin d'identifier les routes connectées, la route par défaut et les interfaces associées.
Compétences démontrées : CLI FortiOS ; diagnostic réseau ; lecture d'une table de routage.
<img width="1470" height="956" alt="004-FGT-Routage-B" src="https://github.com/user-attachments/assets/edba9cae-60aa-4a7e-9f29-da9c872a0b52" />

7. Objets réseau et services

   7.1 Objets d'adresses

Des objets d'adresses ont été créés afin de représenter les réseaux et serveurs utilisés dans les politiques de sécurité, notamment le LAN, la DMZ et le serveur 3CX.
Compétences démontrées : Gestion d'objets réseau ; lisibilité et maintenabilité des politiques.

<img width="1367" height="805" alt="005-FGT-Addresse" src="https://github.com/user-attachments/assets/1bc91c59-57b4-4ae4-b628-21ec79cab609" />

   7.2 Objets de services

Des objets de services représentent les protocoles et ports nécessaires aux applications, notamment HTTPS, SIP et RTP.
Compétences démontrées : Gestion des services ; contrôle précis des ports et protocoles.
<img width="1352" height="830" alt="006-FGT-Services" src="https://github.com/user-attachments/assets/130628a3-8cf9-4147-902c-fe3b81b4a4aa" />

8. Publication du serveur 3CX

   8.1 VIP / DNAT HTTPS

Une règle VIP permet de publier le service HTTPS du serveur 3CX situé dans la DMZ. Le FortiGate agit comme point de contrôle entre Internet et le serveur.
Compétences démontrées : VIP ; DNAT ; publication de services ; sécurisation d'une DMZ.
<img width="1362" height="693" alt="007-FGT- DNAT-VIP-ublication HTTPS 3CX" src="https://github.com/user-attachments/assets/09887b4f-635b-491d-9a99-2737fcfd4f82" />

9. Politiques Firewall

    9.1 Organisation des politiques

Les politiques Firewall définissent explicitement les communications autorisées entre les différentes zones. Une logique de blocage des communications DMZ vers LAN est notamment utilisée.
Compétences démontrées : Firewall Policy ; segmentation ; moindre privilège ; contrôle inter-zones.
<img width="1378" height="810" alt="007-FGT-Politique-Objet" src="https://github.com/user-attachments/assets/8528b1cd-b50a-426c-ab60-a0923e3a6238" />

10. Accès Internet du serveur 3CX

    10.1 DMZ vers Internet avec NAT

Une politique dédiée permet au serveur 3CX de communiquer vers Internet avec NAT activé sur la sortie WAN. La source est limitée au serveur 3CX.
Compétences démontrées : NAT ; filtrage sortant ; contrôle du trafic DMZ.
<img width="1278" height="827" alt="008-FGT-DMZ-3CX-to-Internet-NAT" src="https://github.com/user-attachments/assets/a3ff45fb-cea4-4da6-b978-aecd8470f830" />

11. DNS et Split DNS

    11.1 Configuration DNS

Le FortiGate utilise des serveurs DNS configurés pour assurer la résolution des noms nécessaires à l'infrastructure.
Compétences démontrées : DNS ; services réseau.
<img width="1346" height="666" alt="009-FGT-DNS" src="https://github.com/user-attachments/assets/17a544ad-e3b8-4407-8898-c09fccfc76df" />

   11.2 Split DNS

Une zone DNS interne permet d'adapter la résolution d'un domaine associé à l'environnement 3CX selon le contexte réseau.
Compétences démontrées : Split DNS ; résolution interne ; architecture de services.
<img width="1112" height="647" alt="010-FGT-Split DNS" src="https://github.com/user-attachments/assets/e2797581-7761-4e78-bdd7-6356898be83b" />

12. VPN

    12.1 Configuration du VPN

La configuration VPN comprend une Phase 1, une Phase 2, une segmentation du tunnel, un réseau distant et une politique associée au VPN.
Compétences démontrées : VPN ; IPsec ; sécurisation des accès distants.
<img width="1103" height="617" alt="013-FGT-VPN" src="https://github.com/user-attachments/assets/395dcbb1-6fdd-4d51-93fb-05ac2375630b" />

   12.2 Validation avec FortiClient

La configuration est validée avec FortiClient et montre un état de connexion VPN établi avec le profil VPN du laboratoire.
Compétences démontrées : FortiClient ; validation d'un tunnel ; accès distant sécurisé.
<img width="870" height="579" alt="014-FGT_Client" src="https://github.com/user-attachments/assets/f5bb3109-7674-4c02-941e-c7739b3ce4d6" />

13. SD-WAN et multi-WAN

    13.1 Intégration de WAN1 et WAN2
Deux interfaces WAN ont été intégrées au SD-WAN afin de gérer plusieurs chemins de connectivité Internet.
Compétences démontrées : SD-WAN ; multi-WAN ; résilience réseau.
<img width="1666" height="354" alt="015-FGT-SDWAN" src="https://github.com/user-attachments/assets/8b41f878-f0d2-4639-a008-adc33be62dc1" />

14. Règle SD-WAN

    14.1 Règle SD-WAN

Une règle SD-WAN nommée SDWAN-Internet utilise WAN1 et WAN2 comme membres et prend notamment en compte la latence.
Compétences démontrées : Règles SD-WAN ; sélection de chemin ; qualité réseau.
<img width="1662" height="291" alt="016-FTG-RGL_SDWAN" src="https://github.com/user-attachments/assets/403cd391-ede9-4094-8e5f-2840c330382c" />

15. Sondes SLA

    15.1 Sondes SLA SD-WAN
Les sondes SLA permettent de mesurer la qualité des liens WAN, notamment la latence, la perte de paquets et la gigue.
Compétences démontrées : SLA ; monitoring ; latence ; perte de paquets ; gigue.
<img width="1570" height="717" alt="0018-FGT-SONDE-SDWAN" src="https://github.com/user-attachments/assets/a4896b84-620c-495b-9689-6ef25b383559" />

16. Monitoring SD-WAN

    16.1 Monitoring SD-WAN

Le monitoring présente l'état des interfaces WAN et les métriques associées. Cette capture complète la configuration SD-WAN, les règles et les sondes SLA.
Compétences démontrées : Supervision WAN ; analyse des performances ; SD-WAN.
<img width="1762" height="533" alt="019-FGT_monitoring-sdwan" src="https://github.com/user-attachments/assets/5724aa58-799b-427f-80a3-010447b9a7cf" />

17. Filtrage Web

    17.1 Filtrage Web

Un profil de filtrage Web nommé LAB17-WEB-FILTER a été configuré avec des catégories de risques en blocage. La capture indique également une limitation liée à la licence FortiGuard Web Filtering pour certaines fonctions.
Compétences démontrées : Web Filtering ; contrôle d'accès ; compréhension des dépendances de licence.
<img width="1406" height="903" alt="020-FGT-FILTRAGE-WEB" src="https://github.com/user-attachments/assets/6dc007ef-4ee3-4d9a-91c3-6e1d3c837a5a" />

18. Prévention d'intrusion — IPS

    18.1 IPS

Le module IPS présente des signatures classifiées par sévérité, cible, système d'exploitation, action et CVE. Les exemples visibles comprennent SQL Injection, Buffer Overflow, Remote Code Execution et Botnet.
Compétences démontrées : IPS ; signatures de sécurité ; CVE ; prévention d'intrusion.
<img width="1790" height="934" alt="022-FGT-IPS" src="https://github.com/user-attachments/assets/0f417c2a-84e9-4ad3-91a1-c92baa3d0955" />

19. Journalisation et analyse du trafic

    19.1 Journaux FortiGate

Les journaux permettent d'observer les communications traitées par le pare-feu, notamment la date/heure, la source, la destination, l'application, le résultat et la règle utilisée. Des flux associés à 3CX sont visibles.
Compétences démontrées : Logs Firewall ; analyse des flux ; troubleshooting ; validation des politiques.
<img width="1790" height="934" alt="022-FGT-IPS" src="https://github.com/user-attachments/assets/9e8b38bf-b971-4fef-8d79-f98c4c94daa1" />

20. QoS et Traffic Shaping pour la VoIP

    20.1 QoS et Traffic Shaping

Une politique QOS-VOIP-3CX applique le Traffic Shaper high-priority au trafic SIP et RTP 9000-10999 afin de prioriser les communications VoIP.
Compétences démontrées : QoS ; Traffic Shaping ; SIP ; RTP ; optimisation de la VoIP.
<img width="1798" height="586" alt="023-FGT-QOS" src="https://github.com/user-attachments/assets/cfc64042-5c34-49cd-af2d-e9ddb8aed7ae" />

21. Compétences démontrées

Administration réseau

Administration d'un FortiGate 60F physique

Configuration des interfaces réseau

Segmentation LAN / DMZ / WAN

Routage IPv4

Analyse d'une table de routage

Utilisation de la CLI FortiOS

Sécurité réseau

Configuration de politiques Firewall

Segmentation inter-zones

Principe du moindre privilège

Sécurisation d'une DMZ

NAT

DNAT

VIP

Publication contrôlée de services

IPS

Web Filtering

Infrastructure et services

DNS

Split DNS

Gestion d'objets réseau

Gestion d'objets de services

Intégration d'un serveur 3CX

Publication HTTPS

Gestion des flux SIP/RTP

VPN

Configuration VPN

IPsec

FortiClient

Validation de connectivité

Sécurisation des accès distants

SD-WAN et optimisation

Multi-WAN

SD-WAN

Règles SD-WAN

SLA

Latence

Perte de paquets

Gigue

Monitoring WAN

QoS

Traffic Shaping

Priorisation du trafic VoIP

Supervision et diagnostic

Analyse des journaux Firewall

Validation des flux

Diagnostic du routage

Vérification du trafic applicatif

Analyse de la qualité des liens WAN

22. Défis techniques et approche de diagnostic

L'objectif du laboratoire était de ne pas considérer le pare-feu comme une simple interface de configuration. Lorsqu'un service réseau ne fonctionne pas, plusieurs composants peuvent être impliqués.

Méthode de diagnostic appliquée

Vérifier l'état de l'interface

Vérifier l'adressage IP

Vérifier la table de routage

Vérifier les objets réseau

Vérifier la politique Firewall

Vérifier le NAT / DNAT

Vérifier les ports et services

Vérifier les journaux

Valider depuis le client

Confirmer le résultat

23. Ce que j'ai appris

Ce laboratoire m'a permis de développer une compréhension plus complète du rôle d'un pare-feu nouvelle génération dans une infrastructure réseau.

Segmentation réseau ; Administration Firewall; NAT et publication de services; Sécurisation d'une DMZ; VPN; DNS; SD-WAN; Supervision; IPS; Analyse des journaux; QoS.

J'ai également compris l'importance de considérer la sécurité comme un ensemble de mécanismes complémentaires; 
Segmentation + Firewall + NAT + IPS + Logs + SD-WAN + QoS

24. Approche de sécurité

Segmentation

Le LAN, la DMZ et le WAN sont séparés afin de limiter les communications inutiles.

Moindre privilège

Les politiques Firewall définissent explicitement les communications nécessaires.

Réduction de la surface d'exposition

Les services publiés depuis Internet sont limités aux besoins identifiés, notamment pour 3CX.

Contrôle des flux

Les communications sont contrôlées par les politiques Firewall, les objets réseau et les objets de services.

Supervision

Les journaux permettent de vérifier le comportement réel du trafic.

Résilience

Le SD-WAN permet de gérer plusieurs liens WAN et d'évaluer leur qualité.

Optimisation

Le Traffic Shaping permet de prioriser les flux VoIP sensibles aux performances réseau.

25. Conclusion

Ce projet m'a permis de mettre en pratique l'administration d'un FortiGate 60F dans un environnement de laboratoire reproduisant plusieurs scénarios d'entreprise.

Le laboratoire couvre le cycle complet :

Architecture → Segmentation → Routage → Firewall → NAT → Services → VPN → SD-WAN → Sécurité → Supervision → Optimisation

La configuration d'un environnement 3CX en DMZ a également permis de travailler sur des problématiques concrètes de publication de services, de filtrage des flux SIP/RTP, de DNS et de qualité de service.

Au-delà de la configuration des fonctionnalités, ce projet m'a permis de développer une démarche de diagnostic basée sur l'observation du réseau, la vérification du routage, l'analyse des politiques et l'exploitation des journaux.

26. Technologies et compétences clés

FortiGate 60F; FortiOS; Firewall; LAN / DMZ / WAN; IPv4 Routing; NAT / DNAT; VIP; DNS / Split DNS; VPN / IPsec; FortiClient; SD-WAN; SLA; IPS; Web Filtering; Firewall Logs; QoS; Traffic Shaping; 3CX / VoIP; SIP / RTP
Network Troubleshooting.








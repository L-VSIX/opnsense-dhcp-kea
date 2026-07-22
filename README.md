# 📡 Configuration des réservations DHCP avec Kea — OPNsense

> Attribution d'adresses IP par sous-réseau VLAN via le moteur DHCP Kea intégré à OPNsense, avec passage progressif vers des réservations statiques sur le parc.

## Rôle de Kea dans l'architecture

OPNsense assure à la fois le rôle de passerelle, de point de filtrage inter-VLAN et de **serveur DHCP via KEA** — le moteur DHCP moderne d'OPNsense (successeur d'ISC DHCP). Chaque VLAN déclaré côté pare-feu reçoit un sous-réseau KEA DHCP dédié, avec sa propre plage d'allocation.

## Procédure

1. Une fois l'interface logique du VLAN créée côté OPNsense avec son adresse de passerelle, déclarer le **sous-réseau Kea** correspondant (Services › Kea DHCP).
2. Définir la plage d'allocation dynamique du sous-réseau.
3. Pour les hôtes critiques (contrôleurs de domaine, filers, hyperviseurs), transformer l'allocation en **réservation statique** basée sur l'adresse MAC, afin de garantir une IP stable dans le temps.

## Pourquoi des IP statiques sur le parc

Une phase du projet a consisté à **fixer les adresses IP** de l'ensemble du parc plutôt que de dépendre uniquement du bail DHCP dynamique — notamment pour la fiabilité des règles de filtrage inter-VLAN et de la résolution DNS interne, qui référencent des IP précises.

## Repos liés

- `opnsense-segmentation-vlan` — cartographie des VLAN portés par Kea
- `documentation-cartographie-reseau`

## Auteur

**Lilian Vertueux** — [LinkedIn](https://www.linkedin.com/in/lilian-vertueux/)

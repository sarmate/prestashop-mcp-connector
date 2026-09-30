# Connecteur MCP pour PrestaShop

Relie Claude, ChatGPT ou tout assistant compatible MCP à une boutique **PrestaShop**. Le commerçant pose ses questions en français (factures, impayés, clients, ventes par région, stocks) et fait préparer ses devis, sans ouvrir le back-office.

Le connecteur est un **module PrestaShop** : le serveur MCP tourne dans la boutique, sur l'hébergement du commerçant. Aucun service tiers, aucun abonnement.

**Essayez-le avec votre propre Claude**, sur une boutique de démonstration aux données fictives : <https://www.studio.sarmate.net/mcp/essai/>
Vidéo de démonstration : <https://youtu.be/KrIiPDKdDL8>

## Outils

En lecture seule par défaut.

| Outil | Rôle |
|---|---|
| `search_orders` | Commandes par référence, client, statut, période, montant, produit ou lieu (ville, code postal, département, région, pays) |
| `get_order` | Détail d'une commande : lignes, adresses de facturation et de livraison, historique, paiements, facture |
| `search_invoices` | Factures par numéro, période, client, société, montant, produit ou lieu de facturation, avec les totaux de TVA |
| `get_invoice` | Détail d'une facture et ventilation de la TVA |
| `list_unpaid_orders` | Commandes en attente de paiement, avec leur ancienneté et les coordonnées du client, pour préparer les relances |
| `search_customers` | Clients par nom, société, lieu, nombre de commandes, montant dépensé, inactivité, impayés |
| `get_customer` | Fiche client : adresses, statistiques d'achat, dernières commandes et impayés |
| `sales_summary` | Chiffre d'affaires et commandes par mois, produit, ville, département, région, pays ou moyen de paiement |
| `search_products` | Produits avec prix, stock par déclinaison, ventes sur 30 et 90 jours, couverture de stock estimée |
| `report_unsupported_request` | Enregistre une demande que le connecteur ne sait pas traiter, pour l'améliorer |

En option, seulement pour les jetons autorisés à créer des devis :

| Outil | Rôle |
|---|---|
| `create_quote` | Devis numéroté avec PDF : produits du catalogue (nom, référence ou déclinaison) et lignes libres (prestations), remises par ligne ou globale, frais de port. Enregistré dans le module seulement : ni panier, ni commande, ni changement de stock |
| `get_quote`, `search_quotes`, `cancel_quote` | Lire, lister et annuler les devis (un devis annulé garde son numéro) |

## Sécurité

- Un jeton par assistant ou par équipe, avec ses droits (devis ou non), ses limites d'appels par minute et par jour, et sa révocation en un clic.
- Chaque appel est journalisé : outil, paramètres, résultat, durée.
- Option de masquage des données personnelles : prénom et initiale, e-mail et téléphone tronqués, jamais la rue.
- Création de devis désactivée tant que le commerçant ne l'autorise pas.
- Jetons stockés sous forme d'empreinte.

## Connexion

Point d'accès « Streamable HTTP » : `https://<votre-boutique>/module/studiomcp/endpoint`

- Claude Code : `claude mcp add --transport http boutique https://<votre-boutique>/module/studiomcp/endpoint --header "Authorization: Bearer <jeton>"`
- claude.ai (Paramètres → Connecteurs → Ajouter un connecteur personnalisé) : le jeton peut passer dans l'adresse (`?key=<jeton>`) si le commerçant active cette option, car claude.ai n'envoie pas d'en-tête.

## Compatibilité

Testé sur PrestaShop 8.2, avec claude.ai et Claude Code.

## À propos

Développé par [Studio Sarmate](https://www.studio.sarmate.net/), qui conçoit aussi des modules PrestaShop sur mesure et des serveurs MCP pour d'autres logiciels métier. Installation sur votre boutique, ou connecteur pour un autre outil : <https://www.studio.sarmate.net/mcp/>

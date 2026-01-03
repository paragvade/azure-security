# Vnet Peering
- Private connectivity between two or more virtual networks- traffic never traverses the public internet.
- Different than VPN
    - Vnet peering is only between Azure Vnets. VPN is for connecting Azure with on-prem or other clouds.
    - Vnet peering connection is not encrypted but uses Azure backbone network. VPN is encrypted using IPsec/IKE but traffic flows over internet.
    - Vnet peered connections have lower latency, higher bandwidth - no extra hops to traverse over internet, no encryption.
    - Vnet peering takes just minutes to configure. VPN gateway takes over 30 mins.
    - Vnet peering is not transitive by default. VPN Gateway is transitive with BGP enabled.
    - Vnet peering use case --> cross-region data replication, database failover within azure. VPN use case --> hybrid connectivity, cross-cloud connections.

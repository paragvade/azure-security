# ExpressRoute
- Connect on-prem network to Azure using completely private connection with help of **ISP**. Using ExpressRoute, on prem network can talk with not only Azure services but also with Microsoft 365.
- ExpressRoute is faster, more reliable and secure than VPN
- Dynamic routing between on-prem and Microsoft via BGP
- Built-in redundancy --> Each *ExpressRoute circuit* (connection between Partner edge location and Microsoft edge location) has two connections
- **ExpressRoute locations** - different from Azure regions. Once you connect to an ExpressRoute location, all Microsoft resources (Azure, M365) within that 'geopolitical region' becomes available to connect. A geopolitical region includes many Azure regions. E.g. North America is a geopolitical region. It includes Azure regions like East US, West US, Central US, Canada East, etc. It also includes ExpressRoute locations like New York, Silicon Valley, Vancouver etc. Connecting to ExpressRoute at New York location will make whole North America geopolitical region available. 
- **ExpressRoute Premium**- Global Connectivity i.e. can access Microsoft services in any region around world through ExpressRoute by enabling ExpressRoute Premium
- **ExpressRoute Global Reach** - to connect on-prem data centers in different parts of the world using Microsoft network
- **ExpressRoute Direct**- instead of using ISP to connect to Microsoft edge location, direct physical connectivity from data center to Microsoft Edge location. Exclusive ports on Microsoft's hardware than sharing ISPs infra. Regulated industries need physical separation and layer 2 encryption (MACSec)- which is available only in Direct. In terms of bandwidth, Direct has only 2 options-10 Gbps or 100 Gbps (hence costly). Standard ExpressRoute can start with 50 Mbps.

 
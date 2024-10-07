1. Check [PSN Portal](https://psn.qld.gov.au/app/dashboard/view)to see if devices down

2. Check **Site Change Calendar** to see if site has outage during outage
	1. <span style="color:rgb(146, 208, 80)">Yes</span> - Place ticket "On Hold", Link Change, state change affecting site. 
	2. <span style="color:rgb(255, 0, 0)">No</span> - Continue 3.

3. Check [Ergon](https://www.ergon.com.au/network/outages/outage-finder/outage-finder-map) | [Energex](https://www.energex.com.au/home/power-outages/emergency-outages-streets/)for power outages in the general area
	1. <span style="color:rgb(146, 208, 80)">Yes</span> - Place ticket "On Hold", Snip/paste outage to ticket, state change affecting site. 
	2. <span style="color:rgb(255, 0, 0)">No</span> - Continue 4.

4. SSH to Router - Check uptime / Carriage
```
sh ver | include uptime|System returned|System restarted|Last reload
sh ip bgp summ | begin Neighbor
```
1. Power - 
2. Carriage - 
3. Other - Continue to 





4. Check access to site router via C-Fabric (This would point to Cisco 30 week bug)
    
5. Call site to verify the following:
    
    1. Power to site 
        
    2. Power to equipment in PSN rack (including the RCD)
        
    3. Ask customer to reboot Service Provider NTU
        
    4. Once NTU rebooted, gather information on light sequence on NTU
        
    5. If site is still offline once NTU is up, then ask customer to reboot the site router.
        
6. Contact Service Provider and log a fault call (Either by phone or Portal)
    
    1. Provide Service Number for site service
        
    2. NTU Light sequence information
        
    3. Include the PSNMC Incident number in the Service Provider ticket
        
    4. Any other pertinent information as requested by Service Provider
        
    5. Gather reference number for incident
        
7. Update Incident 
    
    1. Update notes with pertinent information
        
    2. Generate 'External Task' and record fault reference number provided by Service Provider 
        
    3. Put reference number in the Summary or Description section so you can quickly identify your faults when contacted by the Service Provider.
        
    4. Access and update Incidents at least weekly. 
        
    5. When fault is resolved place relevant details in the Journal & Resolutions section.



#### **Power Check

Outage Finder - https://www.ergon.com.au/network/outages/outage-finder/outage-finder-map


#### **Carriage Check

| Carriage | URL                                                                                                                                                                                                                                                                                                   |
| -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| NBN      | https://energyqld.service-now.com/csm?id=eql_csm_index                                                                                                                                                                                                                                                |
| Telstra  | https://myid.telstra.com/identity/as/authorization.oauth2?client_id=b2b-telstraconnect&redirect_uri=https%3A%2F%2Fconnectapp.telstra.com&response_type=id_token%20token&scope=openid%20b2b%20username%20profile%20email&state=1912ccd84ffb4d1b94e18f586dc0f1d5&nonce=7a02ba33684c44e2990cf88ba39ce627 |
| Starlink | https://www.starlink.com/account/dashboard                                                                                                                                                                                                                                                            |



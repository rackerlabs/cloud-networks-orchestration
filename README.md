# Rackspace Cloud Networks Orchestration (HEAT) Templates
A collection of scripts that make it easy to set up routing
and gateway instances via Rackspace Cloud Networks (neutron).

## Current Scripts

cloud-nw-route

| Script Name        | Purpose  
| ------------- |-------------|
| cloud-nw-route.yml      | Makes a Cloud Network suitable for routing traffic (adds DNS servers and default gateway to subnet)|
| cloud-nw-route-generic-gw.yml     | same as cloud-nw-route, but with a generic gateway instance|  
| cloud-nw-route-c7-gw.yml | same as cloud-nw-route, but with a CentOS 7 gateway instance   

## How to Use

To use the Cloud Orchestration templates, copy the desired template to your clipboard,
then navigate to the [mycloud.rackspace.com portal](https://mycloud.rackspace.com). Click
**Orchestration**,
then click **"Stack Templates"**. From that page, click **"Create Custom Template."**
Paste the template into the text box, then click **"Create Template and Launch
Stack"**.

Fill in the stack details with your preferred information, such as Cloud
Server Image, preferred IP scheme, etc.

## How to Build Servers Behind the Gateway Instance

Build the same way as a normal Cloud Server (via the [mycloud.rackspace.com portal](https://mycloud.rackspace.com)), but deselect PublicNet and select
the Cloud Network you created with the template. ServiceNet is optional, but
recommended. (ServiceNet provides access to Cloud Load Balancers, Cloud Files, and Cloud Backups internal endpoints).

## Caveats

At the moment, these templates are only compatible with local storage flavors (General Purpose or I/O). Flavors that require a bootable volume (such as
Memory or Compute v1) will not work.

Gateway instances always have 2 default gateways injected by the Neutron API.
This is required for servers behind the gateway to function properly. If you use the generic template, your gateway instance might require manual configuration before it can route traffic properly. You can either login via the Emergency Console and make the changes manually, or make the changes via cloud-init user-data (see cloud-nw-route-c7-gw.yml for an example).

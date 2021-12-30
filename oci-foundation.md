# Oracle Cloud Infrastructure Foundations

## OCI Introduction

### Region

Uma região é composta por domínios de disponibilidade (avaliability domains). 

### Choosing a Region

- Location: Choose a region closest to your uses for lowest latency and highest performance!
- Data residency & compliance: Many countries have strict data residency requirementes.
- Service Availabinity: New cloud services are made avaliable based on regional demand, regulatory complicance, resource avaliability, and other factors.

### Availability Domains

Isolated from each other, fault tolerant, unlikely to fail simultaneosly. ADs not shared your physical infrastructure. A falha em um AD não impacta em outro. 

Cada domínio de disponibilidade possuí 3 domínios de falha.

### Fault Domains

Each Avaliability Domain has three Fault Domains (FD). Logical **data center** within an AD. Resources placed in diferent FDs will not share single points of hardware failure.

In any region, resources in at mot ONE fault domain are being actively changed at any ponit in time. This means that avaliability problems caused by chance procedures are isolated at the fault domain level.

You can control the placement of your compute or dtabase instaces to fault domains at instane "lauch time".

Orientação geral: Replicar a sua aplicação nos domínios de falha dentro de um domínio de disponibilidade. Para melhorar, você pode replicar por mais de um domínio de disponibilidade.

A sincronização entre as cópias pode ser realizada  por tecnologias como o Oracle Data Guard.

Design your architecture to deploy instances that perform the same tasks:
- In different Fault Domains (in one AD regions);
- In different Availability Domains for multiple AD regions.




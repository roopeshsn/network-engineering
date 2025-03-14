# VLAN Workbook

The topology is uniform in every scenarios consisting of 2 switches and 2 host devices. You task is to find if ping work from Host-01 to Host-02. If not then you need to find more than one possible solutions to make it work.

## Scenario-1:
<!-- <img src="./assets/scenario-1.png" width="800" height="600" /> -->
![Scenario-1](./assets/scenario-1.png)

Will the ping work between Host-01 to Host-02? 

## Scenario-2:

![Scenario-2](./assets/scenario-2.png)

Will the ping work between Host-01 to Host-02? If not then how it can be resolved?

## Scenario-3:

![Scenario-3](./assets/scenario-3.png)

One change when compared to scenario-2 is that the port configuration is changed between switches? Will the ping work now?

## Scenario-4:

![Scenario-4](./assets/scenario-4.png)

In this scenario the ports to hosts devices are configured as Trunk, also the allowed VLAN is configured as VLAN 10.

## Scenario-5:

![Scenario-5](./assets/scenario-5.png)

Every port of switches are configured as Trunk Native VLAN 10.

## Scenario-6:

![Scenario-6](./assets/scenario-6.png)

Switch-01's Port to Host-01 is configured as Trunk Native VLAN 100 and Switch-02'1 port to Host-02 is configured as Access VLAN 10.

## Scenario-7:

![Scenario-7](./assets/scenario-7.png)

Every port of switches are configured as Trunk Allowed VLAN 10 and Native VLAN are also 10.
# Subnetting Guide

How to find network and broadcast addresses for the given IP address?

- To find the network address, flip all the host bits to 0.
- To find the broadcase address, flip all the host bits to 1

## Subnetting Cheatsheet

| Group Size | 128 | 64  | 32  | 16  | 8   | 4   | 2   | 1   |
|------------|-----|-----|-----|-----|-----|-----|-----|-----|
| Subnet     | 128 | 192 | 224 | 240 | 248 | 252 | 254 | 255 |
| CIDR       | /25 | /26 | /27 | /28 | /29 | /30 | /31 | /32 |
| CIDR       | /17 | /18 | /19 | /20 | /21 | /22 | /23 | /24 |
| CIDR       | /9  | /10 | /11 | /12 | /13 | /14 | /15 | /16 |
| CIDR       | /1  | /2  | /3  | /4  | /5  | /6  | /7  | /8  |

2^(32 - CIDR) is total no. of IP addresses

## Wildcard Mask

Subtract each octet from 255.

| CIDR          | /26 (255.255.255.192)              | 
|---------------|------------------------------------|
| Subnet Mask   | 11111111.11111111.11111111.11000000|
| Wildcard Mask | 00000000.00000000.00000000.00111111|


- Wildcard mask bit 0 match the corresponding bit value in the address
- Wildcard mask bit 1 ignore the corresponding bit value in the address

### Discontiguous Wildcard Mask

Till now we've seen that,
- Subnet masks are a series for 1's followed by 0's.
- Wilcard masks are a series for 0's followed by 1's, where 0 will be matched and 1 will be not matched (ignored).

Also 0.0.8.255 (0.0.00001000.11111111) is valid Wildcard mask, which is known as Discontiguous Wildcard Mask.

For example say I have two networks, 192.168.8.0/24 and 192.168.16.0/24. I want to match only these two networks. OUR ACL has the following rules,

```
permit 192.168.8.0 0.0.0.255
permit 192.168.16.0 0.0.0.255
```

Now I would like to accomplish the same using only one rule. This is where Discontiguous Wildcard Mask help.

Let's convert both network addresses to binary,

192.168.8.0 ->  11000000.10001000.00001000.00000000

192.168.16.0 -> 11000000.10001000.00010000.00000000

As you see the fourth and fifth bits in the third octet is not identical. Let's not match those bits. So our wildcard mask is 0.0.24.255. And now our ACL has this rule,

```
permit 192.168.8.0 0.0.24.255
```

Now say a packet with source IP address 192.168.16.1 is wanted to egress to the internet. 

Source IP     192.168.16.1 -> 11000000.10001000.00010000.00000001

Base IP       192.168.8.0  -> 11000000.10001000.00001000.00000000

Wildcard Mask 0.0.24.255   -> 00000000.00000000.00011000.11111111

As you see we are not matching both fourth and fifth bits in the third octet. So the packet with the IP address 192.168.8.0 is permitted.

Let's say now the packet with source IP 192.168.16.1 reach the Gateway.

Source IP     192.168.9.1  -> 11000000.10001000.00001001.00000001

Base IP       192.168.8.0  -> 11000000.10001000.00001000.00000000

Wildcard Mask 0.0.24.255   -> 00000000.00000000.00011000.11111111

As you see we are not matching fourth and fifth bits in third octet. Also last bit is not matching with the base IP address as per wildcard mask. So the packet with the IP address 192.168.9.1 is not permitted.

## Reference:

[IP Subnetting and Subnetting Examples](https://ipcisco.com/lesson/ip-subnetting-and-subnetting-examples/)
[Wildcard Masks in ACLs](https://www.ciscopress.com/articles/article.asp?p=3089353&seqNum=5)
---
title: IP adress ranges
author: Roel M. Hogervorst
date: '2020-03-25'
slug: ip-adress-ranges
categories:
  - other
tags:
  - internet
  - GCP
  - binary
---

For work I had to configure ip adresses in the firewall of a google cloud project. 

I did not understand the 'slash-notation', also known as CIDR notation, so this is a note to help me understand it later again. 

(This is about ip4 and not ip6)
The CIDR notation is an ip adres xxx.xxx.xxx.xxx followed by a slash '/' and a number.

The number after the slash is somesort of mask that tells what part of the network is important. In fact it tells what bits are important from left to right but to understand 
how it works you have to do a bit of mental rotation. 

An IP-adress consists of groups seperated by the dot. But in 'reality' the internet works with bits. So every group is 8 bits (an octet) and can take a number between 0 and 255 which is 2 to the power of 8 $2^{8} = 256$ but computer scientists count from zero.

so every octet is actually something like this:

```
0 0 0 0 0 0 0 0  # number 0
0 0 0 0 0 0 0 1  # number 1
0 0 0 0 0 0 1 0  # number 2
... (etc)
1 1 1 1 1 1 1 1  # number 255
```

And we can declare how many of these bits are important.
So for instance we can say '245/7'

```
1 1 1 1 0 1 0 1 # 245
! ! ! ! ! ! ! X # (! is important)
```

But because we say only the first 7 are important the last number can be either a 1 
or a zero, so both 245 and 244 are allowed:

```
1 1 1 1 0 1 0 1 # 245
1 1 1 1 0 1 0 0 # 244
```

But in internet-land there are 4 of these octets, and so there are 4*8=32 bits and we just count from left to right. 


Now these notes are hosted on netlify, what is the ip adres:

```
# this doesn't work on windows, it's a unix/linux command
nslookup notes.rmhogervorst.nl
```

Returns 143.93.108.123 

What is that in octets?

```{r}
number2binary = function(number, noBits) {
       binary_vector = rev(as.numeric(intToBits(number)))
       if(missing(noBits)) {
          return(binary_vector)
       } else {
          binary_vector[-(1:(length(binary_vector) - noBits))]
       }
    }
purrr::map(c(143, 93, 108, 123),number2binary)
```

So the four octets will be:
```
[[1]]
 [1] 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 1 0 0 0 1 1 1 1

[[2]]
 [1] 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 1 0 1 1 1 0 1

[[3]]
 [1] 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 1 1 0 1 1 0 0

[[4]]
 [1] 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 1 1 1 1 0 1 1
```

So `143.93.108.123/32` translates to all 32 bits are important

but allowing `143.93.108.123/30` allows access for 

```
 143.93.108.120
 143.93.108.121
 143.93.108.122
 143.93.108.123 
```

If you don't want to do this everytime try out this website:

- This is a great tool to see what the notation actually does [netmask tool](https://www.ultratools.com/tools/netMask)

References

- [CIDR stands for Classless Inter-Domain Routing](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing)

- Copied the function from a [stackoverflow page](https://stackoverflow.com/questions/6614283/converting-decimal-to-binary-in-r)

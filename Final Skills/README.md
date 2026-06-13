# Final Skills

Here lies two practice papers from Canvas, A and B. 

Both are essentially identical other than IPs and VLAN IDs

## Structure

10 minutes reading time
120 minutes exam time
5 minutes informal "leave-devices-in-exec-and-sign-out" time

Therefore the "two hour exam" is actually 135 minutes.

You *are* allowed to write on your paper during reading time, so figure out your IPs first (VLSM done for you)

Lab journals were not checked during my session for whatever reason... Take this with a grain of salt, since in networks and switching, everyones journal was.

## The Exam

It was really easy:

There were three routers, one switch and one ungraded Ethernet PC

Everything on the practice paper was present on the real paper. There were no additions or exclusions

There were only TWO VLANs (and one management); only one NAT pool covering whole internal space (one NAT ACL), OSPF single base area (never said to make anything a passive interface, but I did so anyways because this is how we were taught - to only send HELLO packets to routers that participate in OSPF only), DHCP on one VLAN (two excluded addresses), loopbacks in /32 range, no loopback on the internal router, just database loopback on middle router, PPP and CHAP, and one ACL that consisted of two permits, two denys, one permit any, and the implicit deny at the end. TELNET was enabled on two routers with an access-class. MOTD on one single router just like the practice (I think they're trying to exploit muscle memory of people MOTD-ing every device which is a minor error, quite scummy). IP addresses are *not* given, but VLSM is done - mine consisted of "use the first IP" and "use the second IP" whereby the practice only wanted last IP (which sucked.) 

Don't stress about other NAT modes, its almost guaranteed to be PAT (overload NAT)
Same with routing protocol, its probably guaranteed to be OSPF

Both of these protocols are industry standard and are used basically everywhere, makes no sense to examine older unused protocols in a practical

## Mistakes I Made

The practice exams usually wanted DHCP on the middle router and thus the internal router needed a helper-address to forward DHCP broadcasts. I was complacent in reading the exam and actually did this, which was wrong since the DHCP was meant to be on internal. Everything worked of course, but then it took me a second readthrough of the exam during testing to realise I put DHCP on the wrong router and reverted my configuration to make it correct thankfully. Basically, read the device names!

## Advice to give

To any future students, I advise:

- Complete the practice exams, but don't be complacent in your knowledge: while the real exam is easier, its very important you know EVERY topic taught
- Canvas mentioned lab 6C is very good practice: I entirely agree, do this lab, its effectively the final exam
- Remember CHAP authentication uses opposite hostname usernames (if you don't know what this means I highly recommend you understand cause this is a major)
- ACL placement, study this, along with ACL ordering!
- Do ACLs last, so you can ping every device from every device to test your network
- If DHCP is not on your internal router, it WILL NOT WORK until you've done the routing protocol for return traffic even though DHCP is first in the paper before OSPF
- Check your interface states: SVI is always down by default, router interfaces down by default
- Remember to trunk your switchport g1/0/11: somehow I forgot this and was wondering why nothing was working, then I realised I was too caught up in the actual routing I forgot about the switching
- The exam says to not advertise the ISP link: this literally means do not write "network <public ip> 0.0.0.3 area 0" in OSPF config
- This is routing principles, learn what IP classes are. I've had several people say "oh all the exams have 192.168" IPs they're all the same... No... This IP range is private class C, and CANNOT be routed, its special. Learn this.
- After NAT is configured, your ISP router therefore CANNOT ping internal IP addresses. This is normal given literally what network address translation does: converts private IPs to a set of public IPs. If you're a gamer, this is exactly what port forwarding is/does
- If you're using AI to assist, take its answers with a grain of salt. We have different Cisco IOS versions, and sometimes the AIs are overconfident in their wrong answers that go against what we've been taught in classes
- Best practices are not exactly marked, i.e., disabling unused switchports is not a requirement nor will it punish you
- Write down or learn wildcard masks: this is pretty important given you'll be using these a lot. In some IOS versions including ours, typing a SUBNET mask in a wildcard mask parameter will be automatically be converted to a wildcard mask - Packet tracer doesn't do this, but I advise not to rely on this implicit conversion as its a bit flaky and can fail
- The virtual machine has windows Notepad. You can use it to write ACLs, notes, and whatever else you might need


## Good Luck

You got this bro, lock in, do the practices, you'll be fine. Its really not that bad.

Joey Manani
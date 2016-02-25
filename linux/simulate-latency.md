# Simulating latency

In certain circumstances it may be useful to simulate poor network conditions 
to cover edge cases.

    # Enable Network Emulator Kernel module
    modprobe sch_netem

    # Verify that it is enabled
    lsmod

    # Add a 300 ms ping delay on eth0
    tc qdisc add dev eth0 root netem delay 300ms
    
    # Change ping delay to 25ms
    tc qdisc replace dev eth0 root netem delay 25ms (Change the ping delay to 25ms)

    # Change ping delay to vary between 20-100 ms
    tc qdisc replace dev eth0 root netem delay 100ms 20ms distribution normal

    # View current settings
    tc -s qdisc

    # Remove netem setting on eth0
    tc qdisc del dev eth0 root netem

# References

http://www.linuxfoundation.org/collaborate/workgroups/networking/netem#Packet_loss

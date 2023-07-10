# DPDK-based Probe Generation and eBPF-based Packet Processing with XDP

This repository contains the code and instructions for using DPDK-based probe generation and eBPF-based packet processing with XDP for network scanning.

## DPDK-based Probe Generation

The DPDK-based probe generation tool allows you to send probe packets to scan a range of network addresses and ports. It leverages DPDK libraries for high-performance packet processing.

### Usage

1. Configure DPDK environment:

export RTE_SDK=/path/to/dpdk
export RTE_TARGET=your_target_platform


2. Build the DPDK-based probe generation application:

cd $RTE_SDK
make


3. Launch the DPDK-based probe generation application:

sudo ./build/app/probe_generation --target-port=<port> --scan-addresses=<start_address>-<end_address> --scan-ports=<start_port>-<end_port>


- Replace `<port>` with the target port number to send the probe packets.
- Replace `<start_address>` and `<end_address>` with the range of network addresses to be scanned.
- Replace `<start_port>` and `<end_port>` with the range of port numbers to be scanned.

`DPDk-based -l 0-7 -- -c /etc/dpdk/probe.yaml --queues 1 --portmask 0xff`
`./rcv_handle -l 8-13 -n 1 -- -q 1 -p 0xff -s`

### usage
1 -p --portmask => port maske e.g. 0xFFFF).:

2 -P --portmap => port map(in '(x, y),(b,z)'

3 -q --queues => The amount of RX  per port (default value is 1).

4 -x --promisc => promiscuous mode on all enabled ports.

5 -s --stats =>  real-time packet counter stats

6 -c --configuration config file path


## eBPF-based Packet Processing with XDP

The eBPF-based packet processing with XDP allows you to handle and process incoming packets using eBPF programs attached to XDP hooks within the Linux kernel.

### Usage

1. Compile the eBPF program:

clang -O2 -target bpf -c packet_processing_ebpf.c -o ebpf_program.o


2. Load the eBPF program using `ip` command:

sudo ip link set dev <interface_name> xdp obj ebpf_program.o


- Replace `<interface_name>` with the name of the network interface to attach the XDP program.

3. Monitor the packet processing using `tcpdump` or other packet capture tools:

sudo tcpdump -i <interface_name>


- Replace `<interface_name>` with the name of the network interface.

## Contributing

Contributions to this repository are welcome. If you encounter any issues or have suggestions for improvements, please feel free to open an issue or submit a pull request.

## License

This project is licensed under the [MIT License](LICENSE).

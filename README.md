NS2 Network Simulation Experiments
This document outlines various NS2 simulation setups using OTcl scripts. Each section includes the objective, network topology, and corresponding code.

1. 🌐 Network Without Traffic
Objective: Create nodes and links without generating any traffic.
set ns [new Simulator]

set tracefile [open out.tr w]
set namfile [open out.nam w]
$ns trace-all $tracefile
$ns namtrace-all $namfile

set n0 [$ns node]
set n1 [$ns node]
set n2 [$ns node]
set n3 [$ns node]

$ns duplex-link $n0 $n1 1Mb 10ms DropTail
$ns duplex-link $n1 $n2 1Mb 10ms DropTail
$ns duplex-link $n2 $n3 1Mb 10ms DropTail

proc finish {} {
    global ns tracefile namfile
    $ns flush-trace
    close $tracefile
    close $namfile
    exec nam out.nam &
    exit 0
}

$ns at 5.0 "finish"
$ns run

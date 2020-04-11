## Role Variables


**tuned_profile**: The profile to set. Set to `recommended` by default. Basic profiles that are available are:

- balanced                    - General non-specialized tuned profile
- desktop                     - Optimize for the desktop use-case
- hpc-compute                 - Optimize for HPC compute workloads
- latency-performance         - Optimize for deterministic performance at the cost of increased power consumption
- network-latency             - Optimize for deterministic performance at the cost of increased power consumption, focused on low latency network performance
- network-throughput          - Optimize for streaming network throughput, generally only necessary on older CPUs or 40G+ networks
- powersave                   - Optimize for low power consumption
- throughput-performance      - Broadly applicable tuning that provides excellent performance across a variety of common server workloads
- virtual-guest               - Optimize for running inside a virtual guest
- virtual-host                - Optimize for running KVM guests

**tuned_daemon**: If true, enable the daemon to support dynamic tuning.

**tuned_dynamic_tuning**: Enable dynamic tuning.

**tuned_sleep_interval**: Sleep interval for checking for events, in seconds.

**tuned_update_interval**: Update interval for dynamic tuning, in seconds.

**tuned_enable_recommend**: Enable recommend functionality.

**tuned_reapply_sysctl**: Wether to apply sysctl from `/etc` after tuned's sysctl are
applied.


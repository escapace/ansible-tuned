# escapace.tuned

This Ansible role installs and configures the tuned system tuning daemon on Linux systems. Tuned is a daemon that monitors system activity and dynamically adjusts system settings to optimize performance for different workloads. The role supports both single profile configuration and multiple profile stacking, with automatic profile recommendation based on system characteristics.

## Role Variables

### tuned_profile

The tuned profile(s) to activate. Can be specified as a string for a single profile or a list for multiple profiles. Defaults to `recommended` which automatically selects the best profile for the system, or `aws` when running on EC2 instances.

**Type**: `string` or `list`  
**Default**: `recommended` (or `aws` for EC2 instances)

#### Available Profiles

| Profile                   | Description                                                                                                                   |
| ------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| `accelerator-performance` | Throughput performance based tuning with disabled higher latency STOP states                                                  |
| `atomic-guest`            | Optimize virtual guests based on the Atomic variant                                                                           |
| `atomic-host`             | Optimize bare metal systems running the Atomic variant                                                                        |
| `aws`                     | Optimize for AWS EC2 instances                                                                                                |
| `balanced`                | General non-specialized tuned profile                                                                                         |
| `balanced-battery`        | Balanced profile biased towards power savings changes for battery                                                             |
| `desktop`                 | Optimize for the desktop use-case                                                                                             |
| `hpc-compute`             | Optimize for HPC compute workloads                                                                                            |
| `intel-sst`               | Configure for Intel Speed Select Base Frequency                                                                               |
| `latency-performance`     | Optimize for deterministic performance at the cost of increased power consumption                                             |
| `network-latency`         | Optimize for deterministic performance at the cost of increased power consumption, focused on low latency network performance |
| `network-throughput`      | Optimize for streaming network throughput, generally only necessary on older CPUs or 40G+ networks                            |
| `optimize-serial-console` | Optimize for serial console use                                                                                               |
| `powersave`               | Optimize for low power consumption                                                                                            |
| `recommended`             | Automatically select the best profile for the system                                                                          |
| `throughput-performance`  | Broadly applicable tuning that provides excellent performance across a variety of common server workloads                     |
| `virtual-guest`           | Optimize for running inside a virtual guest                                                                                   |
| `virtual-host`            | Optimize for running KVM guests                                                                                               |

### Other Variables

**tuned_daemon**: Enable the tuned daemon.
**Type**: `boolean`  
**Default**: `true`

**tuned_dynamic_tuning**: Enable dynamic tuning. When disabled, only static tuning will be used. Can be individually disabled in plugins.  
**Type**: `boolean`  
**Default**: `true`

**tuned_sleep_interval**: TuneD daemon sleep interval for checking events, in seconds. Controls responsiveness time and power savings.  
**Type**: `integer`  
**Default**: `1`

**tuned_update_interval**: Update interval for dynamic tuning, in seconds. Must be multiple of sleep_interval. Set to 0 to disable periodic wakeups.  
**Type**: `integer`  
**Default**: `10`

**tuned_enable_recommend**: Enable recommend functionality. When disabled, recommend command is unavailable and returns hardcoded profile (balanced).  
**Type**: `boolean`  
**Default**: `true`

**tuned_reapply_sysctl**: Reapply user sysctl settings after TuneD sysctl settings. When true, TuneD won't override user-provided system sysctl settings.  
**Type**: `boolean`  
**Default**: `true`

## Examples

### Single Profile

```yaml
- hosts: servers
  roles:
    - role: escapace.tuned
      vars:
        tuned_profile: 'throughput-performance'
```

### Multiple Profiles

```yaml
- hosts: servers
  roles:
    - role: escapace.tuned
      vars:
        tuned_profile:
          - 'latency-performance'
          - 'virtual-guest'
```

### Custom Configuration

```yaml
- hosts: servers
  roles:
    - role: escapace.tuned
      vars:
        tuned_profile: 'network-latency'
        tuned_dynamic_tuning: false
        tuned_sleep_interval: 5
        tuned_update_interval: 30
```

## Role Variables

**tuned_use_recommended_profile**: Set the profile which is recommended for the
machine instead of the one given in 'profile'.

**tuned_profile**: The profile to set. Unused if `use_recommended_profile` is true.
Basic profiles that are available are `balanced`, `powersave`,
`throughput-performance`, and `latency-performance`. More profiles may be
available depending on OS version.

**tuned_daemon**: If true, enable the daemon to support dynamic tuning.

**tuned_dynamic_tuning**: Enable dynamic tuning.

**tuned_sleep_interval**: Sleep interval for checking for events, in seconds.

**tuned_update_interval**: Update interval for dynamic tuning, in seconds.

**tuned_enable_recommend**: Enable recommend functionality.

**tuned_reapply_sysctl**: Wether to apply sysctl from `/etc` after tuned's sysctl are
applied.


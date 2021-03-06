..
    Warning: Do not edit this file. It is automatically generated from the
    software project's code and your changes will be overwritten.

    The tool to generate this file lives in openstack-doc-tools repository.

    Please make any changes needed in the code, then run the
    autogenerate-config-doc tool from the openstack-doc-tools repository, or
    ask for help on the documentation mailing list, IRC channel or meeting.

.. _nova-workarounds:

.. list-table:: Description of workarounds configuration options
   :header-rows: 1
   :class: config-ref-table

   * - Configuration option = Default value
     - Description

   * - ``handle_virt_lifecycle_events`` = ``True``

     - (Boolean) Enable handling of events emitted from compute drivers.

       Many compute drivers emit lifecycle events, which are events that occur when, for example, an instance is starting or stopping. If the instance is going through task state changes due to an API operation, like resize, the events are ignored.

       This is an advanced feature which allows the hypervisor to signal to the compute service that an unexpected state change has occurred in an instance and that the instance can be shutdown automatically. Unfortunately, this can race in some conditions, for example in reboot operations or when the compute service or when host is rebooted (planned or due to an outage). If such races are common, then it is advisable to disable this feature.

       Care should be taken when this feature is disabled and 'sync_power_state_interval' is set to a negative value. In this case, any instances that get out of sync between the hypervisor and the Nova database will have to be synchronized manually.

       For more information, refer to the bug report:

        https://bugs.launchpad.net/bugs/1444630

       Interdependencies to other options:

       * If ``sync_power_state_interval`` is negative and this feature is disabled, then instances that get out of sync between the hypervisor and the Nova database will have to be synchronized manually.

   * - ``disable_rootwrap`` = ``False``

     - (Boolean) Use sudo instead of rootwrap.

       Allow fallback to sudo for performance reasons.

       For more information, refer to the bug report:

        https://bugs.launchpad.net/nova/+bug/1415106

       Possible values:

       * True: Use sudo instead of rootwrap

       * False: Use rootwrap as usual

       Interdependencies to other options:

       * Any options that affect 'rootwrap' will be ignored.

   * - ``disable_libvirt_livesnapshot`` = ``True``

     - (Boolean) Disable live snapshots when using the libvirt driver.

       Live snapshots allow the snapshot of the disk to happen without an interruption to the guest, using coordination with a guest agent to quiesce the filesystem.

       When using libvirt 1.2.2 live snapshots fail intermittently under load (likely related to concurrent libvirt/qemu operations). This config option provides a mechanism to disable live snapshot, in favor of cold snapshot, while this is resolved. Cold snapshot causes an instance outage while the guest is going through the snapshotting process.

       For more information, refer to the bug report:

        https://bugs.launchpad.net/nova/+bug/1334398

       Possible values:

       * True: Live snapshot is disabled when using libvirt

       * False: Live snapshots are always used when snapshotting (as long as there is a new enough libvirt and the backend storage supports it)

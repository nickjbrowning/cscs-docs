[](){#ref-platform-cwp}
# Climate and Weather Platform

The Climate and Weather Platform (CWP) provides compute, storage and support to the climate and weather modeling community in Switzerland.

## Getting Started

### Getting access

Project administrators (PIs and deputy PIs) of projects on the CWP can to invite users to join their project, before they can use the project's resources on Alps.

This is currently performed using the [account and resource management tool][ref-account-ump].

Once invited to a project, you will receive an email, which you can need to create an account and configure [multi-factor authentication][ref-mfa] (MFA).

## Systems

Santis is the system deployed on the Alps infrastructure for the climate and weather platform.
Its name derives from the highest mountain Säntis in the Alpstein massif of North-Eastern Switzerland.

<div class="grid cards" markdown>
-   :fontawesome-solid-mountain: [__Santis__][ref-cluster-santis]

    Santis is a large [Grace-Hopper][ref-alps-gh200-node] cluster.
</div>

[](){#ref-cwp-storage}
## File systems and storage

There are three main file systems mounted on the CWP system Santis.

| type |mount | filesystem |
| -- | -- | -- |
| Home | /users/$USER | [VAST][ref-alps-vast] |
| Scratch | `/capstor/scratch/cscs/$USER` | [Capstor][ref-alps-capstor] |
| Project | `/capstor/store/cscs/userlab/<project>` | [Capstor][ref-alps-capstor] |

### Home

Every user has a [home][ref-storage-home] path (`$HOME`) mounted at `/users/$USER` on the [VAST][ref-alps-vast] filesystem.
The home directory has 50 GB of capacity, and is intended for configuration, small software packages and scripts.

### Scratch

The Scratch filesystem provides temporary storage for high-performance I/O for executing jobs.

See the [Scratch][ref-storage-scratch] documentation for more information.

The environment variable `SCRATCH=/capstor/scratch/cscs/$USER` is set automatically when you log into the system, and can be used as a shortcut to access scratch.

!!! warning "scratch cleanup policy"
    Files that have not been accessed in 30 days are automatically deleted.

    **Scratch is not intended for permanent storage**: transfer files back to the [Store][ref-storage-store] after job runs.

### Project Store

Project storage is backed up, with no cleaning policy, as intermediate storage space for datasets, shared code or configuration scripts that need to be accessed from different vClusters.

The environment variable `PROJECT` is set automatically when you log into the system, and can be used as a shortcut to access the Store path for your primary project.

Hard limits on capacity and inodes prevent users from writing to [Store][ref-storage-store] if the quota is reached.
You can check quota and available space by running the [`quota`][ref-storage-quota] command on a login node or ela.

!!! warning
    It is not recommended to write directly to the `$PROJECT` path from jobs.

# allocgpu
Script for automatic GPU sharing and allocation on server.

This script supports detecting free GPUs, allocating free GPUs on a server and automatic queueing for GPU tasks. Users can also set maximum GPUs to use and activate specific conda environment for the task.

## Usage

The basic usage is to add any script after allocgpu:
``
source <path_to_allocgpu> script
``

And the script will automatically allocate 1 free GPU on the server for the `script` to run. When there are no free GPUs, it would retry every 5 minutes for the next free GPU to use for 12 hours.

Or, to modify the parameters of `allocgpu`:

``
source <path_to_allocgpu> -g <gpus_to_use> --max_wait_time <maximum_time_to_wait> -c <conda_env_name> -a <use_all_free_gpus_when_timeout> -x <max_gpus_for_current_user> script
``

This would allocate `<gpus_to_use>` GPUs. Before running `script`, `conda activate <conda_env_name>` would be run first. `allocgpu` would only check the first `<max_gpus_for_current_user>` GPUs on the server, and if the remaining GPUs is less than `<gpus_to_use>`, `allocgpu` would retry every 5 minutes for `<maximum_time_to_wait>`. If timeout and free GPU count is still less than `<gpus_to_use>`, setting `-a` would allocate all remaining GPUs on the server.

## How to use
1. Put this file in some folders in `~/`, like `~/scripts/`.
2. (optional) Add the folder mentioned in the previous step into `PATH` for convenience.
3. Run the script.

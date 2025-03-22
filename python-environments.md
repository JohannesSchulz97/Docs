# Managing Python and System Environments

Python environments are essential for managing dependencies and ensuring that projects have access to the correct versions of libraries. Two popular package managers with built-in tools for creating and managing Python environments are `conda` and `pip` with `virtualenv`. While `pip` is compatible with conda if used in the right way, `virtualenv` becomes obsolete when managing isolated environments with `conda`.

## Pip

`pip` is the default Python package manager, dedicated to installing Python packages. While it provides access to a broader range of Python packages than `conda`, it lacks conda’s safeguards against dependency conflicts.

Project environments can be isolated with `virtualenv` when using `pip` alone, but this adds another layer of management. When combined with `conda`, the best practice is to use `pip` only after installing all possible dependencies with `conda` first.

## Conda

`conda` is a system package manager, meaning it operates on a higher level than a specific coding language package manager such as `pip`. It allows users to install entire software stacks such as Python + Django + Celery + PostgreSQL + nginx. Additionally, it is not limited to Python but supports R, Node.js, Java, C, C++, Perl, and more.

Conda has an `env` system that allows you to manage these installations across multiple isolated environments (in contrast to `virtualenv`, environments are managed globally and are stored in `anaconda3/envs/`). It performs installations in an isolated, userspace manner, meaning you can set up complex software stacks without needing root privileges. In many ways, conda serves as a lightweight userspace alternative to Docker for isolating software stacks.

By default, when you install conda for the first time, the `base` environment is auto-activated. This remains in use until you create and switch to another environment. You don’t need a third-party environment management system with conda.



## Recommended Approach

1. For any new project, create a separate `conda` environment with a descriptive and unique name.
2. Install dependencies with `conda` whenever possible.
3. For packages unavailable via `conda`, use the version of `pip` **included in** `conda` to install required `pip` dependencies into your project's `conda` environment. Ensure the conda environment is activated before using `pip`.
4. Always activate the respective environment before running code.

The `conda` `base` environment should be reserved for managing system-level tools. It’s recommended to deactivate the automatic `base` environment activation upon shell startup to prevent accidentally installing packages there:

```bash
conda config --set auto_activate_base false
```

It’s good practice to regularly save the environment (all installed dependencies) in a dedicated file to ensure easy recovery and consistency across different machines and users:

```bash
conda env export > environment.yml
```

To only view packages that have been explicitly installed with conda use: 

```bash
conda env export --from-history > environment.yml
```
This however wont show the packages installed with `pip` anymore.
These can be separately stored with
```bash
pip freeze > requirements.txt
```
Following these best practices ensures smooth environment management, minimizes dependency issues, and keeps projects organized.



## Important Commands

- Create a new environment:    
`conda create --name myenv pkg1==ver1 pkg2==ver2 ...`
Specification of packages to install into the evironment as well as their version numbers is optional.
- Activate the environment:    `conda activate myenv`
- Deactivate the environment:   `conda deactivate`
- List all environments:   `conda env list`
- Rename an environment:    `conda rename --name old_name new_name`
- Delete an environment:   `conda remove --name myenv --all`
- List installed packages: `conda list`
- Install a package: `conda install [-c channel_name] package_name`. The **default channel** (managed by Anaconda) does not always have all the packages. A quite popular alternative with an often broader selection of packages is `conda-forge`.
The recommended approach is to use the default channel whenever possible and download them from `conda-forge` only if needed.
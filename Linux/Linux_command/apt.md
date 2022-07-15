# apt

## apt remove package

### `apt remove package_name`
remove all executable binary file, but keeps corresponding configuration and data files

### `apt remove --purge package_name` and `apt purge package_name`
remove all files related to package_name, including binary files and global configuration fils,
but remains dependency package and configuration file that in your $HOME directory.

### `apt autoremove`
remove all orphaned packages in system, you can run this after purge some packages


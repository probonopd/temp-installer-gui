# Graphical installer frontend

__WORK IN PROGRESS__. DO NOT USE ON SYSTEMS WITH VALUABLE DATA AS IT MAY OVERWRITE THE CONTENTS OF YOUR DISK. This is a temporary home until this is properly tested and integrated.

![](https://user-images.githubusercontent.com/2480569/93003383-836da580-f53e-11ea-976c-76c1a29a27e0.png)

## Theory of operation

* The graphical installer frontend is an assistant (wizard) that guides the user through the installation. It consists of multiple pages.
* None of the actual "business logic" (the actual installer) is implemented in the graphical installer frontend. Instead, a shell script is called to perform the installation.
* The graphical installer frontend shows a progress bar during installation. This is calculated by bytes on the target disk divided by bytes needed
* When the disk selection screen is shown, the graphical installer frontend will invoke the shell script with `INSTALL`

## Environment variables

Environment variables are the proposed way for communicating back and forth between the installer script and the graphical installer frontend.

### For retrieving the required space on the target disk

* `INSTALLER_PRINT_MIB_NEEDED=YES`

When this is present, the installer must respond with just the number of bytes required on the target disk, e.g., `INSTALLER_MIB_NEEDED=2158`. The installer script must write this to stderr and then exit with no further action.

### For performing the installation

When these are present, the installer script must proceed with the installation with no further questions asked.

* `INSTALLER_ROOT_PASSWORD`, e.g., `p!wrd&ejwH`
* `INSTALLER_USERNAME`, e.g., `john`
* `INSTALLER_USER_PASSWORD`, e.g., `7§97jhejwH`
* `INSTALLER_HOSTNAME`, e.g., `johns-computer`
* `INSTALLER_DEVICE`, e.g., `da1`
* `INSTALLER_LANGUAGE`, e.g., `zh`
* `INSTALLER_COUNTRY`, e.g., `CN`
* `INSTALLER_LOCALE_UTF8`, e.g., `zh_CN.UTF-8`

During installation, the installer script should make liberal use of `stdout` and `stderr`. These will not be shown to the user by default but may be helpful for debugging.

The installer script must exit with the exit code `0` on success and may use any other exit codes otherwise. If so desired, we can align on different exit codes that can trigger different reactions in the graphical installer frontend.

## Trademarks

According to the [FreeBSD Trademark Usage Terms and Conditions](https://freebsdfoundation.org/legal/trademark-usage-terms-and-conditions/),

> Any individual, organization, or company may, without explicit permission from the Foundation, use the FreeBSD Marks to show support for the Project or as part of a notice to users that a product incorporates the FreeBSD operating system.

Nevertheless an official request has been made to incorporate the FreeBSD logo into the graphical installer frontend, as a means to signal to users that what gets installed is the real FreeBSD system rather than some modified variant of it.

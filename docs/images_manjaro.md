# ovos-image-arch-recipe

Make a manjaro based OpenVoiceOS image

source code: https://github.com/OpenVoiceOS/ovos-image-arch-recipe/

## Building

### Docker Automated Image Building
The included Dockerfile can be used to build a default image in a Docker environment.

The following dependencies must be installed on the build system before running the
container:

* [chroot](https://wiki.debian.org/chroot)
* [qemu-user-static](https://wiki.debian.org/QemuUserEmulation)

First, create the Docker container:
```shell
docker build . -t ovos-image-builder
```

Then, run the container to create a OVOS Image. Set `CORE_REF` to the branch of
`ovos-core` that you want to build and `RECIPE_REF` to the branch of `ovos-image-recipe`
you want to use. Set `MAKE_THREADS` to the number of threads to use for `make` processes.
```shell
docker run \
-v /home/${USER}/output:/output:rw \
-v /run/systemd/resolve:/run/systemd/resolve \
-e CORE_REF=${CORE_REF:-dev} \
-e RECIPE_REF=${RECIPE_REF:-master} \
-e MAKE_THREADS=${MAKE_THREADS:-4} \
--privileged \
--network=host \
--name=ovos-image-builder \
ovos-image-builder
```

The entire build process will generally take several hours; it takes 1-2 hours
on a build server with 2x Xeon Gold 5118 CPUs (48T Total).

### Interactive Image Building

The scripts in the `automation` directory are available to help automate building a default image.
For building an image interactively:

```shell
bash automation/prepare.sh
bash /tmp/run_scripts.sh
```

The below documentation describes how to manually build an image using the individual scripts in this repository.

## Steps

### Getting Started

The scripts and overlay files in this repository are designed to be applied to a base image
as the `root` user. It is recommended to apply these scripts to a clean base image. 
Instructions are available [at opensource.com](https://opensource.com/article/20/5/disk-image-raspberry-pi).

> **Note**: The GUI shell is not installable under some base images

For each step except [boot_overlay](#boot_overlay), the directory corresponding
to the step should be copied to the mounted image and the script run from a terminal
`chroot`-ed to the image. If running scripts from a booted image, they should be
run as `root`.

### Preparation
From the host system where this repository is cloned, running `prepare.sh <base_image>`
will copy boot overlay files, mount the image, mount DNS resolver config from the host system,
copy all other image overlay files to `/tmp`, and `chroot` into the image. From here, you can
run any/all of the following scripts to prepare the image before [cleaning up](#Clean-Up)

### core_configuration
Configures user accounts and base functionality for RPi. `ovos` user is created with proper permissions here.

At this stage, a booted image should resize its file system to fill the drive it is flashed to. Local login and 
ssh connections should use `ovos`/`ovos` to authenticate and be prompted to change password on login.

### network_manager
Adds Balena wifi-connect to enable a portal for connecting the Pi device to a Wi-Fi network.

A booted image will now be ready to connect to a network via SSID `OVOS`.

### sj201
For SJ201 board support, the included script will build/install drivers, add required overlays, install required system 
packages, and add a systemd service to flash the SJ201 chip on boot. This will modify pulseaudio and potentially overwrite 
any previous settings.

>*Note:* Running this scripts grants GPIO permissions to the `gpio` group. Any user that interfaces with the SJ201 board
> should be a member of the `gpio` group. Group permissions are not modified by this script

Audio devices should now show up with `pactl list`.
Audio devices can be tested in the image by recording a short audio clip and playing it back.

```shell
parecord test.wav
paplay test.wav
```

### embedded_shell
Installs ovos-shell and mycroft-gui-app. Adds and enables ovos-gui.service to start the shell
on system boot.

The image should now boot to the GUI shell.

### ovos_core
Installs `ovos-core` and dependencies. Configures services for core modules.

At this stage, the image is complete and when booted should start OVOS.

### dashboard
Installs the [OVOS Dashboard](https://github.com/openvoiceos/ovos-dashboard) and service
to start the dashboard from the GUI.

From the GUI `Settings` -> `Developer Settings` menu, `Enable Dashboard` will now start
the dashboard for remote access to device diagnostics.

### camera
Installs `libcamera` and other dependencies for using a CSI camera.

The default camera skill can be used to take a photo; `libcamera-apps` are also
installed for testing via CLI.

### splash_screen
Enables a custom splash screen and disables on-device TTY at boot.

On boot, a static image should be shown until the GUI Shell starts.

### Clean Up
`cleanup.sh` removes any temporary files from the mounted image before unmounting it.
After running `cleanup.sh`, the image is ready to burn to a drive and boot.


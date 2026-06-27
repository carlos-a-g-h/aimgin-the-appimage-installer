# AIMGIN, The AppImage "Installer"

## About this repo

I made an installer for AppImages. The AppImages are installed by decompressing them into a system and integrating the application

AIMGIN can work with AppImages and SQUASHFS compressed AppDirs

For the sake of not repeating myself throughout this README file, I will refer to both AppImages and AppDirs compressed as SQUASHFS files as "application" or "apps"

### Ok, hear me out

We can all aggree that installing AppImages by decompressing them goes against how AppImages are supposed to be used, yes, but this is not a disadvantage on systems that are ran from compressed media (such as live systems for example), it is an improvement

### Size comparisons

For the following real test I had two SQUASHFS filesystems, each holding two different versions of the same OS

- File A, "asere.squashfs" (older version) has AppImages directly copied inside it, these are normal AppImage files and they are not decompressed

- File B, "asere-2026-05-22.squashfs" (most recent version) has all of its AppImages decompressed

In the following picture, I'm comparing the disk space occupied by two SQUASHFS filesystems

<img width="1920" height="1080" alt="SQUASHFS filesystems" src="https://github.com/carlos-a-g-h/aimgin-scripts/blob/main/2026-05-22-142133_1920x1080_scrot.png?raw=true" />

In the following picture I mounted both filesystems to analyze the real size of "/usr/appimages/" in each of them

<img width="1920" height="1080" alt="AppImages VS decompressed AppImages" src="https://github.com/carlos-a-g-h/aimgin-scripts/blob/main/2026-05-22-142414_1920x1080_scrot.png?raw=true" />

The SQUASHFS compressed filesystem with bundled AppImages (File A) is heavier, because AppImages are files that are already compressed and MKSQUASHFS cannot compress them when building the filesystem image

The SQUASHFS compressed filesystem with decompressed AppImages (File B) is lighter, in this case even with almost 4 times the occupied size in AppImages, this is because MKSQUASHFS compressed the entire filesystem including the applications that are provided as AppImages

### Conclusion

This is just yet another way to use AppImages, again, NOT recommended for traditional systems due to disk space usage, but you can use it in a traditional setup if you think disk space is cheap (if you already use Flatpaks or Snaps, you probably already think like that lol)

## How to use

[![Easier than your mom](https://raw.githubusercontent.com/carlos-a-g-h/aimgin-scripts/refs/heads/main/Screenshot_20260607_175040_mpv.jpg)](ttps://ia902909.us.archive.org/5/items/appimage_installer_sh/appImage_installer_demo_by_carlos-a-g-h.mp4)

Watch a video [here](https://archive.org/download/appimage_installer_sh/appImage_installer_demo_by_carlos-a-g-h.mp4)

The video was uploaded to [the internet achive](https://archive.org/details/appimage_installer_sh) as well as this repo

### Requirements

The requirements depend on how much you want to do. If you want the full experience, install "yad" (for a GUI instead of a TUI), "wget" (to grab apps from the internet using the UI) and "squashfs-tools" (for dealing with SQUASHFS files)

### Simple installation and usage instructions

Step 1: [Download the repo](https://github.com/carlos-a-g-h/aimgin-the-appimage-installer/archive/refs/heads/main.zip) or git clone it and unzip it

Step 2: Run "Setup.Install.desktop" to install aimgin

Step 3: Run "aimgin.desktop" or "AIMGIN, The AppImage Installer" from your favorite launcher

AIMGIN will be installed in /usr/lib/aimgin

You can uninstall AIMGIN by running "Setup.Uninstall.desktop"

### The scripts

This part of the readme and below is only if you're interested in using the AIMGIN scripts from the commandline, mainly for unnatended installations

There are 2 main scripts: The the extractor script and the Installer script

#### Extractor script

$ /usr/lib/aimgin/aimgin.extractor.sh [FilePath]

The extractor script extracts the contents of the application file. After extracting, the script will run the Installer script automatically

"FilePath" is a path that leads to the application file, wether it's a normal AppImage or a SQUASHFS file

#### Installer script

$ /usr/lib/aimgin/aimgin.installer.sh [Name] [AppDir]

Performs the installation of an already extracted application, preferrably by the Extractor script

"Name" is the name for the application, make sure it does not have any special characters such as spaces or slashes

"AppDir" is the path to an AppDir

#### It's not that hard, actually

If you're on a chroot or something inyecting any new AppImages to a system, just run the Extractor script to install an AppImage. Manually running the Extractor and then the Installer should be for debugging purposes

Keep in mind that the UI script is the only part that is capable of downloading applications from the internet, but it's not meant to be used for unnatended installations. So any app files that you need from the Internet, download them sepparately using wget or whatever

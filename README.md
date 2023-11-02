# RZG2L

######################################

!renesas rzg2l manifest VLP 3.05!


repo init -u https://github.com/perplerain/RZG2L -m manifest-vlp_305.xml

repo sync

Need to download codec & graphics-lib

[https://www.renesas.com/us/en/document/sws/rz-mpu-video-codec-library-evaluation-version-rzv2l-rtk0ef0045z15001zj-v110enzip?r=1496691]

https://www.renesas.com/us/en/document/swo/rz-mpu-graphics-library-evaluation-version-v112-rzg2l-and-rzg2lc-rtk0ef0045z13001zj-v112xxzip?r=1467981


After downloading the proprietary package, please decompress them then put meta-rz-features folder at $WORK folder.

############## Build ###########

TEMPLATECONF=$PWD/meta-renesas/meta-rzg2l/docs/template/conf/ source poky/oe-init-build-env build

To build optional features (Docker, Codec or Graphics, QT5, Bootloaders, Security), add necessary layers

For Docker

$ bitbake-layers add-layer ../meta-openembedded/meta-filesystems
$ bitbake-layers add-layer ../meta-openembedded/meta-networking
$ bitbake-layers add-layer ../meta-virtualization

For Codec

$ bitbake-layers add-layer ../meta-rz-features/meta-rz-codecs

For Graphics

$ bitbake-layers add-layer ../meta-rz-features/meta-rz-graphics

For QT5

$ bitbake-layers add-layer ../meta-qt5

For Security (supported for RZ/G2[H,M,N,E], RZ/G2[L,LC,UL] and RZ/V2L)

$ bitbake-layers add-layer ../meta-rz-features/meta-rz-security

Build the target file system image using bitbake:

$ MACHINE=smarc-rzg2l bitbake core-image-<target>

<target> for these built types:
Others: bsp, weston, qt

!!!! have to change meta-renesas/meta-rz-common/recipes-debian/buster/sources/glib2.0.inc to uploaded file !!!

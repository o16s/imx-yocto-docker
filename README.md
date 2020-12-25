# imx-yocto-docker
Docker container with Yocto toolchain for i.MX SoCs.


## Quickstart

1. Rename example.env to .env and change contents.
2. On your local host: `mkdir ~/imx-linux-zeus-default`
3. Drop into the container shell: `docker-compose run imx-linux-zeus`
4. Setup the toolchain e.g.: `DISTRO=fsl-imx-fb MACHINE=imx6ull9x9evk source imx-setup-release.sh -b build` or return to an existing build folder: `source setup-environment build`
5. `bitbake core-image-minimal` - builds a minimal bootable image for MACHINE

- Make a standalone SDK that can be distributed and installed on other hosts: `DISTRO=fsl-imx-fb MACHINE=imx6ull9x9evk bitbake core-image-minimal -c populate-sdk`

## Bitbake

- `bitbake linux-imx -c fetch` - execute fetch task for linux-imx recipe
- `bitbake uboot-imx -c fetch` - execute fetch task for uboot-imx recipe
- `bitbake-layers show-layers`
- `bitbake-layers show-recipes "*-image-*"` - Show all images
- `bitbake -g <image> && cat pn-depends.dot | grep -v -e '-native' | grep -v digraph | grep -v -e '-image' | awk '{print $1}' | sort | uniq` - Show packages belonging to <image>
- `bitbake -s | grep <pkg>` - search if <pkg> is present
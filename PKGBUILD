# Based on the file created for Arch Linux by:
# Tobias Powalowski <tpowa@archlinux.org>
# Thomas Baechler <thomas@archlinux.org>

# Maintainer: Philip Müller <philm@manjaro.org>
# Maintainer: Guinux <guillaume@manjaro.org>
# Maintainer: Rob McCathie <rob@manjaro.org>

pkgbase=linux49
pkgname=('linux49' 'linux49-headers')
_kernelname=-MANJARO
_basekernel=4.9
_basever=49
_aufs=20170206
_bfq=v8r7
#_git=69973b830859bc6529a7a0468ba0d80ee5117826
pkgver=${_basekernel}.11
pkgrel=1
arch=('i686' 'x86_64')
url="http://www.kernel.org/"
license=('GPL2')
makedepends=('xmlto' 'docbook-xsl' 'kmod' 'inetutils' 'bc' 'elfutils')
options=('!strip')
source=("https://www.kernel.org/pub/linux/kernel/v4.x/linux-${_basekernel}.tar.xz"
        #"https://www.kernel.org/pub/linux/kernel/v4.x/testing/linux-${_basekernel}-{_rc}.tar.xz"
        #https://github.com/torvalds/linux/archive/v${_basekernel}.tar.gz
        #linux-${_basekernel}-${pkgrel}.tar.gz::https://github.com/torvalds/linux/archive/${_git}.tar.gz
        "http://www.kernel.org/pub/linux/kernel/v4.x/patch-${pkgver}.xz"
        # the main kernel config files
        'config' 'config.x86_64' 'config.aufs'
        # standard config files for mkinitcpio ramdisk
        "${pkgbase}.preset"
        "${pkgbase}.hook"
        "aufs4.9-${_aufs}.patch.bz2"
        'aufs4-base.patch'
        'aufs4-kbuild.patch'
        'aufs4-loopback.patch'
        'aufs4-mmap.patch'
        'aufs4-standalone.patch'
        'tmpfs-idr.patch'
        'vfs-ino.patch'
        "0001-block-cgroups-kconfig-build-bits-for-BFQ-${_bfq}.patch::http://algo.ing.unimo.it/people/paolo/disk_sched/patches/${_basekernel}.0-${_bfq}/0001-block-cgroups-kconfig-build-bits-for-BFQ-v7r11-4.5.0.patch"
        "0002-block-introduce-the-BFQ-${_bfq}-I-O-sched.patch::http://algo.ing.unimo.it/people/paolo/disk_sched/patches/${_basekernel}.0-${_bfq}/0002-block-introduce-the-BFQ-v7r11-I-O-sched-for-4.5.0.patch"
        "0003-block-bfq-add-Early-Queue-Merge-EQM-to-BFQ-${_bfq}.patch::http://algo.ing.unimo.it/people/paolo/disk_sched/patches/${_basekernel}.0-${_bfq}/0003-block-bfq-add-Early-Queue-Merge-EQM-to-BFQ-v7r11-for.patch"
        "http://algo.ing.unimo.it/people/paolo/disk_sched/patches/${_basekernel}.0-${_bfq}/0004-Turn-into-BFQ-${_bfq}-for-${_basekernel}.0.patch"

        # ARCH Patches
        'change-default-console-loglevel.patch'
        '0001-x86-fpu-Fix-invalid-FPU-ptrace-state-after-execve.patch'
        # MANJARO Patches
)
sha256sums=('029098dcffab74875e086ae970e3828456838da6e0ba22ce3f64ef764f3d7f1a'
            '23e773a670f3cac11a92c4e442405dea6d2c28fea0f914ea2ba4bea313c26541'
            '19adb7cc873dc2855beb18563520c2bc0c82432892b5ab43d9b0139281fff1e7'
            '03b5d6f8de3006e3a1849dbc2228c1f6de42abf34fa0196ad50c1e0caf8e6627'
            'd1cecc720df66c70f43bdb86e0169d6b756161c870db8d7d39c32c04dc36ed36'
            '43942683a7ff01b180dff7f3de2db4885d43ab3d4e7bd0e1918c3aaf2ee061f4'
            '5016e07c4afa91866566f6812aa7a4c69537d3abf64076c0307863f45a491e77'
            '45dcbc18e52df245218508e7f2813d2f09bf290b0d1e6f03619d7b335134b199'
            '535295f114dfe01c23e1251a1ef46a5aeab23b509c0c784be8330272736084db'
            'cc46a882be029cdcdf134915e34286db2af58b4f91a8b520dd11c15129a765c4'
            'd829062ed46e565c8fce1a43081810129e9ba0f22260cc3f68d0c8ea29677db7'
            '6b64e16324ec241ad02b540343aeed133f5b8e50a73c836e846183772f74a3d3'
            'dd62bacdfd3f16be81b0d6b5cfb2a45ae03fc0e3c126d321d198d3f19ebd84a8'
            'db7a22592a3d192dd84c84c20f361972bccfd84de346d8d7684488d118eade83'
            'e13bf072112864338cf610c8d694b8d82ae08844851b80d6d3f1cb61e112290e'
            'ee2fb11cdeab92bd93fd80044b698ff7b2abf4573a35fd891864419b3c650b23'
            'edc0693cf16900c790a4bb25ab2f7482a4c5bb1f998e59b23dea486989abbe07'
            '2dd17bdf945b973b569c8614a1de943833d7e3e4d60921308d580d944f922fa7'
            '3c7b48abd0c5a123252278edcb671e4127dd075617ab862b275b693d456d5e0e'
            '44e7e15c95af9676f715569e72688fd64304a70d2854b0f804c156d4961c72c0'
            '3e955e0f1aae96bb6c1507236adc952640c9bd0a134b9995ab92106a33dc02d9')

prepare() {
#  mv "${srcdir}/linux-${_git}" "${srcdir}/linux-${_basekernel}"
  cd "${srcdir}/linux-${_basekernel}"

  # add upstream patch
  patch -p1 -i "${srcdir}/patch-${pkgver}"

  # add latest fixes from stable queue, if needed
  # http://git.kernel.org/?p=linux/kernel/git/stable/stable-queue.git
  # enable only if you have "gen-stable-queue-patch.sh" executed before
  #patch -Np1 -i "${srcdir}/prepatch-${_basekernel}`date +%Y%m%d`"

  # set DEFAULT_CONSOLE_LOGLEVEL to 4 (same value as the 'quiet' kernel param)
  # remove this when a Kconfig knob is made available by upstream
  # (relevant patch sent upstream: https://lkml.org/lkml/2011/7/26/227)
  patch -p1 -i "${srcdir}/change-default-console-loglevel.patch"

  # Revert a commit that causes memory corruption in i686 chroots on our
  # build server ("valgrind bash" immediately crashes)
  # https://bugzilla.kernel.org/show_bug.cgi?id=190061
  patch -Rp1 -i "${srcdir}/0001-x86-fpu-Fix-invalid-FPU-ptrace-state-after-execve.patch"

  # add aufs4 support
  patch -Np1 -i "${srcdir}/aufs4.9-${_aufs}.patch"
  patch -Np1 -i "${srcdir}/aufs4-base.patch"
  patch -Np1 -i "${srcdir}/aufs4-kbuild.patch"
  patch -Np1 -i "${srcdir}/aufs4-loopback.patch"
  patch -Np1 -i "${srcdir}/aufs4-mmap.patch"
  patch -Np1 -i "${srcdir}/aufs4-standalone.patch"
  patch -Np1 -i "${srcdir}/tmpfs-idr.patch"
  patch -Np1 -i "${srcdir}/vfs-ino.patch"

  # add BFQ scheduler
  patch -Np1 -i "${srcdir}/0001-block-cgroups-kconfig-build-bits-for-BFQ-${_bfq}.patch"
  patch -Np1 -i "${srcdir}/0002-block-introduce-the-BFQ-${_bfq}-I-O-sched.patch"
  patch -Np1 -i "${srcdir}/0003-block-bfq-add-Early-Queue-Merge-EQM-to-BFQ-${_bfq}.patch"
  patch -Np1 -i "${srcdir}/0004-Turn-into-BFQ-${_bfq}-for-${_basekernel}.0.patch"

  if [ "${CARCH}" = "x86_64" ]; then
    cat "${srcdir}/config.x86_64" > ./.config
  else
    cat "${srcdir}/config" > ./.config
  fi

  cat "${srcdir}/config.aufs" >> ./.config

  if [ "${_kernelname}" != "" ]; then
    sed -i "s|CONFIG_LOCALVERSION=.*|CONFIG_LOCALVERSION=\"${_kernelname}\"|g" ./.config
    sed -i "s|CONFIG_LOCALVERSION_AUTO=.*|CONFIG_LOCALVERSION_AUTO=n|" ./.config
  fi

  # set extraversion to pkgrel
  sed -ri "s|^(EXTRAVERSION =).*|\1 -${pkgrel}|" Makefile

  # don't run depmod on 'make install'. We'll do this ourselves in packaging
  sed -i '2iexit 0' scripts/depmod.sh

  # normally not needed
  make clean

  # get kernel version
  make prepare

  # load configuration
  # Configure the kernel. Replace the line below with one of your choice.
  #make menuconfig # CLI menu for configuration
  #make nconfig # new CLI menu for configuration
  #make xconfig # X-based configuration
  #make oldconfig # using old config from previous kernel version
  # ... or manually edit .config

  # rewrite configuration
  yes "" | make config >/dev/null
}

build() {
  cd "${srcdir}/linux-${_basekernel}"

  # build!
  make ${MAKEFLAGS} LOCALVERSION= bzImage modules
}

package_linux49() {
  pkgdesc="The ${pkgbase/linux/Linux} kernel and modules"
  depends=('coreutils' 'linux-firmware' 'kmod' 'mkinitcpio>=0.7')
  optdepends=('crda: to set the correct wireless channels of your country')
  provides=("linux=${pkgver}")
  install=${pkgname}.install

  cd "${srcdir}/linux-${_basekernel}"

  KARCH=x86

  # get kernel version
  _kernver="$(make LOCALVERSION= kernelrelease)"

  mkdir -p "${pkgdir}"/{lib/modules,lib/firmware,boot}
  make LOCALVERSION= INSTALL_MOD_PATH="${pkgdir}" modules_install
  cp arch/$KARCH/boot/bzImage "${pkgdir}/boot/vmlinuz-${_basekernel}-${CARCH}"

  # add kernel version
  if [ "${CARCH}" = "x86_64" ]; then
     echo "${pkgver}-${pkgrel}-MANJARO x64" > "${pkgdir}/boot/${pkgbase}-${CARCH}.kver"
  else
     echo "${pkgver}-${pkgrel}-MANJARO x32" > "${pkgdir}/boot/${pkgbase}-${CARCH}.kver"
  fi

  # set correct depmod command for install
  sed -e "s|%BASEKERNEL%|${_basekernel}|g;s|%KERNVER%|${_kernver}|g;s|%ARCH%|${CARCH}|g" \
  "${startdir}/${install}" > "${startdir}/${install}.pkg"
  true && install=${install}.pkg

  # install mkinitcpio preset file for kernel
  sed "s|%PKGBASE%|${pkgbase}|g;s|%BASEKERNEL%|${_basekernel}|g;s|%ARCH%|${CARCH}|g" "${srcdir}/${pkgbase}.preset" |
  install -D -m644 /dev/stdin "${pkgdir}/etc/mkinitcpio.d/${pkgbase}.preset"

  # install pacman hook for initramfs regeneration
  sed "s|%PKGBASE%|${pkgbase}|g;s|%BASEKERNEL%|${_basekernel}|g;s|%ARCH%|${CARCH}|g" "${srcdir}/${pkgbase}.hook" |
  install -D -m644 /dev/stdin "${pkgdir}/usr/share/libalpm/hooks/98-${pkgbase}.hook"

  # remove build and source links
  rm -f "${pkgdir}"/lib/modules/${_kernver}/{source,build}
  # remove the firmware
  rm -rf "${pkgdir}/lib/firmware"
  # gzip -9 all modules to save 100MB of space
  find "${pkgdir}" -name '*.ko' -exec gzip -9 {} \;
  # make room for external modules
  ln -s "../extramodules-${_basekernel}${_kernelname:--MANJARO}" "${pkgdir}/lib/modules/${_kernver}/extramodules"
  # add real version for building modules and running depmod from post_install/upgrade
  mkdir -p "${pkgdir}/lib/modules/extramodules-${_basekernel}${_kernelname:--MANJARO}"
  echo "${_kernver}" > "${pkgdir}/lib/modules/extramodules-${_basekernel}${_kernelname:--MANJARO}/version"

  # Now we call depmod...
  depmod -b "${pkgdir}" -F System.map "${_kernver}"

  # move module tree /lib -> /usr/lib
  mkdir -p "${pkgdir}/usr"
  mv "${pkgdir}/lib" "${pkgdir}/usr/"

  # add vmlinux
  install -D -m644 vmlinux "${pkgdir}/usr/lib/modules/${_kernver}/build/vmlinux" 
}

package_linux49-headers() {
  pkgdesc="Header files and scripts for building modules for ${pkgbase/linux/Linux} kernel"
  provides=("linux-headers=$pkgver")

  install -dm755 "${pkgdir}/usr/lib/modules/${_kernver}"

  cd "${srcdir}/linux-${_basekernel}"
  install -D -m644 Makefile \
    "${pkgdir}/usr/lib/modules/${_kernver}/build/Makefile"
  install -D -m644 kernel/Makefile \
    "${pkgdir}/usr/lib/modules/${_kernver}/build/kernel/Makefile"
  install -D -m644 .config \
    "${pkgdir}/usr/lib/modules/${_kernver}/build/.config"

  mkdir -p "${pkgdir}/usr/lib/modules/${_kernver}/build/include"

  for i in acpi asm-generic config crypto drm generated keys linux math-emu \
    media net pcmcia scsi sound trace uapi video xen; do
    cp -a include/${i} "${pkgdir}/usr/lib/modules/${_kernver}/build/include/"
  done

  # copy arch includes for external modules
  mkdir -p "${pkgdir}/usr/lib/modules/${_kernver}/build/arch/x86"
  cp -a arch/x86/include "${pkgdir}/usr/lib/modules/${_kernver}/build/arch/x86/"

  # copy files necessary for later builds, like nvidia and vmware
  cp Module.symvers "${pkgdir}/usr/lib/modules/${_kernver}/build"
  cp -a scripts "${pkgdir}/usr/lib/modules/${_kernver}/build"

  # fix permissions on scripts dir
  chmod og-w -R "${pkgdir}/usr/lib/modules/${_kernver}/build/scripts"
  mkdir -p "${pkgdir}/usr/lib/modules/${_kernver}/build/.tmp_versions"

  mkdir -p "${pkgdir}/usr/lib/modules/${_kernver}/build/arch/${KARCH}/kernel"

  cp arch/${KARCH}/Makefile "${pkgdir}/usr/lib/modules/${_kernver}/build/arch/${KARCH}/"

  if [ "${CARCH}" = "i686" ]; then
    cp arch/${KARCH}/Makefile_32.cpu "${pkgdir}/usr/lib/modules/${_kernver}/build/arch/${KARCH}/"
  fi

  cp arch/${KARCH}/kernel/asm-offsets.s "${pkgdir}/usr/lib/modules/${_kernver}/build/arch/${KARCH}/kernel/"

  # add docbook makefile
  install -D -m644 Documentation/DocBook/Makefile \
    "${pkgdir}/usr/lib/modules/${_kernver}/build/Documentation/DocBook/Makefile"

  # add dm headers
  mkdir -p "${pkgdir}/usr/lib/modules/${_kernver}/build/drivers/md"
  cp drivers/md/*.h "${pkgdir}/usr/lib/modules/${_kernver}/build/drivers/md"

  # add inotify.h
  mkdir -p "${pkgdir}/usr/lib/modules/${_kernver}/build/include/linux"
  cp include/linux/inotify.h "${pkgdir}/usr/lib/modules/${_kernver}/build/include/linux/"

  # add wireless headers
  mkdir -p "${pkgdir}/usr/lib/modules/${_kernver}/build/net/mac80211/"
  cp net/mac80211/*.h "${pkgdir}/usr/lib/modules/${_kernver}/build/net/mac80211/"

  # add dvb headers for external modules
  # in reference to:
  # http://bugs.archlinux.org/task/9912
  mkdir -p "${pkgdir}/usr/lib/modules/${_kernver}/build/drivers/media/dvb-core"
  cp drivers/media/dvb-core/*.h "${pkgdir}/usr/lib/modules/${_kernver}/build/drivers/media/dvb-core/"
  # and...
  # http://bugs.archlinux.org/task/11194
  mkdir -p "${pkgdir}/usr/lib/modules/${_kernver}/build/include/config/dvb/"
  cp include/config/dvb/*.h "${pkgdir}/usr/lib/modules/${_kernver}/build/include/config/dvb/"

  # add dvb headers for http://mcentral.de/hg/~mrec/em28xx-new
  # in reference to:
  # http://bugs.archlinux.org/task/13146
  mkdir -p "${pkgdir}/usr/lib/modules/${_kernver}/build/drivers/media/dvb-frontends/"
  cp drivers/media/dvb-frontends/lgdt330x.h "${pkgdir}/usr/lib/modules/${_kernver}/build/drivers/media/dvb-frontends/"
  mkdir -p "${pkgdir}/usr/lib/modules/${_kernver}/build/drivers/media/i2c/"
  cp drivers/media/i2c/msp3400-driver.h "${pkgdir}/usr/lib/modules/${_kernver}/build/drivers/media/i2c/"

  # add dvb headers
  # in reference to:
  # http://bugs.archlinux.org/task/20402
  mkdir -p "${pkgdir}/usr/lib/modules/${_kernver}/build/drivers/media/usb/dvb-usb"
  cp drivers/media/usb/dvb-usb/*.h "${pkgdir}/usr/lib/modules/${_kernver}/build/drivers/media/usb/dvb-usb/"
  mkdir -p "${pkgdir}/usr/lib/modules/${_kernver}/build/drivers/media/dvb-frontends"
  cp drivers/media/dvb-frontends/*.h "${pkgdir}/usr/lib/modules/${_kernver}/build/drivers/media/dvb-frontends/"
  mkdir -p "${pkgdir}/usr/lib/modules/${_kernver}/build/drivers/media/tuners"
  cp drivers/media/tuners/*.h "${pkgdir}/usr/lib/modules/${_kernver}/build/drivers/media/tuners/"

  # add xfs and shmem for aufs building
  mkdir -p "${pkgdir}/usr/lib/modules/${_kernver}/build/fs/xfs/libxfs"
  mkdir -p "${pkgdir}/usr/lib/modules/${_kernver}/build/mm"
  cp fs/xfs/libxfs/xfs_sb.h "${pkgdir}/usr/lib/modules/${_kernver}/build/fs/xfs/libxfs/xfs_sb.h"

  # copy in Kconfig files
  for i in $(find . -name "Kconfig*"); do
    mkdir -p "${pkgdir}"/usr/lib/modules/${_kernver}/build/`echo ${i} | sed 's|/Kconfig.*||'`
    cp ${i} "${pkgdir}/usr/lib/modules/${_kernver}/build/${i}"
  done

  # add objtool for external module building and enabled VALIDATION_STACK option
  if [ -f tools/objtool/objtool ]; then
    mkdir -p "${pkgdir}/usr/lib/modules/${_kernver}/build/tools/objtool"
    cp -a tools/objtool/objtool ${pkgdir}/usr/lib/modules/${_kernver}/build/tools/objtool/
  fi

  chown -R root.root "${pkgdir}/usr/lib/modules/${_kernver}/build"
  find "${pkgdir}/usr/lib/modules/${_kernver}/build" -type d -exec chmod 755 {} \;

  # strip scripts directory
  find "${pkgdir}/usr/lib/modules/${_kernver}/build/scripts" -type f -perm -u+w 2>/dev/null | while read binary ; do
    case "$(file -bi "${binary}")" in
      *application/x-sharedlib*) # Libraries (.so)
        /usr/bin/strip ${STRIP_SHARED} "${binary}";;
      *application/x-archive*) # Libraries (.a)
        /usr/bin/strip ${STRIP_STATIC} "${binary}";;
      *application/x-executable*) # Binaries
        /usr/bin/strip ${STRIP_BINARIES} "${binary}";;
    esac
  done

  # remove unneeded architectures
  rm -rf "${pkgdir}"/usr/lib/modules/${_kernver}/build/arch/{alpha,arc,arm,arm26,arm64,avr32,blackfin,c6x,cris,frv,h8300,hexagon,ia64,m32r,m68k,m68knommu,metag,mips,microblaze,mn10300,openrisc,parisc,powerpc,ppc,s390,score,sh,sh64,sparc,sparc64,tile,unicore32,um,v850,xtensa}

  # remove a files already in linux-docs package
  rm -f "${pkgdir}/usr/lib/modules/${_kernver}/build/Documentation/kbuild/Kconfig.recursion-issue-01"
  rm -f "${pkgdir}/usr/lib/modules/${_kernver}/build/Documentation/kbuild/Kconfig.recursion-issue-02"
  rm -f "${pkgdir}/usr/lib/modules/${_kernver}/build/Documentation/kbuild/Kconfig.select-break"
}

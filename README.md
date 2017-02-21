# linux49.9
manjaro linux kernel 4.9.9 bisect

    git bisect start
    # good: [c8ea2f3b8247b6046f02527127ecf2fd0b045f46] Linux 4.9.8
    git bisect good c8ea2f3b8247b6046f02527127ecf2fd0b045f46
    # bad: [d2e4b66b4ef24aeecb0cdef7278aa00850461de9] Linux 4.9.9
    git bisect bad d2e4b66b4ef24aeecb0cdef7278aa00850461de9
    # good: [04eb7db25bb1bcf4ee1631d1099fc03308929c12] mmc: sdhci: Ignore unexpected CARD_INT interrupts
    git bisect good 04eb7db25bb1bcf4ee1631d1099fc03308929c12
    # good: [8bc382a9652bc17277caf2c3d9dad6d0b55bb7db] USB: serial: qcserial: add Dell DW5570 QDL
    git bisect good 8bc382a9652bc17277caf2c3d9dad6d0b55bb7db
    # good: [5f0ee562605b4290959675830273d5485616d0cd] iio: health: afe4404: retrieve a valid iio_dev in suspend/resume
    git bisect good 5f0ee562605b4290959675830273d5485616d0cd
    # skip: [e02136282296dbc90f3c88b1cc5202ec0d5ed9f1] irqdomain: Avoid activating interrupts more than once
    git bisect skip e02136282296dbc90f3c88b1cc5202ec0d5ed9f1
    # good: [13363b6988f60be9f75146a52476a5e8d55f503c] x86/irq: Make irq activate operations symmetric
    git bisect good 13363b6988f60be9f75146a52476a5e8d55f503c
    # good: [72cd604cfd864b06c5a10d2bb139b19825e0fcbc] fs: break out of iomap_file_buffered_write on fatal signals
    git bisect good 72cd604cfd864b06c5a10d2bb139b19825e0fcbc
    # bad: [f2a0409a08502d64fbe3990354dff5902b08d2fb] drm/i915/execlists: Reset RING registers upon resume
    git bisect bad f2a0409a08502d64fbe3990354dff5902b08d2fb
    # first bad commit: [f2a0409a08502d64fbe3990354dff5902b08d2fb] drm/i915/execlists: Reset RING registers upon resume

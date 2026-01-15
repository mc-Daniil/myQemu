Build
```
cd qemu-9.2.0
mkdir build && cd build
../configure --target-list=x86_64-softmmu --enable-sdl --disable-werror --enable-slirp
ninja
```

Run Alpine
```
./qemu-img create -f qcow2 alpine.qcow2 8G
./qemu-system-x86_64 -m 512 -boot once=d -cdrom ../../alpine-standard-3.23.2-x86_64.iso -drive file=alpine.qcow2 -enable-kvm -nographic
Ctrl+A - c - trigger-vmexit
```

Edited files:
1. hmp-commands.hx (new command trigger-vmexit and documentation)
2. monitor/hmp-cmds.c (Function `hmp_trigger_vmexit`)
3. include/monitor/hmp.h (Header for new function)
# qemu_arm64_uboot
git clone https://github.com/u-boot/u-boot.git -b v2022.07

make qemu_arm64_defconfig

make

On Buildroot select bootloaders->uboot->qemu_arm64 


Follow the link https://schspa.tk/2019/10/22/uboot-online-debug.html

(gdb) p/x ((gd_t *)$x18)->relocaddr

$8 = 0x7ff12000

(gdb) add-symbol-file u-boot $8


qemu callstack   
#0  armv8_switch_to_el2 () at arch/arm/cpu/armv8/transition.S:30->br x4 //x4 is kernel entry point   
#1  0x00000000476d4ca4 in boot_jump_linux (images=0x477d1e88, flag=<optimized out>) at arch/arm/lib/bootm.c:326  
#0  do_bootm_linux (flag=256, argc=3, argv=0x466c2fb8, images=0x477d1e88) at arch/arm/lib/bootm.c:385  
#1  0x00000000476d5f98 in do_bootm_states (cmdtp=0x477a6c28, flag=0, argc=3, argv=0x466c2fb8, states=5904, images=0x477d1e88, boot_progress=<optimized out>)
    at boot/bootm.c:861  
#2  0x00000000477052b4 in cmd_call (repeatable=0x4659146c, argv=0x466c2fb0, argc=4, flag=0, cmdtp=0x477a6c28) at common/command.c:582  
#3  cmd_process (flag=<optimized out>, argc=4, argv=0x466c2fb0, repeatable=0x477d2f1c, ticks=0x0 <_start>) at common/command.c:637  
#4  0x00000000476fafc4 in run_pipe_real (pi=0x466c2e40) at common/cli_hush.c:1675  
#5  run_list_real (pi=0x466c2e40, pi@entry=0x4 <_start+4>) at common/cli_hush.c:1872  
#6  0x00000000476fb150 in run_list (pi=0x4 <_start+4>) at common/cli_hush.c:2021  
#7  parse_stream_outer (inp=0x0 <_start>, inp@entry=0x46591620, flag=flag@entry=5) at common/cli_hush.c:3211  
#8  0x00000000476fa8bc in parse_string_outer (flag=5, s=0x0 <_start>) at common/cli_hush.c:3283  
#9  parse_string_outer (s=0x0 <_start>, flag=5) at common/cli_hush.c:3261  
#10 0x00000000476fad9c in run_pipe_real (pi=0x466b3de0) at common/cli_hush.c:1636  
#11 run_list_real (pi=0x466b3de0, pi@entry=0x466c2e00) at common/cli_hush.c:1872  
#12 0x00000000476fb150 in run_list (pi=0x466c2e00) at common/cli_hush.c:2021  
#13 parse_stream_outer (inp=0x466c2c80, inp@entry=0x465917f0, flag=flag@entry=3) at common/cli_hush.c:3211  
#14 0x00000000476fa870 in parse_string_outer (flag=3, s=0x466c2c80 "") at common/cli_hush.c:3277  
#15 parse_string_outer (s=0x466c2c80 "", flag=3) at common/cli_hush.c:3261  
#16 0x00000000476d7f00 in qfw_boot (dev=<optimized out>, bflow=<optimized out>) at boot/bootmeth_qfw.c:65  //QEMU uboot  
#17 0x00000000476dac58 in bootflow_boot (bflow=<optimized out>) at boot/bootflow.c:510  

#0  announce_dram_init () at common/board_f.c:204  
#1  0x0000000000083c34 in initcall_run_list (init_sequence=init_sequence@entry=0xaa1c8 <init_sequence_f>) at lib/initcall.c:74  
#2  0x0000000000029e14 in board_init_f (boot_flags=<optimized out>) at common/board_f.c:974  
#3  0x00000000000029e8 in _main () at arch/arm/lib/crt0_64.S:100  



<details>
<summary>⬆️Update Notes (May 30, 2025)</summary>

May 30, 2025

1. Fixed the issue of a spelling error in variable 223.


May 29, 2025

1. From now on, for each remote firmware update, the corresponding tag will be checked before each release. For example, for x86 firmware, it's [Update-x86]. If a similar firmware to be released is found, the old one will be deleted first, keeping only one, before the new one is released. This will prevent an excessive backlog.


May 25, 2025

1. Replace [Clean releases and workflows] ( New setup instructions are here )


May 24, 2025

1. Fixed an error that occurred when running the "[Free up Ubuntu disk space]" function. Previously, I was using the source code from the author " endersonmenezes ". I pulled it over and made some minor fixes, resulting in about 2-3GB more disk space after the fix.


May 19, 2025

1. Fixed some minor issues and added a cache clearing function. If you encounter strange errors during compilation, usually like "ERROR: target/linux failed to build.", it's likely due to caching. Unchecking the cache option and recompiling will clear the cache first, then cache it again during compilation. If you keep unchecking the cache during compilation, it's equivalent to never using the cache.


May 11, 2025

1. Several older LuCI branches have been removed from the Lienol source code. I've also removed the compilation of older LuCI branches from the official source code in my scripts, as well as older LuCI branches from Tianling. This is because Passwall and SSR-Plus update too quickly. The issue of not being able to compile NaiveProxy was fixed on April 24th, but it's not compiling again now. If you don't need to compile these, you can add them back yourself.


April 24, 2025

1. Fixed the issue where NaiveProxy could not be compiled in versions below 23.05.


April 23, 2025

1. I've reorganized the scripts. For versions 23.05 and below, compiling Passwall and SSR-Plus now requires using Shadowsocks-libev. Using Shadowsocks_Rust is problematic because Passwall updates too quickly, and outdated source code can cause compilation failures. For versions below 23.05, NaiveProxy has been removed.

2. The content of the diy-part.sh file has been slightly modified; do not copy it directly.

3. If you don't want to use this repository to compile, you can use the repository at https://github.com/281677160/actions-openwrt , which is the original version and has not been modified at all.


March 30, 2025

1. The option to select a server CPU for compilation has been removed. After testing, it's now almost entirely AMD CPUs of the same model that are visible. If the option to select a server CPU for compilation was used, it would continuously loop through the CPUs without actually compiling.


March 26, 2025

1. The repositories for " padavanonly " and " hanwckf " have been merged into the Mt798x repository.

2. Compiling using the hanwckf-21.02 branch means compiling the openwrt-21.02 branch from the hanwckf author's repository. Compiling using other branches means compiling the repository from the padavanonly author's repository. Both are closed-source MTK network card drivers.

3. The compileable device files for openwrt-23.05 and hanwckf-21.02 [mt7981 and mt7986] are all pulled from branch 2410 of the padavanonly author's repository. In other words, devices of the [mt7981 and mt7986] type are simultaneously synchronized with branch 2410 of the padavanonly author.


March 25, 2025

1. Fixed a compilation error in some source code where enabling the `export Enable_IPV6_function="1"` option caused a missing dependency and compilation error when selecting IPv6 in some source code.

2. Fixed a compilation error in some source code when the `export Enable_IPV4_function="1"` option was enabled. Some source code could not be fully cleared for IPv6 before compilation, which caused a compilation error.

3. Fixed the error "WARNING: Makefile 'package/feeds/danshui/v2raya/Makefile' has a dependency on 'kmod-nft-tproxy', which does not exist" when compiling older versions of the source code.


March 21, 2025

Fixed various issues caused by the script not being updated for a long time, and added the source code to the repository https://github.com/padavanonly/immortalwrt-mt798x-24.10.


January 14, 2024

This fixes the issue where the private repository cannot start compilation and synchronize updates to the upstream repository. Note that if you have set your repository as a private repository, the online firmware update function will not work because the private repository cannot be detected, and therefore cannot download the firmware from your private repository's releases.


September 2, 2023

Adding the "Free up Ubuntu disk space" feature resolves a recent compilation failure due to insufficient server space.


June 16, 2023

Fixed the issue where some source code could not compile the N1 firmware.

In some source code files, the "armvirt" folder has been changed to "armsr," and the device files have changed accordingly. To check the source code folder, look in the "target/linux" section of the corresponding source branch; it will either contain "armvirt" or "armsr."

Previous model files were typically as follows:

CONFIG_TARGET_armvirt=y
CONFIG_TARGET_armvirt_64=y
CONFIG_TARGET_armvirt_64_Default=y
Some of the current model files have been changed to:

CONFIG_TARGET_armvirt=y
CONFIG_TARGET_armvirt_64=y
CONFIG_TARGET_armvirt_64_DEVICE_generic=y
If the source code file is named "armsr", the device model file is typically:

CONFIG_TARGET_armsr=y
CONFIG_TARGET_armsr_armv8=y
CONFIG_TARGET_armsr_armv8_DEVICE_generic=y
The above specifications are for reference only. Please refer to the corresponding source code via SSH connection for further information.

June 11, 2023

1. The time setting for clearing Actions space operation records has been changed. Previously, it was calculated by day; now it is calculated by minute.

2. The method for cleaning up released firmware has been modified. It is still calculated based on the number of releases retained. By default, it will automatically retain [cloud-based online updates] and [rootfs.tar.gz format firmware packaged from Amlogic/Rockchip series]. Those not cleaned up need to be manually deleted. (A bug was discovered at 11:00 AM on June 11th: this cleanup method can only retrieve the first 30 releases. If your repository has more than 30 releases, it will not retrieve the later ones. Furthermore, if the number of released releases retained exceeds 30, no releases will be cleaned up. It is recommended that for releases exceeding 30, only the necessary ones should be retained for now, and the rest should be cleaned up. Then, in future use, avoid exceeding 30 releases for normal operation.)

4. Because it needs to be used in conjunction with the cleanup and release operation, the cloud name for online updates has changed. Only recompiled versions will work; previously compiled versions will not be detected.

5. Added automatic deletion functionality to the workflow that stops due to CPU switching servers during the filtering process.


June 3, 2023

1. Each compilation automatically checks the upstream repository version. If there are updates upstream, it automatically synchronizes. Synchronization is divided into minor and major version updates. Minor version updates will not change your existing device folders, such as the [diy, files, patches, seed] folder. Major version updates completely overwrite your current repository with the upstream repository. Regardless of the version number, backups are retained. A new [backups] folder will appear in the root directory, containing all files from your repository before the update. You can simply delete this folder if you no longer need it.

2. If the process encounters an error at the step of "Detecting files and comparing upstream versions," check if the upstream repository has been synchronized, or if your repository is missing any files that caused the process to stop.

3. diy-part.sh has been modified; some controls have been changed. Don't directly overwrite the old ones; configure them again.

4. The option to not use plugin packages from my repository has been removed. Now, plugin packages from my repository will always be used. This is because my repository includes local compilation. Having this option would require writing a lot more code, which is annoying, so I simply removed it.

5. Now you can directly delete folders on GitHub, so I've disabled the previous folder deletion function and only kept the function to create device-specific folders.

6. For source code that my repository can compile, if the upstream branch is added or removed, you can change the branch number accordingly. For example, Tianling's source code recently added [openwrt-23.05], which your repository doesn't have; you can add it yourself. Alternatively, if the upstream branch is removed, you'll encounter errors when pulling the source code during compilation; simply delete that branch number. Theoretically, it should support all branches, but the branch must be compileable. For instance, some branches haven't been updated in a long time, and basic dependencies haven't been changed, so they definitely won't compile. Also, some source code will encounter compilation errors when adding LUCI.

7. Fixed the issue where I couldn't modify the plugin names in the collection of plugin packages in diy-part.sh settings. Now you should be able to change them freely, as long as the names you enter are accurate.

8. Those functions like uploading to cloud storage are basically disabled because the author hasn't updated the repository source code. I'm too lazy to fix them anymore, so I've removed those functions from my repository. If anyone knows how to fix them, they can go to the repository for the upload function and modify it to work.


May 13, 2023

1. All plugin packages in the source code have been reorganized. Due to technical limitations, Docker cannot be added to the gl-ax1800 source code. Some source code cannot compile the NaiveProxy for SSRplus and Passwall. Some source code's VSSR and iStore can compile successfully but are not usable. We need to check if any other plugins have this issue.

2. Firmware compiled from the gl-ax1800 source code cannot be directly converted to Xwrt firmware. Installation will result in errors and the system will freeze. If you are using firmware compiled from the gl-ax1800 source code and want to use Xwrt firmware, be sure to first install any other author's firmware onto the gl-ax1800 source code before installing the Xwrt firmware.

3. I've reorganized all the theme plugins from the source code. Some themes are too old and don't support many newer plugins. While some newer plugins have misaligned names in the theme, which isn't a big deal since they're still visible and configurable, many themes simply don't display the plugin's existence, or have different names even though they're essentially the same. So I removed those themes. (For LUCI 18.06, some good themes include luci-theme-argon, luci-theme-design, luci-theme-opentopd, and luci-theme-kucat. For themes after 19.07, there are very few options left. Thanks to the authors of these themes for their hard work.)

4. Regardless of whether luci-theme-argon is included in the source code, I have replaced it with the luci-theme-argon theme by jerrykuku.

5. In the custom settings, you can only choose one of (export Enable_IPV6_function="0"), (export Enable_IPV4_function="0"), and (export Create_Ipv6_Lan="0") to enable. If you enable all of them at the same time, only (export Enable_IPV6_function="1") will be enabled.

6. After each firmware installation and code execution, everything will run smoothly and then reboot. You can access the firmware through the background page after the code execution is complete. However, because it reboots every few tens of seconds (approximately 20-30 seconds for everything to finish running, slightly longer if there are many processes), some people may modify settings without saving them. Since the time is short, there's not enough time to save, leading to a situation where you think you've made changes, but later find they haven't. You should wait for the reboot before making any further settings. If you encounter this problem, please don't panic.


April 22, 2023

1. The autobuild repository has been merged here. Those who previously pulled the autobuild repository should no longer be able to use it. Please pull this repository again. The old build-actions repository also needs to be pulled again to use the new build-actions repository (please do not continue to pull and use the autobuild repository, this is my personal repository).

2. The compilation tutorial has been completely revised. If you still can't start compiling after following the tutorial, I can only say watch it a few more times.

3. Added the option to compile source code, allowing free switching between source code branches of the same author's source code (which branches can be selected for each author's source code are specified in the settings.ini file).

4. Amlogic firmware does not limit itself to a single source code. Theoretically, any source code that can compile into a rootfs.tar.gz package should be usable. Commonly used sources include (Tianling's openwrt-21.02 branch, Da Diao's master branch, and the official master branch). Firmware compilation and packaging are performed in two separate steps, eliminating issues of insufficient packaging space or compilation/packaging time. The already compiled rootfs.tar.gz file can be manually packaged multiple times using the packaging program. (Updated Amlogic and Rockchip firmware packaging setup tutorial)

5. The luci-app-oscam plugin fails to compile via cloud. Do not select this plugin when compiling via cloud. Local compilation, however, can be successful.

6. The source code for the Da Diao (大雕) software may encounter compilation errors when adding the mac80211 driver to some devices. If this occurs, please contact the source code author with the log files for assistance.

7. I've added the "gl-ax1800" branch to the repository. This isn't the branch from https://github.com/coolsnowwolf/lede , but rather the source code from another repository : https://github.com/coolsnowwolf/openwrt-gl-ax1800 . It seems to be specifically designed for the gl-ax1800 router. I've looked at it and tested it; it's essentially a 4.14 kernel source code. Anyone who needs this kernel can use this branch to compile.
</details>

---

<details>
<summary>🔎Various tutorials</summary>



GitHub Actions Compilation Tutorial

Amlogic and Rockchip series firmware packaging and setup tutorial

Instructions for Online Firmware Update Plugins

</details>

---

<details>
<summary>📳Local translation</summary>


One-click compilation of OpenWrt firmware on local Ubuntu

</details>

---

###Acknowledgements!
Thanks to the following experts (in no particular order)

coolsnowwolf Lienol immortalwrt openwrt x-wrt P3TERX Hyy2001X dhxh ophub nicholas-opensource hx210 hyird World Peace klever1988 actions svenstaro jerrykuku

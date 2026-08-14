## Hi there 👋

<!--

**Here are some ideas to get you started:**

🙋‍♀️ A short introduction - what is your organization all about?
🌈 Contribution guidelines - how can the community get involved?
👩‍💻 Useful resources - where can the community find your docs? Is there anything else the community should know?
🍿 Fun facts - what does your team eat for breakfast?
🧙 Remember, you can do mighty things with the power of [Markdown](https://docs.github.com/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)
-->
# Features
✅ GPU加速
<br>
✅ MPP硬件编解码
<br>
✅ 虚拟WIFI
<br>
✅ 虚拟Sensor
<br>
🈚️ 虚拟Camera
<br>
🈚️ 虚拟Mic
<br>
🈚️ 虚拟GPS
<br>
🈚️ 虚拟电源
<br>

# Build Android Image
```bash
#!/bin/bash
. build/envsetup.sh
lunch aosp_dodroid-userdebug
# lunch aosp_dodroid-eng

export TARGET_BOARD_PLATFORM_GPU=mali-G52
export TARGET_RK_GRALLOC_VERSION=4

m
```

# Build Docker Image
```bash
#!/bin/bash
cd out/target/product/dodroid

mount system.img system -o ro
mount vendor.img vendor -o ro

docker rmi dodroid 2>/dev/null

tar --xattrs -c vendor -C system --exclude="./vendor" . | DOCKER_DEFAULT_PLATFORM=linux/arm64 docker import -c 'ENTRYPOINT ["/init", "androidboot.hardware=mali"]' - dodroid

umount system vendor

docker save dodroid -o ../../../../dodroid.img
```

# AppImage Installation Scripts

## Another one?

This is yet another set of installation scripts for AppImages. The difference? AppImages are decompressed and integrated into the system. This may seem to go against what AppImages are, but believe me when I tell ya that there are very important reasons to do this

## I can explain...

My distribution is a live system, which is more or less what people call nowadays an "immutable system". Updating or adding new software through the package manager can be very time consuming and frustrating, so at first I came up with the idea of just bundling AppImages into the system and then compressing it However, due to how compression works, the size of the resulting SQUASHFS image increased drammatically with each new AppImage I added to my system, because they were not being compressed. At first It wasn't a problem for me, I knew why the compressed filesystem was getting larger, but I kept adding more and more AppImages into my system, increasing the size by a lot, until I considered "maybe I should to something about this"

Paralel to this, I was getting concerned about the performance of some AppImages and there were also some unexpected issues when running internal scripts from AppImages in side a chroot, for this specific issue  at first I thought that the solution was to permanently mount them or something

So I came up with the idea of decompressing the AppImages and then let mksquashfs do the compression on everything, and the results were very positive

# Size comparison

In these two pictures I am comparing two versions of my system, one with AppImages inside, compressed, (which is heavy af) and a more recent one (the one with the date in the filename)

<img width="1920" height="1080" alt="Real size of decompressed AppImages" src="https://github.com/carlos-a-g-h/aimgin-scripts/blob/main/2026-05-22-142414_1920x1080_scrot.png?raw=true" />

<img width="1920" height="1080" alt="The new compressed filesystem with decompressed AppImages is smaller" src="https://github.com/carlos-a-g-h/aimgin-scripts/blob/main/2026-05-22-142133_1920x1080_scrot.png?raw=true" />

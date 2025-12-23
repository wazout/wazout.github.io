---
title: Rescuezilla - Linux Cloning Made Easy
date: 2025-12-22 12:00:00 -0800
categories: [Hardware, Software]
tags: [rescuezilla, apple, upgrade, ssd]   #TAG names should always be lowercase
image: /assets/rescuezilla.jpg
---


While cleaning out my closet, I stumbled upon my 2015 MacBook Pro. You can’t deny how amazing its build quality is. Mine shipped with 16 GB of RAM and a 128 GB SSD. This MacBook also has a brand‑new Retina display, thanks to Apple’s “*delamination gate*.”

I wanted that same hardware quality in a Linux machine, so I installed Pop!_OS to test it. Everything worked almost perfectly, except the SSD was too small and the battery lasted only about three hours. After picking up a new battery, a 1 TB NVMe SSD, an NVMe enclosure, an NVMe adapter, and spending roughly $300, I was ready for a new daily driver.

The next challenge was cloning the internal SSD to the new one. After a quick web search, I discovered Rescuezilla, an open‑source GUI front‑end for Clonezilla that simplifies the cloning process.

Let’s walk through the steps I took to upgrade the internal SSD. First, you will need to create a Rescuezilla bootable USB drive.

## Create a Rescuezilla Bootable USB Drive

1. Go to **rescuezilla.com** and download the latest stable release (e.g., v2.6.1).
2. Download and install **Balena Etcher**.
3. Open Balena Etcher and click **Flash from file**.
4. Select the downloaded Rescuezilla `.iso` file.
5. Click **Select target** and choose your USB flash drive.
6. Click **Flash** and wait for the process to finish.

> This will erase the USB drive, so make sure there’s nothing important on it.
{: .prompt-danger }

Once complete, you now have a bootable Rescuezilla USB.

Next, eject the USB drive, run BleachBit as root and clean everything except “Free Disk Space.” Power down the computer, then insert both the Rescuezilla USB and the SSD you want to clone to, and boot the machine into Rescuezilla.

## Clone The Internal Drive

1. Select your preferred language with the arrow keys, then hit **Enter**.
2. Choose **Start Rescuezilla** and hit **Enter**.
3. You should now see the start page below.
4. Click **Clone** read the description, and click **Next.**
5. Rescuezilla will list all detected drives. Select the **Source Drive** (your internal drive), then click **Next.**
6. Select the **Destination Drive** (your new SSD), then click **Next.**
7. Click **Next** again to include all partitions.
8. Review the summary and click **Next** to start cloning.
9. Click **Yes** to acknowledge that the destination drive will be erased.
10. A backup summary will be shown; click **Next** to finish.
11. Exit the application to return to the home screen (image below).

You now have a bootable clone of your original drive. Because the new SSD is larger than the original, the main partition needs to be expanded to take full advantage of the extra space. Rescuezilla includes GParted, making this easy.

## Expand The Clone to Include All Available Disk Space

1. Double‑click the **GParted** shortcut on the desktop.
2. Ensure the new SSD is selected in the top‑right dropdown. If your SSD is encrypted, you’ll see a small “swap” partition immediately after the main partition, followed by unallocated free space that we need to absorb.
3. Right‑click the **swap** partition and select **Resize/Move**.
4. Set **Free space following** to 0 and press **Enter**. (The previous “following” value moves to “preceding.”)
5. Click **Resize/Move**, then click the green check‑mark ✅ at the top and choose **Apply**.
6. Right‑click the **main partition** and select **Resize/Move**.
7. Set **New size** to 2 000 000 (2 TB) – GParted will cap this at the maximum available size.
8. Ensure both **Free space preceding** and **Free space following** are set to 0.
9. Click **Resize/Move**, then the green check‑mark ✅ and **Apply** again.
10. Close GParted and shut down the computer using the menu in the bottom-left corner.

You can now replace the internal SSD with the new, larger one. You can also add Rescuezilla to a Ventoy drive.

## Final Thoughts

Rescuezilla turns the traditionally command‑line‑heavy Clonezilla workflow into a point‑and‑click experience, making full‑disk cloning accessible even to newcomers. Pair it with BleachBit for pre‑clone cleanup and GParted for post‑clone resizing, and you have a reliable, end‑to‑end solution for SSD upgrades, system migrations, or quick disaster recovery.
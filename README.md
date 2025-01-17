# LineageOS device tree for the Samsung Galaxy S10

Description
-----------

This repository is to build LineageOS for the S10 (SM-G973F)

How to build LineageOS
----------------------

* Make a workspace:

        mkdir -p ~/lineageos/repo
        cd ~/lineageos/repo

* Initialize the repo:

        repo init -u git://github.com/LineageOS/android.git -b lineage-18.1

* Create a local manifest:

        vim .repo/local_manifests/roomservice.xml

        <?xml version="1.0" encoding="UTF-8"?>
        <manifest>
            <project name="whatanupdate/android_device_samsung_beyond1lte" path="device/samsung/beyond1lte" />
            <project name="whatanupdate/android_device_samsung_exynos9820-common" path="device/samsung/exynos9820-common" remote="github" />
            <project name="whatanupdate/android_kernel_samsung_exynos9820" path="kernel/samsung/exynos9820" remote="github" />
            <project name="whatanupdate/android_vendor_samsung_beyond1lte" path="vendor/samsung/beyond1lte" remote="github" />
            <project name="LineageOS/android_device_samsung_slsi_sepolicy" path="device/samsung_slsi/sepolicy" remote="github" />
	    <project name="LineageOS/android_hardware_samsung" path="hardware/samsung" remote="github" />
        </manifest>

* Sync the repo:

        repo sync

* Extract vendor blobs

        cd device/samsung/beyond1lte
        ./extract-files.sh

* Setup the environment

        source build/envsetup.sh
        lunch lineage_beyond1lte-userdebug

* Build LineageOS

        m -j20 bacon

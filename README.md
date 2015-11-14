# Layer 7 Technologies - Policy Manager

Layer 7 Technologies was acquired by CA Technologies in 2013.

## Policy Manager as native Mac .app

CA (f.k.a. Layer 7 Technologies) does not ship a native Mac OS X app for the **CA API Gateway Policy Manager**. They only ship a folder with the jar file and also a shell script. As a Mac user you want a real Mac like .app for starting the app faster via your favorite app launcher.

There are different ways to package a native java app. The easiest one for for the non developer user is via `javapackager` in my mind. javapackager comes with your local java installation.

The fastest way is the following.
- Unpack Manager-9.0.00.tar.gz
- Change into the directory Manager-9.0.00
- Place an icon file in the directory (l7tech.icns)
- Build the app

Command to build the app

    /Library/Java/JavaVirtualMachines/jdk1.8.0_65.jdk/Contents/Home/bin/javapackager -deploy \
      -native \
      -name "CA API Gateway Policy Manager" \
      -title "CA API Gateway Policy Manager" \
      -appclass com.l7tech.console.Main \
      -outdir . \
      -outfile "CA API Gateway Policy Manager.app" \
      -srcfiles Manager.jar \
      -srcfiles lib \
      -srcfiles logging.properties \
      -Bruntime="/Library/Java/JavaVirtualMachines/jdk1.8.0_65.jdk" \
      -Bicon=l7tech.icns \
      -BappVersion=9.0.00 \
      -Bmac.CFBundleName="CA API Gateway Policy Manager" \
      -Bmac.CFBundleVersion=1.0

This process creates automatically an `Info.plist` with some default values. You can modify it later on with what you additionally want or need in it. I prefer the prepare an Info.plist file and let the build process use my file.

The following process shows the build with using customized files.
- Unpack Manager-9.0.00.tar.gz
- Change into the directory Manager-9.0.00
- Create the directory structure `package/macosx`
- Place an icon file in the *package/macosx* with the name `CA API Gateway Policy Manager.icns`
- Place the Info.plist file in the *package/macosx* with the name `Info.plist`
- Build the app

    /Library/Java/JavaVirtualMachines/jdk1.8.0_65.jdk/Contents/Home/bin/javapackager -deploy \
      -native \
      -name "CA API Gateway Policy Manager" \
      -title "CA API Gateway Policy Manager" \
      -appclass com.l7tech.console.Main \
      -outdir . \
      -outfile "CA API Gateway Policy Manager.app" \
      -srcfiles Manager.jar \
      -srcfiles lib \
      -srcfiles logging.properties \
      -Bruntime="/Library/Java/JavaVirtualMachines/jdk1.8.0_65.jdk"

The resulting app is in the folder `bundle` and is called **CA API Gateway Policy Manager.app**. As a last thing place the file `InfoPlist.strings` inside the .app in the folder `Contents/Resources`.  
The text from the InfoPlist.strings is shown when you click on **About Main** in the menu bar.


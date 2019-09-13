Title: Keeping the GTK style with Qt 5.7
Lang: en
Tags: qt, gtk

Since version 5.7, Qt has moved the qtstyle support from [qtbase](https://github.com/qt/qtbase/commit/899a815414e95da8d9429a4a4f4d7094e49cfc55)
to a [separate repository](https://github.com/qt/qtstyleplugins/commit/102da7d50231fc5723dba6e72340bef3d29471aa).
For the user that means that he can't just simply export `QT_STYLE_OVERRIDE=GTK+`
to make Qt applications use the GTK widget style and theme.

To get the old behaviour back, you need to install [qtstyleplugins](https://code.qt.io/cgit/qt/qtstyleplugins.git/).
Arch users can use [this PKGBUILD](https://github.com/dglava/pkgbuilds/blob/master/qt5-qtstyleplugins-git/PKGBUILD).
Once you have it installed, don't forget to export `QT_STYLE_OVERRIDE=gtk2`. Pay attention
to the **gtk2** value. Before the split, the environment variable's value was GTK+, but
now you have to set it to gtk2.

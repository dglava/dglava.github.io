Title: Zadržati GTK stil za Qt 5.7
Lang: bs
Tags: qt, gtk

Od verzije 5.7, Qt je odbacio podršku za GTK izgled *widgeta*. Ne potpuno,
nego je samo prebačen u drugi repozitorij. Do sada se nalazio u [qtbase](https://github.com/qt/qtbase/commit/899a815414e95da8d9429a4a4f4d7094e49cfc55),
ali je prebačen u [qtstyleplugins](https://github.com/qt/qtstyleplugins/commit/102da7d50231fc5723dba6e72340bef3d29471aa).
Za korisnike to znači da više ne mogu jednostavno eksportovati `QT_STYLE_OVERRIDE=GTK+`
da bi natjerali Qt programe da koriste GTK temu.

Da bi zadržali staro ponašanje i izgled, sada je potrebno instalirati
[qtstyleplugins](https://code.qt.io/cgit/qt/qtstyleplugins.git/). Arch
korisnici se mogu poslužiti [PKGBUILDom](https://github.com/dglava/pkgbuilds/blob/master/qt5-qtstyleplugins-git/PKGBUILD).
Nakon instalacije potrebno je eksportovati `QT_STYLE_OVERRIDE=gtk2`. Pažnju
posvetite na vrijednost **gtk2**. Do sada je korišteno GTK+, ali sa novim
načinom je potrebno promijeniti GTK+ u gtk2.

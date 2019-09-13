Title: Ukloni naslovnu traku kod maksimiziranih prozora
Lang: bs
Tags: openbox

Naslovna traka mi je jedino korisna kad pomjeram prozore. Iskreno
nije potrebna ni tad sa Openboxom, jer je moguće držati ALT
(po zadanim postavkama) i lijevim klikom pomjerati prozor. Razlog
zašto nisam potpuno uklonio trake je taj što je na laptopu nezgodno
držati ALT, dok na desktopu nemam problema.

Provjerio sam Openbox dokumentaciju i nisam naišao na rješenje.
Ne postoji način da se uvjetno mijenjaju postavke. Postavio sam pitanje
na Openbox [mailing listi](http://icculus.org/pipermail/openbox/2017-February/009285.html)
i ubrzo sam dobio rješenje.

[Orcsome](https://github.com/baverman/orcsome) je program koji
omogućava manipulaciju upravitelja prozorima koji su u skladu sa NETWM
standardom. Openbox je jedan od njih. Napisan je u Pythonu i koristi
Python za konfiguracijski fajl. Imao sam malo problema sa instalacijom.
Autor nije predvidio da će korisnici globalno instalirati program, što je
bilo problematično. No, greška je prijavljena i sve radi bez problema.
Napravio sam PKGBUILD za Arch, koji možete preuzeti [ovdje](https://github.com/dglava/pkgbuilds/blob/master/orcsome-git/PKGBUILD).
PKGBUILD je za najnoviju verziju sa gita. Ako želite objavljene verzije,
imate u [AURu](https://aur.archlinux.org/packages/orcsome/).

Mogućnosti su velike, ali meni treba samo dinamično prikazivanje
(dekoriranje) prozora pri makzimiziranju i ostalim stanjima prozora.
Ovo je dovoljno za željenu funkciju (preuzeto direktno od autora sa
*mailing liste*):

```
from orcsome import get_wm

wm = get_wm()

@wm.on_manage
def on_manage():
    @wm.on_property_change(wm.event_window, '_NET_WM_STATE')
    def property_was_set():
        w = wm.event_window
        if w.maximized_vert and w.maximized_horz:
            if w.decorated:
                wm.set_window_state(w, decorate=False)
        else:
            if not w.decorated:
                wm.set_window_state(w, decorate=True)
```

Fajl sam snimio pod `~/.config/orcsome/rc.py` i stavio da se Orcsome
pokreće automatski pri startu Openbox sesije (u autostart fajlu).

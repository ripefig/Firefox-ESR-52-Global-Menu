# Firefox-ESR-52-Global-Menu
libxul.so with unity patches applied. This is intended as way to make the global menu patches available for Firefox ESR 52 and Zotero.

# Instructions

I split libxul.so into five parts to avoid Github's file restrictions. To combine, enter the cloned directory and run the following command:

    cat x* > libxul.so


From there follow the instruction from this [Zotero bug report](https://github.com/zotero/zotero/issues/302)

> I've managed to get this working. Do the following, assuming that you already have a copy of Firefox with the unity patches applied:
> 
> 1. copy the `firefox` binary to overwrite `zotero-bin` (or make `zotero-bin` a symlink to `firefox`)
> 2. copy all the `*.so` files (including the directory `$LIBDIR/firefox/gtk2/`) into the zotero directory
> 3. add the following lines to `zotero.css` (in `zotero.jar`):
> 
> ```
> window[shellshowingmenubar="true"] menubar {
>   display: none !important;
> }
> 
> window[shellshowingmenubar="true"]
> toolbar[type="menubar"]:not([customizing="true"]) {
>   min-height: 0 !important;
>   border: 0 !important;
> }
> ```
> EDIT:
> 
> alternatively, change the last line of the script that launches `zotero` from
> 
> ```
> "$CALLDIR/zotero-bin" -app "$CALLDIR/application.ini" $*
> ```
> to
> 
> ```
> /path/to/firefox -app "$CALLDIR/application.ini" $*
> ```
> and place the CSS above in `~/.zotero/zotero/<profile id>.default/chrome/userChrome.css`



libxul.so was compiled for arch, meaning it won't work unless you can get a hold of a few fresh binaries. On my Ubuntu 18.10 system for example, this was [libicu63](https://launchpad.net/ubuntu/disco/+package/libicu63) and [libhunspell-1.7](https://packages.ubuntu.com/disco/amd64/libhunspell-1.7-0/download) from the Ubuntu 19.04 repositories. You can just download the deb packages and install them.

Running zotero-bin from the terminal should tell you what binaries you're missing.

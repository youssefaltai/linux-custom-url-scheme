# How to register custom URL schemes in Linux

First, create a desktop file in `/usr/share/applications/`

###### potato-handler.desktop

```
[Desktop Entry]
Name=Potato URL Handler
GenericName=Text Editor
Comment=Handle URL Scheme potato://
Exec=/usr/share/potato/potato-handler %u
Terminal=false
Type=Application
MimeType=x-scheme-handler/potato;
Icon=potato-icon
Categories=Development;Utility;
Name[en_US]=potato URL Handler
```

Then, update the MIME-types database, using:

```
sudo update-desktop-database
```

Check the `mimeinfo.cache` file.
This file is the cache database created by `update-desktop-database`.

You will probably find multiple ones, 
under `/applications` of every directory in `$XDG_DATA_DIRS`.

In the potato example, you should find an entry 
`x-scheme-handler/potato` with the value `potato-handler.desktop` 
in the `mimeinfo.cache` of `/usr/share/applications/`, since we created
the `potato-handler.desktop` file there.

Now, create the `/usr/share/potato/potato-handler` executable that
we specified in the `potato-handler.desktop`'s `Exec` field.

This executable should take _**exactly one**_ command-line argument,
which is the Potato URL starting with `potato://`, and launch your app
with the parameters it needs.

You can make this executable in Bash, Python, or whatever you prefer,
just make sure you specify in the `Exec` field of the `potato-handler.desktop`
how to execute it.

## Undoing what we just did

Just remove the directory `/usr/share/potato/` 
with the `potato-handler` executable inside it,
and remove the `potato-handler.desktop` file 
from `/usr/share/applications/`,
then update the MIME-types database once more, using:

```
sudo update-desktop-database
```



## Port

### list listening ports

```
sudo lsof -i -P -n | grep LISTEN
```

stop redis or other services
```
sudo systemctl stop redis
```


## LaTex

### installing physics
installed zip file from [this page](https://ctan.org/tex-archive/macros/latex/contrib/physics?lang=en).

then, place the folder under the following path.
/usr/share/texlive/texmf-dist/tex/latex

then, run the following
```
sudo texhash
```

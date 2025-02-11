

## Port

### list listening ports

```
sudo lsof -i -P -n | grep LISTEN
```

or

```
sudo ss -tulpn | grep LISTEN
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


## Chrome stable not updating
go to 
```/etc/apt/sources.list.d/```
edit google-chrome.list
uncomment the ```deb```
part



## tarball

extract tar.gz in a specific folder

```
tar -xvzf rails-new-x86_64-unknown-linux-gnu.tar.gz -C ~/Documents/GitLab/rails-new

```


```
./rails-new --ruby-version 3.4.1 --rails-version 8.0.1 consulchat-1 --devcontainer --database=postgresql --css=tailwind

```


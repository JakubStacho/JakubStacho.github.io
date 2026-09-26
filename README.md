## Personal Website GitHub Repo


### Hugo Setup on WSL
Need to install hugo locally before you start:
```bash
# update package list
sudo apt update

# install curl and wget
sudo apt install -y curl wget

# detect the latest hugo version
VER=$(curl -sL https://api.github.com/repos/gohugoio/hugo/releases/latest | grep tag_name | head -1 | sed 's/.*"v\([^"]*\)".*/\1/')

# check that it worked
echo "Latest Hugo version: $VER"

# download the extended .deb package
wget "https://github.com/gohugoio/hugo/releases/download/v${VER}/hugo_extended_${VER}_linux-amd64.deb" -O /tmp/hugo.deb

# install it
sudo dpkg -i /tmp/hugo.deb

# remove temp download file
rm -f /tmp/hugo.deb

# verify install
hugo version
```

Themes can be added to the hugo page repo as git submodules:
```bash
# add the pico corp theme once you cd into the hugo webpage repo
git submodule add https://github.com/PhantomPixelDev/hugo-theme-pico-corp.git themes/pico-corp

# multiple themes can all be installed as submodules
# once you decide on a theme you can uninstall and remove the unused themse:
git submodule deinit -f themes/old-theme-name
git rm -f themes/old-theme-name
rm -rf .git/modules/themes/old-theme-name
```

The site can be viewed locally for testing and debugging with
```bash
hugo server -D
```
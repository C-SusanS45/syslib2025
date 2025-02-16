# Managing Software

## Commands to Update, Upgrade, and Install Software

```
sudo apt update
sudo apt upgrade (add -y to skip prompt and automatically answer yes)
apt search
apt show
sudo apt install
sudo apt --purge remove
sudo apt autoremove
sudo apt clean
```

## Locate and Install Software

```
sudo apt update
apt search <package_name>
apt show <package_name>
sudo apt install <package_name>
```
Be sure to check last time the version was updated.

## Remove Software and Purge Related Files

```
sudo apt --purge remove <package_name>
sudo apt autoremove
sudo apt clean
```

## Keep System up to Date

```
sudo apt update
sudo apt upgrade
sudo apt autoremove
sudo apt clean
```
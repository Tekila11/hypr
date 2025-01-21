Here's how you can investigate and clean up space:

1. First, let's check what's taking up space. Run this command to see the largest directories in /:
```bash
sudo du -h --max-depth=1 / | sort -rh
```

2. For a more detailed view of package-related disk usage:
```bash
pacman -Qi | awk '/^Name/{name=$3} /^Installed Size/{print $4$5, name}' | sort -h
```

Common areas to check and clean:

1. Package cache:
- Check size: `du -sh /var/cache/pacman/pkg/`
- Clean old packages: `sudo paccache -r`
- Remove all cached packages: `sudo pacman -Scc`

2. Old log files:
```bash
sudo journalctl --vacuum-size=100M  # Limit journal size to 100MB
du -sh /var/log/  # Check log directory size
```

3. Remove orphaned packages:
```bash
sudo pacman -Rns $(pacman -Qtdq)
```

4. Clean temporary files:
```bash
sudo rm -rf /var/tmp/*
```

5. For a GUI tool, you can install and use `bleachbit`:
```bash
sudo pacman -S bleachbit
```


Alternative Solutions:
1. If cleaning doesn't provide enough space, you could resize your partitions using tools like `gparted` from a live USB
2. You might consider moving some directories to your /home partition and creating symlinks



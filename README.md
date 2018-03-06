# Test symbolic link with Git

This repostory is used for illustrate how Git works with symbolic link.

In my computer (Ubuntu 16.04), this repository is stored as

/home/ubuntu/tests/test_symlink

Two symlinks are created:

```bash
  ln -s ./data/example.txt relative_link.txt
  ln -s /home/ubuntu/tests/test_symlink/data/example.txt absolute_link.txt
```

In my working folder, all works well. Now when I push to Github, Github shows content of the two files as follow:

  - relative_link.txt: ./data/example.txt
  - absolute_link.txt: /home/ubuntu/tests/test_symlink/data/example.txt

(It is not what the content of these files actually are, just their representation by Github/GitBucket,etc. Their contents are kept as-is, but Git marks them as symbolic link.)

Now if I pull this repository to another location in another computer, say /opt/test_symblink, git creates 2 symlinks which keeps its link path, i.e. ./data/example.txt and /home/ubuntu/tests/test_symlink/data/example.txt respectively.

Of course relative_link.txt still works since its target, ./data/example.txt is there with the rest of the repository, but absolute_link.txt does not work since there is not /home/ubuntu/tests/test_symlink/data/example.txt anymore!

Where does it help ? Well, when you need to import a file (called "target file") from another project (called "target project") into your project. For instance, when I need to import a Ansible customized module which is developped in anohter project into my "library" folder. I cannot bring the whole project with its subfolders into "library", only the module file. For that I use Git submodule to import the whole target project into my project, then create a (relative) symbolic link to the target file.

#  Configuring Git Large File Storage 

GitHub limits the size of files allowed in repositories. To track files beyond this limit, you can use Git Large File Storage.
Git LFS handles large files by storing references to the file in the repository, but not the actual file itself. To work around Git's architecture, Git LFS creates a pointer file which acts as a reference to the actual file (which is stored somewhere else). GitHub manages this pointer file in your repository. When you clone the repository down, GitHub uses the pointer file as a map to go and find the large file for you.
Different maximum size limits for Git LFS apply depending on your GitHub plan.

*** If you exceed the per file limit of 5 GB, the file will be rejected silently by Git LFS.

- In order to use Git LFS, you'll need to download and install a new program that's separate from Git.
----------------
* Installing Git Large File Storage
```
wget https://github.com/git-lfs/git-lfs/releases/download/v3.4.0/git-lfs-linux-amd64-v3.4.0.tar.gz
```
1. On your computer, locate and unzip the downloaded file.

2. Change the current working directory into the folder you downloaded and unzipped.

3. cd ~/Downloads/git-lfs-1.X.X

Note: The file path you use after cd depends on your operating system, Git LFS version you downloaded, and where you saved the Git LFS download.

4. To install the file, run this command:
```
$ ./install.sh
> Git LFS initialized.
```
* Note: You may have to use sudo ./install.sh to install the file.

5. Verify that the installation was successful:
```
$ git lfs install
> Git LFS initialized.
```
-------------------
* Configuring Git Large File Storage
Once Git LFS is installed, you need to associate it with a large file in your repository.
If there are existing files in your repository that you'd like to use GitHub with, you need to first remove them from the repository and then add them to Git LFS locally.

------------------
* Moving a file in your repository to Git Large File Storage
After installing Git LFS and configuring Git LFS tracking, you can move files from Git's regular tracking to Git LFS.
1. Change your current working directory to an existing repository you'd like to use with Git LFS.
2. To associate a file type in your repository with Git LFS, enter git lfs track followed by the name of the file extension you want to automatically upload to Git LFS.
For example, to associate a .tar.gz file, enter the following command:
```
$ git lfs track "*.tar,gz"
> Adding path *.tar.gz
```
Every file type you want to associate with Git LFS will need to be added with git lfs track. This command amends your repository's .gitattributes file and associates large files with Git LFS.

3. Add a file to the repository matching the extension you've associated:
```
git add path/to/file.tar.gz && git commit -m "add file.tar.gz"
git push
```
You should see some diagnostic information about your file upload:
```
> Sending file.tar.gz
> 44.74 MB / 81.04 MB  55.21 % 14s
> 64.74 MB / 81.04 MB  79.21 % 3s
```
